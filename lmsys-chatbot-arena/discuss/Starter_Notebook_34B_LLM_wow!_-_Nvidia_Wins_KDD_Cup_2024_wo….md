# Starter Notebook 34B LLM wow! - Nvidia Wins KDD Cup 2024 wow!

**Chris Deotte** *Sat Jul 20 2024 10:19:17 GMT+0900 (日本標準時)* (151 votes)

Hi everyone. I would like to share a starter notebook showing how to infer a 34B LLM to infer 25k test samples under 9 hours [here](https://www.kaggle.com/code/cdeotte/infer-34b-with-vllm). Since there are only 2.5 weeks left, I won't share too much, but I'll share a few ideas.

# Use Quantization 4bit AWQ

In this competition we must infer on 2xT4 GPU 16GB VRAM. Therefore we have a total of 32GB VRAM. A 34B LLM in fp16 is 70GB size however when using 4bit it becomes 20GB size (i.e. X billion parameter models become 0.6X GB size in 4bit). Reducing a 34B LLM to 20GB will fit in 32GB VRAM Hooray!

# Infer Using vLLM

The test data is 25k samples therefore we must infer fast. We need to infer each sample on average 1.3 seconds! The library vLLM [here](https://docs.vllm.ai/en/latest/) is faster than Hugging Face and pure PyTorch code! It will easily infer 1 second per sample or less!

# Starter Notebook

I publish a starter notebook [here](https://www.kaggle.com/code/cdeotte/infer-34b-with-vllm) demonstrating how to infer 34B LLM in Kaggle's LMSYS competition to complete 25k test predictions in under 9 hours! My starter notebook illustrates a few tricks:

- How to install vLLM in Kaggle notebooks

- How to use logits processor to force our model to only output "A", "B", "tie"

- How to extract probabilities from these 3 tokens

- How to optimize input token length and output token length

- How to format LLM prompts

# KDD Cup 2024

This year I had the opportunity to team up with 5 NVIDIAN coworkers in KDD Cup 2024 [@aerdem4](https://www.kaggle.com/aerdem4) [@titericz](https://www.kaggle.com/titericz) [@sorokin](https://www.kaggle.com/sorokin) [@simjeg](https://www.kaggle.com/simjeg) [@benediktschifferer](https://www.kaggle.com/benediktschifferer) . The challenge was to build an LLM to answer 11k ecommerce questions under 2 hours using 4xT4 for inference. Competition page [here](https://www.aicrowd.com/challenges/amazon-kdd-cup-2024-multi-task-online-shopping-challenge-for-llms). I learned so much from my fellow NVIDIA Kaggle Grandmasters (KGMON [here](https://www.nvidia.com/en-us/ai-data-science/kaggle-grandmasters/)), Thank you! Our collective ideas earned us 1st place on all 5 tracks of KDD Cup 2024 wow! (LB [here](https://www.aicrowd.com/challenges/amazon-kdd-cup-2024-multi-task-online-shopping-challenge-for-llms/leaderboards))

# Solution

Our solution involved these 3 key components:

- Generate lots of train data

- Finetune largest model possible with QLoRA

- Infer as fast as possible on limited hardward within time constraint

At the end of August we will present our KDD Cup solution live in Barcelona, Spain at KDD Cup 2024 conference, and we will publish a paper. Stay tuned to hear all the details!



---

 # Comments from other users

> ## Anish Vijay
> 
> excellent!
> 
> 
> 


---

> ## hwz13
> 
> 很清晰！very clear
> 
> 
> 


---

> ## kaggk
> 
> Brilliant！
> 
> 
> 


---

> ## Timmy Juicehouse
> 
> Glad to see you here Chris, and congratulation to your Nvidia team. We team also won a good rank but you are much stronger than us. I need to prepare for my wedding next month and cannot leave for Barcelona. I'm looking forward to your solution in Kdd2024. 
> 
> 
> 


---

> ## Metin Meki Abullrahman
> 
> N!ce Work 😍
> 
> 
> 


---

> ## Cindy Y
> 
> Very good! 
> 
> 
> 


---

> ## Kid Liu
> 
> Nice work!
> 
> 
> 


---

> ## Sanket Pramod Bhure
> 
> wow Great work!
> 
> 
> 


---

> ## Liuyanfen166
> 
> Nice work!
> 
> 
> 


---

> ## Rise_Hand
> 
> Great job always! I have a small question that according to my view, different models have different tricks which based on their structure and hyper-parameters. So what should we do to make less cost from past experience, namely how should we trade off between the cost and best results from new different models based on our past experience?
> 
> 
> 


---

> ## YingxiZhang
> 
> wow~~~nice work
> 
> 
> 


---

> ## Cody_Null
> 
> I see you talk about generating data. Is that done with something like this/ do you have like a go to template? 
> 
> ```
> %pip install -q -U ipywidgets
> %pip install -q -U transformers
> %pip install -q -U tokenizers
> %pip install -q -U bitsandbytes
> %pip install -q -U torch
> 
> import pandas as pd
> from tqdm import tqdm
> import torch
> from huggingface_hub import login
> from transformers import AutoModelForCausalLM, AutoTokenizer, BitsAndBytesConfig
> import random
> 
> # Define base prompts and parameters
> base_prompts = [
>     "Generate a single response that would likely merit a reply (Score: 8 to 10) and provide a score from 1 to 10 indicating how probable it is that the response would merit a reply. Examples: 'How can I help you today?' - 10, 'What's your name?' - 10, 'Tell me more about that.' - 9. Format: 'response' - score.",
>     "Generate a single response that might merit a reply (Score: 6 to 7) and provide a score from 1 to 10 indicating how probable it is that the response would merit a reply. Examples: 'Hello there!' - 6, 'Good morning.' - 7. Format: 'response' - score.",
>     "Generate a single response that would likely not merit a reply (Score: 4 to 5) and provide a score from 1 to 10 indicating how probable it is that the response would merit a reply. Examples: 'I don't know.' - 5, 'Maybe you are right, I can look into that.' - 4. Format: 'response' - score.",
>     "Generate a single response with a low probability of meriting a reply (Score: 1 to 3) and provide a score from 1 to 10 indicating how probable it is that the response would merit a reply. Examples: 'Yes.' - 3, 'No.' - 2, 'Umm' - 1. Format: 'response' - score."
> ]
> num_convos = 10000
> batch_size = 128  # Adjust based on your GPU memory
> max_length = 512  # Adjust based on desired response length
> 
> # Model and tokenizer configurations
> model_name = "google/gemma-2-9b"   #"mistralai/Mistral-7B-Instruct-v0.3"  #"meta-llama/Meta-Llama-3-8B-Instruct"
> bnb_config = BitsAndBytesConfig(
>     load_in_4bit=True,
>     bnb_4bit_compute_dtype=torch.float16
> )
> 
> # Log in to Hugging Face
> login(token="hf_JB")
> 
> # Load model and tokenizer
> model = AutoModelForCausalLM.from_pretrained(
>     model_name,
>     quantization_config=bnb_config,
>     device_map="auto",
>     token="hf_JB"
> )
> tokenizer = AutoTokenizer.from_pretrained(model_name, token="hf_JB")
> 
> # Set the pad_token to eos_token
> tokenizer.pad_token = tokenizer.eos_token
> 
> # Set up the device and check GPU availability
> torch.backends.cuda.enable_mem_efficient_sdp(False)
> torch.backends.cuda.enable_flash_sdp(False)
> if not torch.cuda.is_available():
>     raise EnvironmentError("Sorry - GPU required!")
> DEVICE = torch.device("cuda")
> 
> # Specify data extraction
> def extract_data(outputs, base_prompt):
>     convos = []
>     labels = []
>     for output in outputs:
>         response = tokenizer.decode(output, skip_special_tokens=True).strip()
> 
>         # Remove the base prompt from the response
>         if response.startswith(base_prompt):
>             response = response[len(base_prompt):].strip()
> 
>         # Extract response and score
>         if " - " not in response:
>             print('no - in output')
>             continue
> 
>         try:
>             response_text = response.split(' - ')[0].strip().strip('"')
>             score = int(response.split(' - ')[1][:2].strip())
> 
>             # Ensure score is within the expected range
>             if score < 1 or score > 10:
>                 print('invalid score')
>                 continue
> 
>         except (IndexError, ValueError):
>             print('broken output')
>             continue
> 
>         convos.append(response_text)
>         labels.append(score)
> 
>     return convos, labels
> 
> # Generate conversation responses in batches
> convos_df_lst = []
> labels_df_lst = []
> 
> for i in tqdm(range(0, num_convos, batch_size)):
>     # Randomly select a base prompt to encourage diverse responses
>     base_prompt = random.choice(base_prompts)
>     batch_prompts = [base_prompt] * batch_size
>     encoding = tokenizer(batch_prompts, return_tensors="pt", padding=True, truncation=True, max_length=max_length)
>     input_ids = encoding["input_ids"].to(DEVICE)
>     attention_mask = encoding["attention_mask"].to(DEVICE)
> 
>     outputs = model.generate(input_ids, attention_mask=attention_mask, max_length=max_length, pad_token_id=tokenizer.eos_token_id, do_sample=True, temperature=0.7)
>     convos_batch, labels_batch = extract_data(outputs, base_prompt)
> 
>     convos_df_lst.extend(convos_batch)
>     labels_df_lst.extend(labels_batch)
> 
> # Filter out duplicate responses
> unique_responses = list(set(zip(convos_df_lst, labels_df_lst)))
> convos_df_lst, labels_df_lst = zip(*unique_responses) if unique_responses else ([], [])
> 
> # Save to CSV
> df = pd.DataFrame({'convo': convos_df_lst, 'label': labels_df_lst})
> df['label'] = df['label'] >= 7
> display(df)
> output_path = "/mnt/batch/tasks/shared/LS_root/mounts/clusters/cn1/code/Users/CN/Output/dataset.csv"
> df.to_csv(output_path, index=False)
> 
> print(f"Dataset generated and saved to {output_path}")
> 
> ```
> 
> 
> 


---

> ## Waqar Ali
> 
> Congratulations on your upcoming presentation in Barcelona! I'm also thrilled to share that we won all the tracks in the OAG challenge. Despite your few submissions, your top-ranking performance in this competition is truly impressive. I have great admiration for your achievements. 🎁
> 
> 
> 


---

> ## WoNiu666
> 
> wow~~~great work
> 
> 
> 


---

> ## Yixiao Yuan
> 
> Thank you for sharing. I have a question about quantization in training and inference. If we use int4 for inference, is it better to use QLoRA instead of LoRA during training? This might align the training and inference conditions better, but I'm concerned QLoRA may not perform as well as LoRA. What are the trade-offs here?
> 
> 
> 


---

> ## sayoulala
> 
> Congratulations! Looking forward to your presentation in Barcelona. We also won all the tracks in another competition.（ OAG-challenge）.
> 
> Seeing that you submitted very few entries in this competition but still ranked among the top, I admire you greatly.
> 
> 
> 
> > ## Chris DeotteTopic Author
> > 
> > Thanks [@sayoulala](https://www.kaggle.com/sayoulala) Congratulations on your great performance here!
> > 
> > I joined this competition 1 week ago and I'm trying out insights that I learned from KDD Cup 2024. So far the ideas transfer well and are helping me do well here too!
> > 
> > 
> > 
> > > ## sayoulala
> > > 
> > > Thank you. I would like to ask if using vllm will result in a loss of accuracy?
> > > 
> > > 
> > > 
> > > ## sayoulala
> > > 
> > > By the way, my friend [@chizhu2018](https://www.kaggle.com/chizhu2018) is a huge fan of yours. Could I get your autograph for him if you're going to the KDD in Barcelona?
> > > 
> > > 
> > > 
> > ## yechenzhi1
> > 
> > may I ask if you are using models larger than 9B in the lmsys competition?
> > 
> > 
> > 
> > > ## sayoulala
> > > 
> > > Sorry, I won't disclose it before the competition ends.
> > > 
> > > 
> > > 
> > > ## yechenzhi1
> > > 
> > > That's totally okay! I'll try larger models by myself😁 
> > > 
> > > 
> > > 
> > > ## Ilia Zaitsev
> > > 
> > > So far, it looks like the bigger the model, the lower the loss is…
> > > 
> > > 
> > > 


---

> ## HinePo
> 
> Good to see you here, [@cdeotte](https://www.kaggle.com/cdeotte), I'm expecting to learn a lot from you again once the competition ends.
> 
> Do you know if vLLM can be used for Sequence Classification rather than Generation?
> 
> I've searched a bit but couldn't find anything.
> 
> 
> 
> > ## Chris DeotteTopic Author
> > 
> > I do not think we can use vLLM for Sequence Classification. So we need to use vLLM with my notebook or with the Llama3-8B starter notebook [here](https://www.kaggle.com/code/shelterw/sft-llama-3-8b-inference) which uses text generation.
> > 
> > 
> > 


---

> ## Valentin Werner
> 
> Why does this feel like a winning solution post to this challenge, just 2 weeks to early? Congratz on your KDD Cup performance, looking forward to see another of these being posted from you, tailored to this challenge 😉
> 
> EDIT: Also - now we have to train 34B models, I guess?
> 
> 
> 
> > ## yechenzhi1
> > 
> > 
> > now we have to train 34B models, I guess?
> > 
> > I think so😂 just not sure if the leading solutions are currently utilizing larger models.
> > 
> > 
> > 
> > > ## hn
> > > 
> > > I guess some are…my current LB score is actually based on small LMs so far.
> > > 
> > > 
> > > 


---

> ## Rishan Hasan Tenis
> 
> Congratulation, Thank You for sharing! [@cdeotte](https://www.kaggle.com/cdeotte) 
> 
> 
> 


---

> ## S J Moudry
> 
> Can AWQ be used with qlora?  From what I see SequenceClassification model types are not supported by AutoAWQ/PEFT yet.  Would you be performing full fine tuning and then converting to AWQ?
> 
> 
> 
> > ## Chris DeotteTopic Author
> > 
> > We QLoRA finetune with any type of 4bit quantization. After finetuning, we merge the LoRA adapter, and quantize with AWQ (to prepare for inference).
> > 
> > 
> > 


---

> ## dexterxin
> 
> Congratulation on your KDD Cup! 
> 
> It looks like that it's possible to finetune and infer 9B+ pretrained model on limited hardward within time constraint. It's a good news for participants without sufficient computing resources.
> 
> Thanks so much and looking forward to more of your ideas!
> 
> 
> 


---

> ## Ched Martin
> 
> Congratulations!
> 
> 
> 


---

> ## superferg
> 
> May I ask if you have tried gemma2 27B?
> 
> 
> 
> > ## Yichuan Gao
> > 
> > Sadly AutoAWQ does not support Gemma-2 yet, I also wanted to try gemma-2 27b :(
> > 
> > 
> > 


---

> ## yechenzhi1
> 
> Impressive! I thought  9b is the largest model we can use in this competition. 
> 
> 
> 
> > ## Chris DeotteTopic Author
> > 
> > No. It is good to know that we can at least infer 34B quickly on Kaggle's 2xT4 GPU. Therefore we can use 34B in all Kaggle competitions. It has also been shown [here](https://www.kaggle.com/competitions/kaggle-llm-science-exam/discussion/440620), that we can use 70B on Kaggle but the customization makes it slower than using vLLM and 34B. (And that notebook is too slow as is for Kaggle's LMSYS comp).
> > 
> > 
> > 


---

> ## Harshit Sharma
> 
> Congratulations [@cdeotte](https://www.kaggle.com/cdeotte) on the impressive win and for sharing these invaluable insights! Your innovative approach and efficient use of resources are truly inspiring. Can't wait to see your presentation on KDD Cup solution in Barcelona! 🌟🚀
> 
> 
> 


---

