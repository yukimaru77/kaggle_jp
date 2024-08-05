* --- discussion numver 0, the number of votes :151 ---

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



* --- discussion numver 1, the number of votes :96 ---

# External data - additional 157k human preference ratings 🔥🔥🔥

**Darek Kłeczek** *Fri May 03 2024 07:09:30 GMT+0900 (日本標準時)* (96 votes)

I'm super excited to see if smaller models (Kaggle GPU compatible) can effectively rate responses from much larger LLMs. To help you improve your models, I published a dataset with external data:

[https://www.kaggle.com/datasets/thedrcat/llm-human-preference-data-ultrafeedback/data](https://www.kaggle.com/datasets/thedrcat/llm-human-preference-data-ultrafeedback/data)

This is based on Ultrafeedback dataset published on HF by Argilla. I additionally converted it into the competition train data format. 

EDIT: Note that Ultrafeedback uses GPT4 as a judge as a proxy for human raters. I also added ties between models in version 2 that were previously filtered out. See original dataset paper [here](https://arxiv.org/pdf/2310.01377). Thanks [@nbroad](https://www.kaggle.com/nbroad) for catching this. 

Enjoy ❤️🙏👍



---

 # Comments from other users

> ## Dlond Mike
> 
> no use…but just for my notebook
> 
> 
> 


---

> ## Rich Olson
> 
> I added 50k of the items from this to my "Deberta + TF-IDF + Word2Vec + Length" notebook (it's public - I'd post a link - but Kaggle thinks I'm spamming).
> 
> got an identical 1.011 on the LB.  Had same experience with [this dataset](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/500973).
> 
> I take this as indication the data is probably good (or at least not bad) - it's just my notebook isn't able to benefit from the extra data.
> 
> 
> 


---

> ## Nicholas Broad
> 
> How do you think the tie should be handled? If the scores are equal, it should be a tie? (Your dataset only has "model a" winning)
> 
> Update:
> 
> I read more into how they processed the dataset and I noticed a few things:
> 
> I don't think this is human preferences. I think this is using [GPT-4 to rate the responses](https://github.com/OpenBMB/UltraFeedback/tree/main?tab=readme-ov-file#introduction)
> [Ultrafeedback intentionally filters out ties](https://huggingface.co/datasets/argilla/ultrafeedback-binarized-preferences/blob/main/README.md#dataset-processing), whereas the LMSYS dataset has roughly even split between model a winning, b winning, and ties.  
> 
> 
> > ## Darek KłeczekTopic Author
> > 
> > Great catch, thanks! I'll update the thread. I think this can be still useful for pretraining or pseudolabeling. Also found the paper here: [https://arxiv.org/pdf/2310.01377](https://arxiv.org/pdf/2310.01377)
> > 
> > 
> > 
> > > ## Darek KłeczekTopic Author
> > > 
> > > I'll see if I can reproduce the binarization while keeping ties too. 
> > > 
> > > 
> > > 
> > > ## Darek KłeczekTopic Author
> > > 
> > > Version 2 of the [dataset](https://www.kaggle.com/datasets/thedrcat/llm-human-preference-data-ultrafeedback) has ties between models added now. 
> > > 
> > > 
> > > 
> > > ## Turbo
> > > 
> > > Intersting dataset.
> > > 
> > > Did you use this dataset and boost your score?
> > > 
> > > 
> > > 


---

> ## eli plutchok
> 
> Wouldn't you expect gpt-4 rankings to be very different than human rankings? 
> 
> 
> 
> > ## Darek KłeczekTopic Author
> > 
> > There's research pointing that GPT-4 correlates well with human ratings, for example [here](https://arxiv.org/pdf/2306.05685):
> > 
> > The agreement […] between GPT-4 and humans reaches 85%, which is even higher than the agreement among humans (81%). This means GPT-4’s judgments closely align with the majority of humans.
> > 
> > 
> > 
> > > ## eli plutchok
> > > 
> > > Wow. Have you tested GPT4 on the training examples to see how well it scores?
> > > 
> > > 
> > > 


---

> ## justin1357
> 
> Is any data from kaggle covered in this dataset?
> 
> 
> 


---



* --- discussion numver 2, the number of votes :75 ---

# Additional 21k Labelled Conversations 🚀

**Abdullah Meda** *Wed May 08 2024 01:17:13 GMT+0900 (日本標準時)* (75 votes)

This dataset was from the authors themselves at [https://huggingface.co/datasets/lmsys/chatbot_arena_conversations](https://huggingface.co/datasets/lmsys/chatbot_arena_conversations)

The format was quite different to the one being used here for the competition. I have processed it to be in a similar format. Here they are:

- Dataset: [kaggle.com/datasets/abdullahmeda/lmsys-additional-33k-labelled-conversations](https://www.kaggle.com/datasets/abdullahmeda/lmsys-additional-33k-labelled-conversations)

- Processing Script: [kaggle.com/code/abdullahmeda/33k-lmsys-chatbot-arena-conversations/](https://www.kaggle.com/code/abdullahmeda/33k-lmsys-chatbot-arena-conversations/)

An upvote on the [dataset](https://www.kaggle.com/datasets/abdullahmeda/lmsys-additional-33k-labelled-conversations) would be greatly appreciated. Thank you! 🙏

I'll check if there are any duplicates between the datasets if I do get the time tomorrow. Happy coding!

UPDATE: Using the prompts column as deduplication criteria brings the sample count to around 21k. The dataset and script have been updated.



---

 # Comments from other users

> ## eli plutchok
> 
> Hi [@abdullahmeda](https://www.kaggle.com/abdullahmeda) , I tested adding in this training data, and for some reason  it makes the submission score a lot worse.
> 
> 
> 


---

> ## eli plutchok
> 
> Hey, I just realized that a lot of the lines are already on the main dataset. Maybe you can make a new cleaned version of this removing all the duplicates. I'm not sure about the percentage.
> 
> 
> 
> > ## eli plutchok
> > 
> > I think about a third are duplicates from the main training set, but there are also many duplicates within the data set, and I think there are additional ones that are very similar but not exact duplicates.
> > 
> > 
> > 
> > > ## Abdullah MedaTopic Author
> > > 
> > > [@eliplutchok](https://www.kaggle.com/eliplutchok) You may be right when you say that. I have dropped all rows that have similar prompts for now. More columns can be used as a subset when dropping rows, but I have noticed that lesser rows were dropped when using multiple columns. Using just the prompts as deduplication criteria brings the number down to just 21k new samples. I have updated the script as well as the dataset to reflect this. I'll update the post in a bit
> > > 
> > > ```
> > > superset = pd.concat([external_data, train]).reset_index(drop=True)
> > > external_data_deduplicated = superset.drop_duplicates(subset=['prompt'], keep='last')
> > > external_data_deduplicated = external_data_deduplicated[external_data_deduplicated.index.isin(external_data.index)]
> > > 
> > > len(external_data_deduplicated)
> > > >>> 21187
> > > 
> > > ```
> > > 
> > > 
> > > 
> > > ## eli plutchok
> > > 
> > > Btw, I realized another thing. It seems that the lines that had "tie (both bad)" as the winner, you just left blank, but these should all be counted as ties, or else you are left with only 10% ties u unlike the main dataset which has 30% ties.
> > > 
> > > 
> > > 
> > > ## Abdullah MedaTopic Author
> > > 
> > > [@eliplutchok](https://www.kaggle.com/eliplutchok) Thank you for pointing this out. I have made the respective changes!
> > > 
> > > ```
> > > >>> external_data[['winner_model_a', 'winner_model_b', 'winner_tie']].sum(axis=1).all()
> > > True
> > > 
> > > ```
> > > 
> > > 
> > > 


---

> ## Rich Olson
> 
> I just submitted a version of my 1.011 LB notebook which adds the de-duped version to train:
> 
> [https://www.kaggle.com/code/richolson/deberta-tf-idf-word2vec-length](https://www.kaggle.com/code/richolson/deberta-tf-idf-word2vec-length)
> 
> I'll post what I find out.
> 
> 
> 
> > ## Rich Olson
> > 
> > I got an identical 1.011 on the LB (see version 6 of above notebook).
> > 
> > Same results with using 50k items from the "[ultrafeedback](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/499756)" dataset.
> > 
> > I take this as indication the data is probably good (or at least not bad) - it's just my notebook isn't able to benefit from the extra data.
> > 
> > 
> > 
> > ## Ivan Vybornov
> > 
> > A bulk of data comes from the models that are not present in the actual train set, I doubt this will complement tf-idf approach.
> > 
> > 
> > 


---

> ## xiaotingting
> 
> After adding this dataset, the results are significantly better. The use of additional datasets is indeed useful.
> 
> 
> 
> > ## Erik
> > 
> > Hi, both cv and lb at the same time improved?
> > 
> > 
> > 
> > > ## KeShuang Liu
> > > 
> > > Why did I perform better on cv but worse on lb after using the dataset?
> > > 
> > > 
> > > 


---

> ## eli plutchok
> 
> Have you tried it yet with a submission? I'm scared that taking any external data may unintentionally make my model's predictions on the test data worse.
> 
> 
> 
> > ## Sparsh Tewatia
> > 
> > Bro if you try please update the results here too
> > 
> > 
> > 
> > > ## eli plutchok
> > > 
> > > k, will let you know, I hope to try this tomorrow (for me - I'm in NY).
> > > 
> > > 
> > > 
> > > ## go
> > > 
> > > before add data cv is 1.01
> > > 
> > > after add data cv is 1.03…
> > > 
> > > but I haven't submit this version
> > > 
> > > 
> > > 


---



* --- discussion numver 3, the number of votes :45 ---

# The magic behind Gemma2

**Yixiao Yuan** *Thu Jul 25 2024 05:32:05 GMT+0900 (日本標準時)* (45 votes)

According to other benchmarks, llama3.1 8B should be better than Gemma2. But from our experiments and other discussions, in this competiton, gemma2 is better. We found a possible reason in Gemma2's tech report. Gemma2 is pretrained on LMSYS. 🤣



---

 # Comments from other users

> ## Cody_Null
> 
> LMSYS-Chat-1M?? Does that mean there is a dataset of 1M for LMSYS?
> 
> 
> 
> > ## Kishan Vavdara
> > 
> > Yes, but it only contains conversation. [Here](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/499800)  the earlier discussion. 
> > 
> > 
> > 
> > ## Robson
> > 
> > I found this paper: [https://arxiv.org/pdf/2309.11998](https://arxiv.org/pdf/2309.11998)
> > 
> > 
> > 


---

> ## Valentin Werner
> 
> They trained on it - so you don't have to. 
> 
> It is interesting that they only use prompts, not responses, so the use case is very different from ours. I do not see a large benefit from it, but maybe somebody else can explain to me why this could help?
> 
> At the end of the day, many prompts in the lmsys dataset are VERY bad.
> 
> 
> 
> > ## Sparsh Tewatia
> > 
> > It is good with diffrerentiating between a good and bad answers for these type of prompts but don't know when it should be a tie.
> > 
> > 
> > 


---

> ## yechenzhi1
> 
> Hi, can you share the link to Gemma2's tech report?
> 
> 
> 
> > ## Yixiao YuanTopic Author
> > 
> > [https://storage.googleapis.com/deepmind-media/gemma/gemma-2-report.pdf](https://storage.googleapis.com/deepmind-media/gemma/gemma-2-report.pdf)
> > 
> > 
> > 


---

> ## yuanzhe zhou
> 
> it seems that there are many similar open source dataset?
> 
> 
> 


---



* --- discussion numver 4, the number of votes :44 ---

# Suspicious Surge of Novice Accounts on the Leaderboard

**Sercan Yeşilöz** *Thu Aug 01 2024 07:46:45 GMT+0900 (日本標準時)* (44 votes)

I was at 45-50th place 2-3 days ago, and today I see that there are too many novice accounts on the top of the leaderboard. They merged up as a team and are getting similar scores on LB. When I check some of these accounts, I see that most were just signed up a few days ago. I don't want to blame anyone without concrete evidence but these movements in the LB seem suspicious given my previous experiences in the competitions.



---

 # Comments from other users

> ## Fangzhou Liu
> 
> But it doesn't seem to affect the top 100 positions in the charts.
> 
> 
> 
> > ## Victor Lu
> > 
> > Why are some people replying with the same comment? I saw this comment three times in this discussion. One has been deleted. 😂 
> > 
> > 
> > 
> > > ## Cody_Null
> > > 
> > > Some new accounts with strange behavior it seems 
> > > 
> > > 
> > > 


---

> ## RUOFEI_Maggie
> 
> That's great.
> 
> 
> 


---

> ## Huang Jing Stark
> 
> I feel you, there was one day I wake up and found my place dropped 100+😅. I was thinking that did any expert share another great solution, but instead I found a lot of accounts which seems to registerd just recently and got same scores suddently came before me. Now I realize that some dirty things must happen. And I am still struggling to fight for the leaderboard. I will not surrender to those boosters. 😡
> 
> 
> 
> > ## Rise_Hand
> > 
> > Huwawei ! Beat the boosters! Beat the cheaters !!!
> > 
> > It looks like I am a joker compared to the team who easily get a silver medal by sharing privately🤡
> > 
> > 
> > 


---

> ## CPMP
> 
> Finetuning decoder only models is a relatively new thing on Kaggle. It is not surprising to see newcomers doing well IMHO.
> 
> Each time there has been a paradigm shift in Kaggle competition, a new breed of top performers emerged. It happened with XGBoost, then LightGBM, then with CNNs, then with transformers, then with pretrained LLMs, and now with Lora and variants.
> 
> That being said I have no clue about the specifics of the people you target. If you have evidence of cheating then you should send a mail to compliance@kaggle.conm.
> 
> 
> 


---

> ## Victor Lu
> 
> Because some people are selling solutions to this competition on Xiaohongshu, there are cases where a mentor leads a team of a few people to participate in the competition and charges a fee. Especially in the days leading up to the competition team registration deadline, these types of posts appear more frequently. Each post has about a dozen or twenty people inquiring about the price. This issue has been discussed in previous posts: [https://www.kaggle.com/competitions/open-problems-multimodal/discussion/366313](https://www.kaggle.com/competitions/open-problems-multimodal/discussion/366313)
> 
> 
> 
> > ## Valentin Werner
> > 
> > That's insane. How was this adressed in previous competitions? 
> > 
> > I am a bit torn on this:
> > 
> > - If a person is selling their solution by simply adding 4 team members and carrying them to gold, I think that is fine for me?
> > 
> > - If a person is selling their solution away to other teams, that would obviously be against the rules.
> > 
> > I am wondering if the the second case is happening too. When looking at the top 100, several teams with novice or contributor as highest rank have a similar submission pattern and very similar scores.
> > 
> > 
> > 
> > > ## Enter your display name
> > > 
> > > In fact, some people selling solutions come from the same educational institution or know each other. However, to earn more money, they form multiple teams. Therefore, it is almost impossible for them not to communicate with each other.
> > > 
> > > 
> > > 


---

> ## SeshuRaju 🧘‍♂️
> 
> In my opinion, it's not good to make claims about new accounts without proof (not by LB positions). At the end of every competition, the leaderboard often changes, indicating that Kaggle staff have identified and removed multi-accounts or internal sharing teams.
> 
> 
> 


---

> ## Nicholas Broad
> 
> if you have concrete evidence, report it, otherwise, just wait for kaggle to deal with it. After the comp ends, kaggle will remove cheaters
> 
> 
> 
> > ## Greenland chipper shark
> > 
> > [@nbroad](https://www.kaggle.com/nbroad) It's hard to prove without proof, but it's easy for those active and newly created numbers to suspect 🤨, which is the sad story
> > 
> > 
> > 
> > ## Greenland chipper shark
> > 
> > [@nbroad](https://www.kaggle.com/nbroad) I'm checking it out now, nothing against anyone, just finding a flood of contributors and newbies pouring out like a river
> > 
> > 
> > 
> > ## Cody_Null
> > 
> > I have new found faith in Kaggles ability to handle these cheaters. In IMC 2024 they managed to clear 20 cheaters from the top 50. And many more from the rest of the leaderboard. I am confident the Kaggle staff will do everything they can to get it right!
> > 
> > 
> > 


---

> ## zsyyyy_y
> 
> But it doesn’t seem to affect the top 100 positions in the charts
> 
> 
> 
> > ## Cody_Null
> > 
> > lol is that right?
> > 
> > 
> > 


---

> ## Vincy
> 
> It look like a ….
> 
> 
> 


---

> ## Pmantony
> 
> Might be a sign of increased interest in machine learning 
> 
> 
> 


---



* --- discussion numver 5, the number of votes :42 ---

# ChatBot Arena Prompts Can Distinguish Models. The Bradley-Terry model. Elo Ratings on Kaggle.

**Marília Prata** *Fri May 03 2024 14:27:26 GMT+0900 (日本標準時)* (42 votes)

# ChatBot Arena

Super cool Notebook Chatbot Arena MLE Elo Rating

[Chatbot Arena: MLE Elo Rating (Bradley-Terry model) Calculation (Apr 22, 2024)](#https://colab.research.google.com/drive/1KdwokPjirkTmpO_P1WByFNFiqxWQquwH#scrollTo=B_PYA7oVyaHO)

"Maximum Likelihood Estimation for Elo Ratings (aka Bradley-Terry model). In the context of LLM evaluation, models can be assumed to be static. In this case, the authors could directly fit the ratings by maximum likelihood estimation method (aka Bradley-Terry model), which produce significantly stable ratings. Here they provided an implementation with logistic regression."

[https://colab.research.google.com/drive/1KdwokPjirkTmpO_P1WByFNFiqxWQquwH#scrollTo=PbTdhkLQp113](https://colab.research.google.com/drive/1KdwokPjirkTmpO_P1WByFNFiqxWQquwH#scrollTo=PbTdhkLQp113)

# Chatbot Arena: An Open Platform for Evaluating LLMs by Human Preference

Authors: Wei-Lin Chiang, Lianmin Zheng, Ying Sheng, Anastasios N. Angelopoulos, Tianle Li, Dacheng Li, Banghua Zhu, HaoZhang, Michael I. Jordan, Joseph E. Gonzalez, Ion Stoica.

"To assess the performance of LLMs, the research community has introduced a variety of benchmarks. These benchmarks can be categorized based on two factors: the source of questions (either static or live) and the evaluation metric (either ground truth or human preference). According to these fac tors, benchmarks can be classified into four categories. While a range of benchmarks is beneficial, the most prevalent current method for evaluating LLMs remains a static, ground-truth-based evaluation, partly because such evaluations are inexpensive and reproducible."

"However, these static, ground-truth-based benchmarks exhibit several limitations. Firstly, the questions within these benchmarks are not open-ended, hindering the ability to capture the flexible and interactive use found in real-world settings. Secondly, the test sets in these benchmarks are static, meaning they can become contaminated over time, which undermines the reliability of the evaluation results. Furthermore,for many complex tasks, establishing a definitive ground truth is not only challenging but sometimes unattainable."

" Consequently, current benchmarks fail to adequately address the needs of state-of-the-art LLMs, particularly in evaluating user preferences. Thus, there is an urgent necessity for an open, live evaluation platform based on human preference that can more accurately mirror real-world usage."

"Creating such a benchmark platform entails significant challenges. It requires the collection of live, fresh, and diverse user questions to accurately represent real-world scenarios."

CONTRIBUTIONS MADE by the AUTHORS:

"They built the first large-scale crowd-sourced live LLM evaluation platform with over 1M users visit."

"They conducted an in-depth analysis of the collected data, including prompt diversity, quality, vote quality, and insights on human feedback."

"They will publicly release a human preference dataset with over 100K pairwise votes collected from Chatbot Arena."

"They designed an efficient sampling algorithm that actively chooses which model pairs to show, such that our sample efficiency improves, sometimes to a large degree."

# Risks of Static Benchmarks.

"Static benchmarks have certain issues, including contamination, saturation, overfitting, and a lack of human alignment. DynaBench identifies these challenges and recommends the use of a live benchmark that incorporates a human-in-the-loop approach for classical NLP benchmarks. Their system adopts a similar spirit."

DATA STATISTICS 

"The authors began collecting data in April 2023. As of Jan 2024, they have received around 240K votes from over 90K users. Their data involves more than 50 models, including both proprietary models like GPT-4, Claude, and Gemini, as well as open models such as LLaMA and Mistral. These conversations cover more than 100 languages, with 77% being in English, 5% in Chinese, and the remaining languages, such as Russian, German, Spanish, French, and Japanese, each representing less than 2% of the total. Each data point includes multi-turn conversations between the user and two LLMs, and a vote to indicate which model the user prefers."

# Can Arena Prompts Distinguish Models?

"The authors studied how effective are these topic clusters in distinguishing models strengths. Their result shows models may exhibit varying strengths in different areas, but also highlights some of the topic clusters in Chatbot Arena are effective in differentiate models."

[https://arxiv.org/pdf/2403.04132](https://arxiv.org/pdf/2403.04132)

# Elo Ratings

Remember that it is "Elo", not "ELO" since it was named after Arpad Elo. The USCF implemented Arpad Elo's suggestions in 1960, and the system quickly gained recognition as being both fairer and more accurate than the Harkness rating system.

[Elo rating system](https://en.wikipedia.org/wiki/Elo_rating_system)

"The Elo rating system is a method for calculating the relative skill levels of players, which has been widely adopted in chess and other competitive games. The difference in the ratings between two players serves as a predictor of the outcome of a match. The Elo rating system works well for our case because we have multiple models and we run pairwise battles between them. In this section, we present different methods for calculating Elo ratings."

Compute Ratings

"The authors first use the online linear update algorithm to compute Elo ratings. They chose a small K-factor of 4 to make the Elo ratings more stable and less biased towards recent games."

[https://colab.research.google.com/drive/1KdwokPjirkTmpO_P1WByFNFiqxWQquwH#scrollTo=B_PYA7oVyaHO](https://colab.research.google.com/drive/1KdwokPjirkTmpO_P1WByFNFiqxWQquwH#scrollTo=B_PYA7oVyaHO)

# Elo Ratings on Kaggle

KAGGLE TOPICS:

[Intro to Rating Systems](https://www.kaggle.com/competitions/chess/discussion/92) By Jeff Sonas - 14 y ago

[Elo Ratings Shiny App for Euro Soccer Teams](https://www.kaggle.com/datasets/hugomathien/soccer/discussion/31154) By Kevin Pan - 8 y ago

[Elo RATING ALGORITHM](https://www.kaggle.com/discussions/getting-started/216048) By Kaushik Deb

KAGGLE NOTEBOOKS:

[Elo Ratings in Python](https://www.kaggle.com/code/kplauritzen/elo-ratings-in-python) By Kasper P. Lauritzen

[Simple Simulation & Elo Rating Approach](https://www.kaggle.com/code/kenjee/simple-simulation-elo-rating-approach) By Ken Jee

[Custom Football Elo Rating](https://www.kaggle.com/code/thomasstokes/custom-football-elo-rating) By Thomas Stokes

There are many more on Kaggle. I've just picked a few to exemplify. Therefore, search by Code or Discussion if you intend to read more material.





* --- discussion numver 6, the number of votes :40 ---

# LMSYS Dataset Explorer – Cluster, segment, inspect

**Emmanuel Turlay** *Thu May 30 2024 02:56:10 GMT+0900 (日本標準時)* (40 votes)

Hey folks – Today, we’re releasing a free dataset explorer for the LMSYS challenge.

With our tool, you can browse through individual rows and inspect their content in great detail. We generated semantic clusters, and you can filter conversations by cluster, model pairs, winner model, and so on.

The tool is free and no login is required. Be sure to let the community know what you discover.

Click this link to start exploring: [https://app.airtrain.ai/dataset/bb589c26-8f45-4f42-8ba3-07ef51b73a03/null/1/0](https://app.airtrain.ai/dataset/bb589c26-8f45-4f42-8ba3-07ef51b73a03/null/1/0)



---

 # Comments from other users

> ## Lisa DunlapCompetition Host
> 
> OMG THIS IS SO COOL!!!
> 
> 
> 


---

> ## Cviko Dukanovic
> 
> Amazing product. The meta clusters and clusters are greatly produced!
> 
> 
> 


---

> ## Josh Bauer
> 
> One fun cluster I've found: plenty of variations on the "how much wood could a woodchuck chuck if a woodchuck could chuck wood" tongue twister. Ex: "If, IF, a woodchuck could chuck wood, how much wood could a woodchuck chuck before it lost its job as a project manager?" 😆
> 
> Under "Riddles and Reasoning" > "Woodchuck Tongue Twister", row 4308
> 
> 
> 
> > ## Idriss Chebak
> > 
> > one cool prompt i found was "Construct a rap battle, in the style of Epic Rap Battles of History, with rhyme and meter and personal attacks relevant to each character, between Pikachu and Zeus. Each participant gets 2 verses. There is no announcer and Zeus goes first." 😄
> > 
> > 
> > 


---

> ## Felipe Maia Polo
> 
> Thanks for the amazing work! Is there a way to download the cluster assignments? Thanks!
> 
> 
> 
> > ## Josh Bauer
> > 
> > Glad you like it! You can't export the clusters right now, but it's on our TODO list.
> > 
> > 
> > 
> > ## Emmanuel TurlayTopic Author
> > 
> > We just shipped an update that includes clusters and token counts in the exported file. Have fun!
> > 
> > 
> > 
> > > ## Felipe Maia Polo
> > > 
> > > thank you!
> > > 
> > > 
> > > 


---

> ## Valentin Werner
> 
> The tool looks amazing!
> 
> As you are the the CEO of the company behind the tool, did you check the licenses? I am not sure if you are allowed to publish data from the competition on your platform, given the cc-by-nc license. I know that there was the recommendation not to do such in previous conpetitions.
> 
> Maybe you can instead show us how to use your tool to create such a dashboard instead?
> 
> All the best for your company and product!
> 
> (Also quite the PR stunt to have your employees comment on your thread (Josh & Idriss) 😉)
> 
> 
> 
> > ## Emmanuel TurlayTopic Author
> > 
> > Hi Valentin, thanks for the compliment!
> > 
> > We did check the [license](https://creativecommons.org/licenses/by-nc/4.0/) and it says we are allowed to share, copy, and redistribute the material in any medium or format; adapt, remix, transform, and build upon the material; as long as we attribute credit and offer it under non-commercial terms.
> > 
> > The Dataset Explorer is free and requires no sign-up. The Kaggle page is linked to from the description for attribution.
> > 
> > We certainly want to remain compliant and are offering this work to support the community. Thanks for making us double-check the license 😉
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > Great stuff!
> > > 
> > > 
> > > 


---

> ## YingxiZhang
> 
> The tool is amazing!👍
> 
> 
> 


---



* --- discussion numver 7, the number of votes :39 ---

# [Insights] on 165k Dataset and Model Performance

**justin1357** *Thu Aug 01 2024 20:21:38 GMT+0900 (日本標準時)* (39 votes)

In the past two days, I attempted to integrate the 165k dataset proposed in the discussion area three months ago into the training pipeline. However, this attempt failed on the leaderboard. Therefore, I carefully reviewed the information of this dataset.

Deduplication: I performed deduplication on the 165k dataset and the 55k Kaggle dataset at the prompt and response level. There was no significant duplication found, indicating that the performance decline was not due to overfitting on duplicate data.

Data Source Analysis: After ruling out technical issues, I examined the source of the data. Many people know that this dataset comes from UltraFeedback. However, what most people do not know is that the prompts are not human-generated but sourced from various evaluation datasets such as UltraChat, ShareGPT, Evol-Instruct, TruthfulQA, FalseQA, and FLAN. I believe this is the main reason for the performance drop—the distribution of human prompts from Chatbot Arena differs significantly from the prompts in professional evaluation datasets, which misleads the model.

Model Performance Explanation: This also explains why LLama-3.1, despite performing exceptionally well on various evaluation datasets, did not perform well in this competition. LLama-3.1 uses DPO (Direct Preference Optimization), which essentially "overfits" the professional evaluation prompts. However, these differ from the prompt distribution collected by ChatBot Arena, leading to different standards for evaluating responses.

Successful Models Analysis: This also explains why models like Gemma-2 and LLama-3 performed well in this competition. They share a common feature in the post-training phase: using RLHF (Reinforcement Learning from Human Feedback). Although this method is more costly compared to automatic learning methods like DPO, it aligns more closely with the real human prompt distribution, allowing the model to better understand real human prompts.

Testing Results: I also tested several Gemma-2 models fine-tuned with DPO or SimPO on the UltraFeedback dataset, and their performance was unsatisfactory. This indirectly reflects the issues with DPO-like methods.

I hope these insights are helpful to you. If you found this response useful, I would greatly appreciate your vote.



---

 # Comments from other users

> ## xiaotingting
> 
> Yes, I feel that the processing of data in this competition may be an important point for the increase in the later stage.
> 
> 
> 


---



* --- discussion numver 8, the number of votes :34 ---

# Ranking of models estimated from train data.

**takaito** *Fri May 03 2024 16:08:51 GMT+0900 (日本標準時)* (34 votes)

I overlooked the fact that there is no model name in the test data.

I have estimated which model to choose from train data.

Since I have estimated for all model pair combinations, I'll share it. [notebook](https://www.kaggle.com/code/takaito/lmsys-model-name-catboostclassifier/notebook)

gpt4 tends to be selected more often.

If the model can be predicted 100% from the output, it is possible to score around 1.04 based on the name of the model alone. (This is an expectation based on the CV score at the time of the training.)

['gpt-4-1106-preview', 'gpt-4-0314', 'gpt-4-0125-preview', 'claude-1', 'gpt-4-0613', 'gpt-3.5-turbo-0314', 'claude-instant-1', 'gpt-3.5-turbo-0613', 'claude-2.0', 'claude-2.1', 'mistral-medium', 'vicuna-33b', 'llama-2-70b-chat', 'mixtral-8x7b-instruct-v0.1', 'wizardlm-70b', 'vicuna-13b', 'yi-34b-chat', 'qwen1.5-72b-chat', 'wizardlm-13b', 'starling-lm-7b-alpha', 'guanaco-33b', 'mpt-30b-chat', 'llama-2-13b-chat', 'gemini-pro-dev-api', 'koala-13b', 'gpt-3.5-turbo-1106', 'gemini-pro', 'zephyr-7b-beta', 'tulu-2-dpo-70b', 'gpt-3.5-turbo-0125', 'palm-2', 'pplx-70b-online', 'vicuna-7b', 'openchat-3.5', 'llama-2-7b-chat', 'openhermes-2.5-mistral-7b', 'nous-hermes-2-mixtral-8x7b-dpo', 'solar-10.7b-instruct-v1.0', 'zephyr-7b-alpha', 'codellama-34b-instruct', 'llama2-70b-steerlm-chat', 'dolphin-2.2.1-mistral-7b', 'openchat-3.5-0106', 'falcon-180b-chat', 'mistral-7b-instruct-v0.2', 'qwen1.5-7b-chat', 'deepseek-llm-67b-chat', 'gpt4all-13b-snoozy', 'pplx-7b-online', 'stripedhyena-nous-7b', 'mpt-7b-chat', 'mistral-7b-instruct', 'qwen-14b-chat', 'alpaca-13b', 'RWKV-4-Raven-14B', 'qwen1.5-4b-chat', 'oasst-pythia-12b', 'chatglm-6b', 'fastchat-t5-3b', 'stablelm-tuned-alpha-7b', 'chatglm3-6b', 'llama-13b', 'dolly-v2-12b', 'chatglm2-6b']

I hope this will be of some help!!



---

 # Comments from other users

> ## Fritz Cremer
> 
> This is interesting, since some models like Gemini, annoyingly often starts answers with "Absolutely! …" or "You're right! …". This should make predicting the model quite easy.
> 
> 
> 
> > ## takaitoTopic Author
> > 
> > Thanks for your comment.
> > 
> > As you commented, each model has its own output characteristics.
> > 
> > I think it is possible to predict rough models.
> > 
> > The predicted model name could be used for the features.
> > 
> > 
> > 
> > > ## JunHua Liao
> > > 
> > > Good idea. But I don't know if there is a significant difference between the distribution of model types in the training set and the test set, as there is no model type given for the test dataset.
> > > 
> > > 
> > > 


---

> ## Kishan Vavdara
> 
> 
> 
> Yes! gpt4 wins more often! 
> 
> 
> 


---

> ## Heroseo
> 
> oh, it is really instresting. 
> 
> It's a different story, but it would be more fun if there was llama-3 as well.
> 
> 
> 
> > ## Lisa DunlapCompetition Host
> > 
> > Agreed! The task of just predicting the model itself if quite interesting , perhaps there could be another competition about this in the future…
> > 
> > 
> > 
> > > ## Lisa DunlapCompetition Host
> > > 
> > > Especially if you can describe in language what are the defining characteristics of the model
> > > 
> > > 
> > > 


---

> ## tanaka
> 
> Yeah, this kind of analytics is already done in lmsys.org itself and calculated to elo ranking. You can see current lmsys's ranking in lmsys leaderboard.
> 
> old elo ranking (2023-12-7?)
> 
> current elo ranking (2024-5-27)
> 
> Refs:
> 
> - [https://lmsys.org/blog/2023-12-07-leaderboard/](https://lmsys.org/blog/2023-12-07-leaderboard/)
> 
> 
> 


---

> ## Easter Bunny
> 
> Worth delving into this
> 
> 
> 


---



* --- discussion numver 9, the number of votes :33 ---

# Prediction Using Generation Header

**Takamichi Toda** *Tue Jul 16 2024 16:07:36 GMT+0900 (日本標準時)* (33 votes)

This is still a tried and tested idea and has not yet been successful in my current environment, but I would like to share it.

Currently, from what I can see in public code, the mainstream approach seems to be to base it on Llama or other LLMs and use LoRA to train a classification head. However, LLMs are originally trained to predict the next token, so I think this method is inefficient as it diverges from the original training of the LLM.

My idea is to use the same generative header (CausalLM) as the original LLM.

I adjust the prompts and use the generation probabilities of the tokens A, B and tie.　The predictions are post-processed using softmax so that they sum to one.

Below is a simple sample code:

```
text = """
### Instruction
Which model's answer is appropriate for the prompt?　If both are appropriate, answer `tie`.

### Prompt
{prompt text}

### A
{response A}

### B
{response B}

### Answer
"""

inputs = tokenizer(text)
out = model(inputs)
pred_token_id = tokenizer.encode("A") + tokenizer.encode("B") + tokenizer.encode("tie")
pred = out.logits[0, -1, pred_token_id].softmax(0)

```

Here is the code that evaluates this method using Llama3 8B.

[https://www.kaggle.com/code/takamichitoda/lmsys-zeroshot-prediction](https://www.kaggle.com/code/takamichitoda/lmsys-zeroshot-prediction)

Llama3 has not undergone any special fine-tuning and is used as loaded from the Kaggle model. The evaluation data uses 1/5 of the competition data, which is equivalent to my current validation strategy (correlates well with the public leaderboard).

As a result, we obtained a score of 1.234. It was surprising to me that I could achieve such a result with ZeroShot.

Currently, I am performing SFT on the competition data and adjusting the prompts. However, models that learn classification headers still score better.

Are there others working on a similar approach?



---

 # Comments from other users

> ## James Day
> 
> I tried a similar experiment, primarily because I was hoping to take advantage of training and inference libraries for causal language models that are faster and more memory efficient than the HuggingFace transformers library, namely unsloth and vLLM. However, I actually finetuned the LLMs, as opposed to just doing zero shot inference like [@takamichitoda](https://www.kaggle.com/takamichitoda)'s initial experiment.
> 
> I got 0.902 (CV) with Llama 3 8B Instruct doing next token prediction, which is almost as good as I've been getting with "normal" Llama 3 based classification models. However, the same approach did not work well with Gemma 2 9B (0.990 CV 🤮), possibly due to Gemma's tied embeddings. My CV scores are pretty consistently ~0.03 lower than the corresponding LB scores, so those results translate to ~0.93 & 1.02 LB, which isn't good enough for me to bother submitting.
> 
> 
> 
> > ## Takamichi TodaTopic Author
> > 
> > Thank you for sharing
> > 
> > 0.9 is a great score for me ;)
> > 
> > By the way, I would like to know if possible, what kind of prompt did you use to perform finetuning?
> > 
> > I am using trl's SFTTrainer and learning only output with DataCollatorForCompletionOnlyLM.
> > 
> > 
> > 
> > > ## James Day
> > > 
> > > I used prompts like:
> > > 
> > > ```
> > > Which one of the chatbots below did a better job responding to the user request? Or were they tied?
> > > 
> > > ~~~~~~~~~~ CONVERSATION WITH BOT A ~~~~~~~~~~
> > > 
> > > ### User: "{initial prompt}"
> > > 
> > > ### Bot A Response: "{initial response}"
> > > 
> > > ### User: "{maybe a follow up prompt if available - I included as many conversation turns as will fit in a 3k token context window, discarding the first part of each conversation if necessary}"
> > > 
> > > ### Bot A Response: "{follow up response}"
> > > 
> > > ~~~~~~~~~~ CONVERSATION WITH BOT B ~~~~~~~~~~
> > > 
> > > ### User: "{...}"
> > > 
> > > ### Bot B Response: "{...}"
> > > 
> > > ### User: "{...}"
> > > 
> > > ### Bot B Response: "{...}"
> > > 
> > > ### BEST RESPONSE:
> > > 
> > > ```
> > > 
> > > It was then trained to output " A", " B", or " Tie". The spaces were part of the response tokens.
> > > 
> > > 
> > > 
> > ## Valentin Werner
> > 
> > Do you have the CV discrepancy only for this experiment or for all your models? We did several experiments where it is way below 0.01 in difference, and some where its similar to yours
> > 
> > 
> > 
> > > ## James Day
> > > 
> > > All experiments.
> > > 
> > > Also, I was oversimplifying for the sake of being able to do the math in my head. A more precise estimate of what 0.902 CV translates to on the leaderboard would be 0.902*0.890 + 0.125 = 0.928. The CV-LB correlation data that is based on is included below.
> > > 
> > > 
> > > 
> > > ## ShelterW
> > > 
> > > I think it is your extra prompts that cause the relatively big difference between CV and LB.
> > > 
> > > By the way, do you use qlora or lora to finetune llm？
> > > 
> > > 
> > > 
> > > ## James Day
> > > 
> > > I use qlora.
> > > 
> > > As for the difference between my CV & LB scores, I doubt it has anything to do with the use of external training datasets not provided by the competition organizers (which I assume is what you meant by "extra prompts"), primarily because I did not observe any significant deviations from the preexisting trendline when adding extra data. I think a more likely explanation is that the data provided by the competition organizers isn't perfectly representative of their test data. For example, they may have partitioned their data based on the date on which each conversation occurred, thereby causing the test data to contain responses from new models that aren't present in the training data (or my cross validation data for that matter).
> > > 
> > > Also, one consequence of the trendline having a slope < 1 is that the discrepancies tend to get bigger as CV & LB scores improve. Extrapolating to a ridiculous extent, a model with perfect accuracy in cross validation (CV 0) would likely score ~0.125 on the leaderboard, which is a huge score discrepancy.
> > > 
> > > 
> > > 


---

> ## AbaoJiang
> 
> Hi [@takamichitoda](https://www.kaggle.com/takamichitoda),
> 
> As you mentioned, the performance of Zeroshot prediction is 1.234, which doesn't surpass the score of 1.098 by predicting the global mean.
> 
> However, it's still an interesting idea to try. Thanks for your sharing!
> 
> 
> 
> > ## Valentin Werner
> > 
> > I think the issue is in the softmax assumption without training the models first. The model has basically no intent to predict "A", "B" or "tie" whatsoever, if it not finetuned to realize it should do so. Therefore, the logits are also pretty much nonesense. 
> > 
> > This simple baseline experiment they did does not speak at all for whether their actual experiment will work or how well it will perform.
> > 
> > To me, at first glance I do not see any benefit over the seq class approach directly, as you still probably need to disable the autoregressive generation etc. But it definetly is an interesting idea
> > 
> > 
> > 
> > ## Takamichi TodaTopic Author
> > 
> > I was able to improve the score to 1.037 with SFT and Prompt Tuning. Although the classification header is still better, I intend to continue verification.
> > 
> > 
> > 
> > > ## ShelterW
> > > 
> > > I used SFT to finetune the llama3-8b and improved the LB score to 0.935 [here](https://www.kaggle.com/code/shelterw/training-llama3-8b-4-bit-qlora-sft), welcome to refer to and make suggestions.
> > > 
> > > 
> > > 


---



* --- discussion numver 10, the number of votes :32 ---

# Danube3 (0.5 B & 4B) just dropped!

**Valentin Werner** *Mon Jul 15 2024 15:57:26 GMT+0900 (日本標準時)* (32 votes)

I have used Danube2 for several experiments and even with QLoRA on Kaggle GPU it seems to be a way better alternative to DeBERTa Large. 

Danube3 just came out as 0.5B and 4B and also comes with a Chat model, which might be an upside for this competition. The 4B model outperforms its 1.5B predecessor on all benchmarks by a lot (also a bit of a size difference), while the 0.5B outperforms Qwen2 0.5B on most benchmarks. However, to me it will be particularly interesting, how the 4B model compares to Phi3-Mini, as this is the only other model I know in its weight class. Maybe this is team Danube's secret? 😉

From my experience smaller models, like 0.5B will still not fit on Kaggle GPUs (it should work on a 4090), so I will focus on the 4B model.

I also want to applaud the H2O Team, which is quite active on Kaggle, on this new release! It is always amazing, when talented researchers and Data Scientists contribute towards the Open LLM efforts (also the sheer speed of new releases). Looking forward to see how good this model is!

Links: 

Model card: [https://huggingface.co/h2oai/h2o-danube3-4b-chat](https://huggingface.co/h2oai/h2o-danube3-4b-chat)

Technical Report: [https://arxiv.org/abs/2407.09276](https://arxiv.org/abs/2407.09276)

Benchmarks:

Some benchmarks I aggrated from the [old open LLM leaderboard](https://huggingface.co/spaces/open-llm-leaderboard-old/open_llm_leaderboard). Danube3 is not included in the leaderboard yet, but reports these values on their model card. I think it is very interesting to see how close Danube3 comes to Gemma-7B and Mistral-7B.

| Category | Benchmark | Danube3-4b-Chat | Danube2-1.8B-Chat | Phi-3-Mini-4K-Ins | Gemma-7B | Mistral-7B Ins 0.2 |
| --- | --- | --- | --- | --- | --- | --- |
| Popular aggregated | MMLU  (5-shot) | 54.74 | 37.77 | 69.08 | 64.56 | 60.78 |
| Language Understanding | HellaSwag (5-shot) | 80.36 | 73.54 | 80.60 | 82.20 | 84.88 |
| Reasoning | ARC Challenge (5-shot) | 58.96 | 43.43 | 62.97 | 61.09 | 63.14 |
|  | TruthfulQA (0-shot) | 47.79 | 39.96 | 59.88 | 44.79 | 68.26 |
|  | WinoGrande (5-shot) | 76.48 | 69.77 | 71.6 | 79.01 | 77.19 |
| Math | GSM8K CoT   (5-shot) | 50.18 | 26.16 | 85.7 | 50.87 | 40.03 |
| Average |  | 61.42 | 48.44 | 69.91 | 63.75 | 63.14 |

Models were chosen based on the models microsoft phi3-mini is reporting against on their model card.



---

 # Comments from other users

> ## chaneyMA
> 
> nice work!!!!
> 
> 
> 


---

> ## madarshbb
> 
> Just for curiosity,
> 
> From my experience smaller models, like 0.5B will still not fit on Kaggle GPUs (it should work on a 4090), so I will focus on the 4B model.
> 
> What do you mean by this? Shouldn't 0.5B model be easier to fit than 4B?
> 
> 
> 
> > ## Valentin WernerTopic Author
> > 
> > I mean 0.5 is just big enough so you can't train it on Kaggle without quantization. This is basically similar size as DeBERTa Large
> > 
> > 
> > 


---

> ## Abhay Ayare
> 
> Fantastic guide! Thank you for sharing these valuable resources and insights on becoming a data scientist. Your passion for data science is inspiring. Looking forward to exploring your book "Kaggle for Beginners."
> 
> 
> 
> > ## Valentin WernerTopic Author
> > 
> > There are plenty of kaggle books, but I certainly have not written one of them 😉
> > 
> > 
> > 


---

> ## sayoulala
> 
> Thanks for you share, May I ask that the scores of this competition by the model ?
> 
> 
> 
> > ## Valentin WernerTopic Author
> > 
> > I have no trained it yet. Some experiments (did not try super hard) got danube2-1.8B to .98x for me
> > 
> > 
> > 


---

> ## The-Hai Nguyen
> 
> You are always shedding light on my learning progress all the way back from the PII-detection competition. Really appreciate and thanks for your sharing, it helps me and the others learn a lot throughout the journey 🙏.
> 
> 
> 


---



* --- discussion numver 11, the number of votes :32 ---

# Data Annotation Intuition - why the labels are noisy

**Valentin Werner** *Mon May 13 2024 23:10:26 GMT+0900 (日本標準時)* (32 votes)

I see that there are several ongoing discussions regarding label quality. As someone, who has spent a significant amount of time annotating data (and asking other people to annotate data for me), I want to share an opinion and intution of mine too.

In Data Annotation, you generally want professionals to annotate the data. They are supposed to (but sometimes do not do so) read the data carefully, select the labels carefully etc.; the annotated data is considered the GROUND TRUTH as these experts should be able to objectively decide the correct label (given same understand of the problem and annotation task). 

Then you generally compute an Inter-Annotator Agreement (are n people giving the same label on the same text), which was often seen as a ceiling for performance. Although this is not always the case in reality, this makes sense, because that means that your model is able to learn the intersection of knowledge from multiple annotators. 

Why is this important? The data we are training on is annotated by random people who wanted to try LLMs. While LMSYS is a great tool that I often use and recommend, it is for our problem mostly an annotation tool where the annotator can decide what question they want to annotate for and the data to annotate is generated in real time. 

However, there are several issues with this for our challenge:

- Users are not experts in using or understanding LLMs

- Users are often not experts in the topic they are asking about (and are often not fact-checking the responses)

- Unless users specify the same prompt and receive the same response, there is no way to evaluate Inter-Annotator Agreement

- LMSYS does not allow to undo or redo annotations (e.g., misclicked the wrong side)

- And most importantly: users have different preferences. This annotation task is not objective at all but PURELY subjective

This means we have NOISY labels and should employ techniques to deal with this; there are techniques such as active learning, ensembling, changing loss etc. which might work to address this issue - all of this needs to be tested (although ensembling is something we will do anyways 😉).



---

 # Comments from other users

> ## aotiandragon
> 
> Thanks a lot, It helped me to know the datas
> 
> 
> 


---

> ## Pranav Belhekar
> 
> Thanks for sharing your point. It helped me to analyze the competition.
> 
> 
> 


---

> ## Fae Gaze
> 
> Excellent insights on label noise! You might also explore robust loss functions like focal loss to mitigate noise impact, and consider frameworks like Snorkel to efficiently manage training data through programmable labeling functions
> 
> 
> 
> > ## Valentin WernerTopic Author
> > 
> > Have not heard of Snorkel yet - can you recommend some literature? 
> > 
> > 
> > 


---

> ## Takamichi Toda
> 
> Thank you for sharing. And I was thinking the same thing just now.
> 
> There are some samples in the training data consisting only of very short prompts (one word). A typical example is when the prompt is just "hey". The responses of LLMs to this can generally be divided into two patterns:
> 
> Simply respond with "Hello!".
> After saying "Hello", provide a cue to continue the conversation, such as "How can I assist you today?".
> 
> I think 2 seems to be better, but the training data shows that there were a reasonable number of tie and cases where 1 was winning.
> 
> |  | n_sample | id |
> | --- | --- | --- |
> | hello_lose | 5 | 189242591, 211357242, 326037335, 458677274, 3947327386 |
> | tie | 4 | 1329170872, 3422926530, 4197301939, 4265282380 |
> | hello_win | 2 | 1655058446, 2171261721 |
> 
> The "hay" pattern trend seems to be more to my liking (2 mostly), but there are many other patterns like this that need to be treated as a NOISY label, as you say.
> 
> 
> 
> > ## Valentin WernerTopic Author
> > 
> > And I think is one on the more obvious side, where people just voted a side eventhough both models give the same answer. These people were obviously not thinking of poor ML Developers that need to explain why they did it 😉
> > 
> > I think evaluating how truthful the responses are (if there is a good way to do it) could also be a good feature for training our models
> > 
> > 
> > 


---

> ## Lisa DunlapCompetition Host
> 
> I think this is an amazing point: one of the big challenges with this challenge (no pun intended) - the data is crowdsourced with very minimal filtering so learning how to deal with label noise is incredibly important!
> 
> 
> 


---

> ## JunHua Liao
> 
> I have also discovered the issue of labels noise, mainly due to the same prompt and reponses, where there is a winner, which should be winner_tie. The two solutions currently in mind are: (1). Change the label to winner_tie; (2) Delete noise data
> 
> 
> 
> > ## Lisa DunlapCompetition Host
> > 
> > It may also be beneficial to look in to prompt deduplication or down weighting overrepresented prompts
> > 
> > 
> > 


---

> ## xiaotingting
> 
> At present, cleaning data and selecting models have the greatest impact on the results. I feel that no matter what field you are in, even if you use a large model, the quality of the data is very important.
> 
> 
> 
> > ## Valentin WernerTopic Author
> > 
> > Looking forward to see how you cleaned data, we tried it a bit but were not able to get it to a point where it actually helped
> > 
> > 
> > 
> > > ## Fae Gaze
> > > 
> > > Hi, that is right. Too much cleaning will affect on the score adversely
> > > 
> > > 
> > > 


---

> ## AbChk
> 
> Thanks for sharing your point. It seems like this issue makes us wonder if the test data also has noisy labels?
> 
> 
> 
> > ## Valentin WernerTopic Author
> > 
> > very likely so. I (maybe not so) boldly assume that they did not manually check 25k samples for quality. It is like chosen based on label distribution and models.
> > 
> > 
> > 
> > ## Fae Gaze
> > 
> > the test is also noisy. But, we are not able to clean the noise. Even cleaning the training will affect the score
> > 
> > 
> > 


---



* --- discussion numver 12, the number of votes :31 ---

# Solution file to be updated the week of May 28th

**Sohier Dane** *Tue May 21 2024 01:30:43 GMT+0900 (日本標準時)* (31 votes)

A Kaggle community member informed us that the hidden test set for this competition contains values that have already been published. We were aware of some existing public data, but not that there are actually different versions of the public data using one name. We will update the solution file to ignore the affected rows next week and then rescore all existing submissions. You are welcome to continue to make submissions in the meantime.

Thank you very much to the Kaggler that disclosed this issue.

To everyone else, apologies for the disruption and thank you in advance for your patience. 



---

 # Comments from other users

> ## Psi
> 
> Given the top score, high probability there is another leak…
> 
> 
> 
> > ## Chris Deotte
> > 
> > If it is a leak, this is frustrating. Many teams spent a lot of money and time on compute. 
> > 
> > If it is a leak in the form of released test data, doesn't the host know where they published their test data? Couldn't this have been discovered day one?
> > 
> > 
> > 
> > > ## Psi
> > > 
> > > as you can see in this thread, it already happened once…
> > > 
> > > I hope it is not an explicit data leak, or no leak at all (which seems unlikely though), but rather some clever data exploitation
> > > 
> > > 
> > > 
> > > ## CPMP
> > > 
> > > I miss the days where people had to disclose every external data they used in competition forums.
> > > 
> > > 
> > > 
> > > ## Fae Gaze
> > > 
> > > Hi, I also miss that part. I would appreciate any help on that
> > > 
> > > 
> > > 


---

> ## Paul Mooney
> 
> Following up to note that we updated the solution file and rescored the submissions. The leaderboard page now shows the updated scores. Thanks again to the community members that disclosed this issue!
> 
> 
> 


---

> ## heartkilla
> 
> A link to the data would be appreciated 
> 
> 
> 
> > ## heartkilla
> > 
> > I will clarify. If this data is public and someone has access to it, they can still use it for analysis, even if it’s removed from the test set. 
> > 
> > 
> > 
> > ## dott
> > 
> > It is the 33k LMSYS dataset published on HF [https://huggingface.co/datasets/lmsys/chatbot_arena_conversations](https://huggingface.co/datasets/lmsys/chatbot_arena_conversations) and preprocessed by one of the Kagglers [https://www.kaggle.com/code/abdullahmeda/33k-lmsys-chatbot-arena-conversations](https://www.kaggle.com/code/abdullahmeda/33k-lmsys-chatbot-arena-conversations) into the competition format. We used the latter to detect the leak.
> > 
> > 
> > 
> > > ## heartkilla
> > > 
> > > That's the spirit. Thanks.
> > > 
> > > 
> > > 


---

> ## Fae Gaze
> 
> Thank you for the update and for handling this issue. Looking forward to the revised scores next week!
> 
> 
> 


---

> ## Wasiu Olaitan Garuba 
> 
> That's a lovely idea 
> 
> 
> 


---



* --- discussion numver 13, the number of votes :29 ---

# Unstable Deberta Training Results

**Valentin Werner** *Sat Jun 15 2024 18:19:14 GMT+0900 (日本標準時)* (29 votes)

I spent a lot of time trying the boosting approach without any tf-idf or transformer embeddings and am now moving back to training transformers. Now, early in the competition I trained a deberta-3-large model, which did not break any records, but at least learned something (like 1.039). However, all my current attempts are failing to learn yet again - even with the same parameters as the last time I trained.

Have you experienced similar results where doing rather small changes (e.g., the structure of the input string) results in the model suddenly being unable to learn at all? What are the "best practices" you learned for training deberta / llama & co during this competition (if you dont mind sharing).

Cheers!



---

 # Comments from other users

> ## James Day
> 
> I got 0.997 with deberta-v3-large by having it produce an embedding for each side of the conversation separately, then passing those embeddings to a small 2 layer fully connected classifier. That was my first baseline approach in this competition. It certainly isn't the most accurate, but worked better than what you're describing.
> 
> I haven't really had any stability problems in this competition, but most stability problems where a model fails to converge to anything better than random guessing that I've encountered in the past have stemmed from a misconfigured learning rate schedule, so you might want to try tinkering with that if you haven't already.
> 
> 
> 
> > ## Valentin WernerTopic Author
> > 
> > Welcome back to the competition, James - I remember you die some impressive training in DAIGT too. Looking forward to See you on top of the lb again!
> > 
> > Do I understand correctly that you are only using the embeddings or did you combine two deberta Models and add layers on top of it?
> > 
> > 
> > 
> > > ## James Day
> > > 
> > > My 0.997 baseline used the same deberta backbone to process each "side" of the conversation (where each side is essentially a concatenation of the initial prompt, model X's first response, the follow up prompt (if available), model X's second response… up to a 768 token max context length). The embeddings from the CLS token on each side (A & B) were then concatenated and fed to a small classification head. In other words, there was a single debeta model with a couple extra layers stacked on top. The whole thing was trainable - I did not use a frozen pretrained backbone to compute the embeddings.
> > > 
> > > The approach described above is easily beaten by scaling up to using Llama 3 8B as the foundation model.
> > > 
> > > 
> > > 


---

> ## Takamichi Toda
> 
> I am sharing what has been effective in my experiments. 
> 
> Now difficulty in securing computational resources, I am conducting experiments with DeBERTa xsmall. Please note that you may not achieve the same results due to environmental differences.
> 
> ### Label Smoothing
> 
> I am using CrossEntropyLoss and setting the label_smoothing parameter to 0.2. The reason is that competition data can be labelled differently for the same data, and I thought it could be said to be a kind of noisy data.
> 
> ### Within-task Pre-training
> 
> I train the Masked Language Model using the competition data and use these weights for fine-tuning.
> 
> ### Dropout Off
> 
> I adjusted the Dropout Ratio, but 0 was the most effective. 
> 
> Although I have heard that Dropout should be off for regression problems, this is not. I do not understand why the absence of Dropout yielded better accuracy.🧐
> 
> ### Adversarial Training
> 
> I tried AWP, and it was effective. I also plan to test other methods such as FGM.
> 
> 
> 
> > ## Valentin WernerTopic Author
> > 
> > have you had stable results between XSmall and Large? for me, the smaller models are not converging, so I only trained Large. This obviously has terrible Iteration Speed for the experiments.
> > 
> > Thanks for sharing!
> > 
> > 
> > 
> > ## Valentin WernerTopic Author
> > 
> > Once I tried training with AWP the model instantly learned nothing again - its quite interesting
> > 
> > 
> > 
> > > ## Takamichi Toda
> > > 
> > > Hmm, I wonder why.
> > > 
> > > Which model are you using? I am still using DeBERTa xsmall, so it might be due to the difference in model size.
> > > 
> > > How about applying a small value to the AWP Learning Rate?
> > > 
> > > In my case, it's 1e-4. By the way, the overall learning rate is 2e-5.
> > > 
> > > 
> > > 
> > > ## Valentin WernerTopic Author
> > > 
> > > I will have to look further into AWP, I guess. I have not used it before and took an existing kaggle notebook as basis. 
> > > 
> > > I had no success with any small model and only ever got close to 1.00 with deberta-3-large. I am also using effective batch size of 8 (2 x 4) and a lr of about 8e-6 - so that is muuuuch lower than yours… Time to do some more experiments :)
> > > 
> > > 
> > > 


---

> ## Valentin WernerTopic Author
> 
> I trained a deberta-3-large model yesterday and achieved 1.005 - same training params today get me about 1.07. It seems very unreliable to me - I have yet to schiebe good scores with lora
> 
> 
> 
> > ## James Day
> > 
> > Weird. For me the random variation from run to run is < 0.01. CV & LB are very well correlated too (pearson r = 0.97).
> > 
> > It sounds to me like something is broken or misconfigured in your training pipeline. It isn't a problem inherent to the data itself.
> > 
> > 
> > 
> > > ## yechenzhi1
> > > 
> > > Hi, may I ask how do you get your CV split? I randomly split 10% from the training dataset, and the score from CV and LB are very different, my CV score is 0.889, and LB is 0.922. 
> > > 
> > > 
> > > 


---



* --- discussion numver 14, the number of votes :27 ---

# Load 7b Gemma Keras without any memory issue and FAST.

**Marília Prata** *Sun May 12 2024 07:28:29 GMT+0900 (日本標準時)* (27 votes)

# A tip  to avoid memory issues while running your 1.1 -7b_instruct_en Gemma/Keras Model:

[Gemma 1.1 7B Int8 Load](https://www.kaggle.com/code/awsaf49/gemma-1-1-7b-int8-load) By Awsaf.

On the last topic (2 days ago ), I asked "How to work with Gemma Keras 1.1- 7b instruct-en WITHOUT your Kaggle Notebook being restarted cause you've allocated more memory than is avaiable. Then we should opt to Google Cloud or dismiss our work.

Some answers that I got to that previous topic:  I read/learned  that reducing batches and max_length could help me to load the model and face the memory issue.  Not always, it's a 7b (7 billion parameters model).

But, what if we don't have max_lenght and batches written on our Kaggle Notebook script? Sometimes it happens. Therefore, it's great to have a Plan B:

Fortunately, I found Awsaf's code and published my 1st Gemma 1.1-7b-instruct-en.  

So, take a look and check Awsaf's amazing, cristal clear code:

[Gemma 1.1 7B Int8 Load](https://www.kaggle.com/code/awsaf49/gemma-1-1-7b-int8-load) By Awsaf.

For the record, there aren't many 7b Gemma Keras  Kaggle Notebooks. Though we can find plenty of 2b Models.



---

 # Comments from other users

> ## Adnan Alaref
> 
> Good news for find solution, thanks for sharing  [@mpwolke](https://www.kaggle.com/mpwolke) 
> 
> 
> 
> > ## Marília PrataTopic Author
> > 
> > Indeed Alaref,
> > 
> > I was so happy that I was able to work with Gemma/Keras 1.1-7b_instruct-en without any memory issue that I felt that I should share this topic because very few showed appreciation to Awsaf's code (till yesterday he had only 6 votes for such a remarkable and useful code and  his 2 datasets.  
> > 
> > Maybe, kagglers didn't realize the importance of that code.
> > 
> > For the record, the Notebook ran in only GPU 15 minutes!  Isn't that great?
> > 
> > Besides, I was able to deliver the last Model that the hosts had pinned on this competition.
> > 
> > Not many users are working with 1.1_7b_instruct. In fact, I didn't read any other, except Awsaf's code.
> > 
> > It was almost my "Moby Dick" of models.
> > 
> > Thank you Alaref.
> > 
> > 
> > 


---



* --- discussion numver 15, the number of votes :26 ---

# LLM Models that can be used

**superferg** *Sat Jul 06 2024 21:28:26 GMT+0900 (日本標準時)* (26 votes)

May I ask which models everyone has tried? I tried the following model，Randomly select 20% of the samples as the validation set.：

| Model | Local Validation | Public Leaderboard |
| --- | --- | --- |
| Llama3-8B-instruct | 0.9419 | 0.954 |
| Llama3-8B | 0.9818 | 0.987 |
| Gemma2-9B-instruct | 0.9262 | 1.206 |
| Gemma2-9B | 0.9499 | 1.299 |

Gemma2-9B has obtained abnormal results, I guess it might be a problem with the inference. Does anyone have similar problems?

UPDATE:

With the [new public notebook](https://www.kaggle.com/code/emiz6413/inference-gemma-2-9b-4-bit-qlora), the correct results were obtained.

| Model | Local Validation | Public Leaderboard |
| --- | --- | --- |
| Llama3-8B-instruct | 0.9419 | 0.954 |
| Llama3-8B | 0.9818 | 0.987 |
| Gemma2-9B-instruct | 0.9262 | 0.930 |
| Gemma2-9B | 0.9499 | TODO… |


---

 # Comments from other users

> ## Valentin Werner
> 
> gonna leave this one here 😉
> 
> 
> 
> > ## superfergTopic Author
> > 
> > The current local validation set is 0.91X, I still can't migrate to LB. LoL
> > 
> > 
> > 
> > ## SAY WHAT
> > 
> > so funny！！！
> > 
> > 
> > 


---

> ## Valentin Werner
> 
> Gemma2-9B came out recently. The 9B makes it even harder to train, but it tops the performance benchmarks among these models
> 
> 
> 
> > ## Cody_Null
> > 
> > Were you able to pull the gemma2-9B into kaggle from huggingface or are you using the Gemma 2 · gemma-2-9b-pt · V1 on kaggle models? 
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > We pulled gemma2-9b from huggingface into kaggle.
> > > 
> > > 
> > > 
> > ## s111mple
> > 
> > Finetuned model donnot get fine results~ Have you tried it?
> > 
> > 
> > 


---

> ## xiaotingting
> 
> It seems that the validation set index is positively correlated with the public score, and there is still room for further improvement of the index.
> 
> 
> 


---

> ## Xiot1206
> 
> thanks for providing these key information
> 
> 
> 


---

> ## lllleeeo
> 
> As an nlp newbie, I'd like to ask a possibly stupid question, how did you determine how many parameters you needed to use to participate in the fine-tuning, did you try them one by one? How much is generally best based on experience, is it different for different models, I observed that the public laptop fine-tuning in liama 8b only used 0.02% of the parameters is this too little?
> 
> 
> 
> > ## superfergTopic Author
> > 
> > If there is not enough computing power, using the Lora fine-tuning method may be the only choice.
> > 
> > 
> > 
> > > ## lllleeeo
> > > 
> > > Thanks for your reply! I've rented an A100 and a 4090 and want to do some experiments in parallel, I'm wondering if I can try more parameters based on that computing power, but I'm not sure how much I should start trying.
> > > 
> > > 
> > > 
> > > ## superfergTopic Author
> > > 
> > > The first step can try the top-level public notebook.
> > > 
> > > 
> > > 
> > > ## lllleeeo
> > > 
> > > Thank you it works！
> > > 
> > > 
> > > 


---

> ## Mr.T
> 
> How do you load gemma 2-9b during inference?
> 
> 
> 
> > ## superfergTopic Author
> > 
> > Please refer to the notebook below：
> > 
> > [https://www.kaggle.com/code/emiz6413/inference-gemma-2-9b-4-bit-qlora](https://www.kaggle.com/code/emiz6413/inference-gemma-2-9b-4-bit-qlora)
> > 
> > 
> > 


---

> ## EISLab_hwlee
> 
> Can the Gemma2-27B-instruct model perform better?
> 
> 
> 
> > ## EISLab_hwlee
> > 
> > As a result of the experiment, it was observed that the performance was poor.
> > 
> > 
> > 
> > > ## superfergTopic Author
> > > 
> > > I still can't complete the reasoning of 27B within 9 hours, theoretically, 27B should achieve better results.
> > > 
> > > 
> > > 
> > > ## EISLab_hwlee
> > > 
> > > I also failed to submit it.
> > > 
> > > However, in training, the loss did not fall below 1.0, and the evaluation loss did not fall below 1.0.
> > > 
> > > 
> > > 


---

> ## hn
> 
> Just curious, what was the missing piece that lead to your poor inference results from Gemma2? I see that you mentioned it’s fixed with the public notebook 
> 
> 
> 
> > ## superfergTopic Author
> > 
> > I don't have enough time to figure out the reason, but you can analyze the reason by comparing the following two notebooks.
> > 
> > [https://www.kaggle.com/code/emiz6413/llama-3-8b-38-faster-inference](https://www.kaggle.com/code/emiz6413/llama-3-8b-38-faster-inference)
> > 
> > [https://www.kaggle.com/code/emiz6413/inference-gemma-2-9b-4-bit-qlora](https://www.kaggle.com/code/emiz6413/inference-gemma-2-9b-4-bit-qlora)
> > 
> > 
> > 


---

> ## Mukatai
> 
> In a recent public notebook, a score of 0.941 was recorded with fine-tuning of Gemma2, but this table shows a score of 0.930 with Gemma2-9B-instruct. Is there any difference?
> 
> 
> 
> > ## superfergTopic Author
> > 
> > I am using my own training script, so there should be some differences, I can make it public after the competition ends.
> > 
> > 
> > 
> > > ## Mukatai
> > > 
> > > Thank you. Is Gemma's training conducted on Kaggle? With a public notebook, training on a single dataset exceeds the 30-hour weekly limit
> > > 
> > > 
> > > 


---

> ## Femca7
> 
> May I ask the results you get is from pre-trained or finetuned model ?
> 
> 
> 
> > ## superfergTopic Author
> > 
> > You can see the details in the table I provided, those with an 'instruct' suffix are fine-tuned models.
> > 
> > 
> > 


---

> ## yechenzhi1
> 
> May I ask if Instruct model is better than the base model? I have only tried Instruct model.
> 
> 
> 
> > ## superfergTopic Author
> > 
> > According to my local testing, Llama3-8B instruct is better than Llama3-8B. But perhaps the appropriate hyperparameters for  Llama3-8B have not been found.
> > 
> > 
> > 
> > ## ducnh279
> > 
> > I also had a similar question in the early days when I started with fine-tuning decoder-only models for text classification! 
> > 
> > I asked [@rasbtn](https://www.kaggle.com/rasbtn) (a prominent researcher/educator) on Twitter! He replied:
> > 
> > I also conducted some experiments, and the results indicate that using instruction-tuned versions often gives better performance and faster convergence compared to the base model.
> > 
> > 
> > 
> > > ## yechenzhi1
> > > 
> > > Thanks! That's really helpful!
> > > 
> > > 
> > > 


---



* --- discussion numver 16, the number of votes :26 ---

# Gemma 2 has been released

**Anil Ozturk** *Fri Jun 28 2024 00:49:26 GMT+0900 (日本標準時)* (26 votes)

Google has released the v2 for Gemma. It is available in two versions: 9B and 27B. You might want to try the 9B one.

HuggingFace: [https://huggingface.co/collections/google/gemma-2-release-667d6600fd5220e7b967f315](https://huggingface.co/collections/google/gemma-2-release-667d6600fd5220e7b967f315)



---

 # Comments from other users

> ## Valentin Werner
> 
> If they keep making the small models bigger, kaggle should keep making GPUs bigger 😉
> 
> 
> 
> > ## Enter your display name
> > 
> > Agree, also many packages now no longer support installation on older GPUs like the T4.
> > 
> > 
> > 
> > ## Yashchavn
> > 
> > true, lets see what happens
> > 
> > 
> > 
> > ## SunshineMoment
> > 
> > Agree! we need more powerful gpu
> > 
> > 
> > 


---

> ## Cody_Null
> 
> Update: I have found the reason. The top here causes an OOM error while the bottom works fine. 
> 
> `
> 
> # BitsAndBytes configuration
> 
> ```
> bnb_config =  BitsAndBytesConfig(
>     load_in_8bit=True,
>     bnb_8bit_compute_dtype=torch.float16,
>     bnb_8bit_use_double_quant=False)
> 
> bnb_config = BitsAndBytesConfig(
>     load_in_8bit=True,
>     bnb_8bit_quant_type="nf8",
>     bnb_8bit_use_double_quant=True,
>     bnb_8bit_compute_dtype=torch.bfloat16)
> 
> ```
> 
> `
> 
> 
> 
> > ## Lucifer_is_back_
> > 
> > thanks for that!
> > 
> > 
> > 
> > > ## Matous Famera
> > > 
> > > [@luciferisback](https://www.kaggle.com/luciferisback) I have read Gemma 2 outperforms Llama 3 8b in several benchmarks. I don't know if Gamma 2 can be implemented in this competition though.
> > > 
> > > 
> > > 
> > ## mbyc_xkyz_2023
> > 
> > but , after i strat my code, Unused kwargs: ['bnb_8bit_quant_type', 'bnb_8bit_use_double_quant', 'bnb_8bit_compute_dtype']. These kwargs are not used in , how to understand?
> > 
> > 
> > 


---

> ## xiaotingting
> 
> Gemma v2 is indeed the most useful one I have tried in this competition.
> 
> 
> 


---

> ## Nikhil Tumbde
> 
> Added the 9b base model on kaggle, [here](https://www.kaggle.com/models/nikhiltumbde/gemma-2-9b-hf)
> 
> 
> 


---

> ## Rishit Jakharia
> 
> ### Regarding the GGUF files
> 
> - Did anyone manage to use the Gemma 2 GGUF files on Kaggle
> 
> I am unable to do so myself, as I'm using llama cpp  and the latest version of llamaCPP seems to not be compatible with Kaggle
> 
> 
> 


---

> ## Guocheng Song
> 
> wow， that's amazing
> 
> 
> 


---



* --- discussion numver 17, the number of votes :25 ---

# Converted Ultrafeedback data (External Data)

**Takamichi Toda** *Fri Jun 07 2024 19:14:14 GMT+0900 (日本標準時)* (25 votes)

I have converted Ultrafeedback data shared by [@thedrcat](https://www.kaggle.com/thedrcat) into competition data.

Unlike competition data, Ultrafeedback data has a rating. This means that the model with the higher rating is the winner and the tie is the "tie".

Please see that:

Convert Code: [https://www.kaggle.com/code/takamichitoda/lmsys-convert-ultrafeedback-to-competition](https://www.kaggle.com/code/takamichitoda/lmsys-convert-ultrafeedback-to-competition)

Dataset: [https://www.kaggle.com/datasets/takamichitoda/lmsys-ultrafeedback](https://www.kaggle.com/datasets/takamichitoda/lmsys-ultrafeedback)

I would like to thank [@thedrcat](https://www.kaggle.com/thedrcat) for initially sharing this data.

Please make sure to upvote the [original discussion](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/499756).





* --- discussion numver 18, the number of votes :24 ---

# lmsys chat 1m (is Allowed? - dataset consists of user interactions from the ChatBot Arena) [Solved - Allowed]

**SeshuRaju 🧘‍♂️** *Fri May 03 2024 14:00:35 GMT+0900 (日本標準時)* (24 votes)

## [IMSYS Chat 1M](https://huggingface.co/datasets/lmsys/lmsys-chat-1m)

## KeyValue

| Metric | Value |
| --- | --- |
| Conversations | 1,000,000 |
| Models | 25 |
| Users | 210,479 |
| Languages | 154 |
| Avg. # Turns per Sample | 2.0 |
| Avg. # Tokens per Prompt | 69.5 |
| Avg. # Tokens per Response | 214.5 |

## [Paper - LMSYS-CHAT-1M: A LARGE-SCALE REAL-WORLD LLM CONVERSATION DATASET](https://arxiv.org/pdf/2309.11998)

- LMSYS-Chat-1M is collected from April to August 2023 - on website [https://chat.lmsys.org/](https://chat.lmsys.org/)

- The dataset contains raw conversation text without any processing. To ensure the safe release of

  data, we have made our best efforts to remove conversations that contain personally identifiable

  information (PII).

- The dataset includes one million conversations from 25 state-of-the-art LLMs with 210K users

  across more than 150 languages.

- We remove prompts that are either too short (fewer than 32 characters) or too long (more than 1536 characters).

- Biased user distribution : The majority of users of our website are LLM hobbyists and researchers who are interested in trying and testing the latest LLMs. This suggests that the data

  might not fully represent the broader population. For instance, everyday users or individuals

  from different professions might interact with the LLMs in varied ways. Consequently, results

  derived from this dataset might not generalize across all user groups.

- Containing repeated and low-quality data : The lack of user registration and data filtering can

  result in a significant amount of low-quality and duplicate data. However, we choose to not

  apply any filtering on purpose to reflect the real-world distribution.

- No human preference annotations. This dataset contains raw conversations without any human

  preference annotations. While our website does collect some user votes, we plan to examine

  the quality further before releasing them. We encourage the community to check the human

  preference data released in (Zheng et al., 2023).

# We can compare the Kaggle dataset with 1m dataset

- is PII added and removed more similar prompts or questions as suggested by paper ?

- Generate targets for the filtered dataset using GPT-4

- We can probe LB to check is this data topics exists in private LB ( as 20 clusters  for random 100k as per paper )



---

 # Comments from other users

> ## Lisa DunlapCompetition Host
> 
> Hello! Organizer here: yes it is allowed :)
> 
> 
> 


---

> ## Gaurav Rawat
> 
> Had exactly the same question about some of the lmsys datasets on hugging face ideally most are open I am guessing should be fine
> 
> 
> 
> > ## SeshuRaju 🧘‍♂️Topic Author
> > 
> > I expected the same, till now organiser not conformed. maybe we can consider it as Yes
> > 
> > 
> > 


---



* --- discussion numver 19, the number of votes :22 ---

# Mistral-NeMo release

**Ashwani** *Fri Jul 19 2024 01:09:26 GMT+0900 (日本標準時)* (22 votes)

Mistral-NeMo 12B released 

- Outperforms Gemma2 9B and Llama3 8B

- 128K context window

- Multilingual in 100+ languages: excels in European, Asian & Indian languages

- Quantization-Aware Training at FP8

- Apache 2.0 license

Blog: [https://mistral.ai/news/mistral-nemo/](https://mistral.ai/news/mistral-nemo/)

HF Weights (Base): [https://huggingface.co/mistralai/Mistral-Nemo-Base-2407](https://huggingface.co/mistralai/Mistral-Nemo-Base-2407)

HF Weights (Instruct): [https://huggingface.co/mistralai/Mistral-Nemo-Instruct-2407](https://huggingface.co/mistralai/Mistral-Nemo-Instruct-2407)



---

 # Comments from other users

> ## James Day
> 
> FYI, it appears finetuning for Mistral-NeMo is currently broken in the transformers library (see [https://huggingface.co/mistralai/Mistral-Nemo-Instruct-2407/discussions/6](https://huggingface.co/mistralai/Mistral-Nemo-Instruct-2407/discussions/6)). A fix should be released soon ([https://github.com/huggingface/transformers/pull/32065](https://github.com/huggingface/transformers/pull/32065)).
> 
> As usual, I'm inclined to wait at least a couple days for bugs to be discovered and fixed before attempting to use any new model 😉.
> 
> 
> 


---

> ## Lorry Zou
> 
> I just fune-tuned the instruct model yesterday, seems like it's not even on par with Gemma2 9b…Weird
> 
> 
> 
> > ## Valentin Werner
> > 
> > Might be the bugs James mentioned. These bugs are not always not always black and white, as in they raise Exceptions. Could also be that a different attention mechanism is used, which the model was not trained on or such (not sure if that is actually a thing and if it would cause an Exception, but you probably get the gist)
> > 
> > 
> > 
> > ## Eisuke Mizutani
> > 
> > I installed the latest transformers from source and could run training without error.
> > 
> > But as Lorry Zou mentioned, the result was not so good (even worse than llama3 in my case).
> > 
> > 
> > 


---

> ## EISLab_hwlee
> 
> It's very difficult to implement the code…
> 
> 
> 


---

> ## Valentin Werner
> 
> Release Season going hard in the last 5 weeks of the competition 🚀
> 
> 
> 
> > ## Psi
> > 
> > Thankfully, only three weeks left :)
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > It's quite funny with the GenAI Hype. You may have a breakthrough in the NLP competitions not by modelling techniques, but by sheer coincidence, having companies like H2O, Google or Mistral (& NVIDIA) release some high quality models. Not so long ago, we used to train Mistral-7B for peak performance - now it seems like a 3rd choice model.
> > > 
> > > 
> > > 


---

> ## gentle bird
> 
> new model. who is trying this?
> 
> 
> 


---



* --- discussion numver 20, the number of votes :22 ---

# Share my initial experiment

**suguuuuu** *Thu Jul 04 2024 01:24:22 GMT+0900 (日本標準時)* (22 votes)

Since it seems I won't be able to continue this competition, I am sharing a concept that I explored a month ago. It's possible that similar content has already been shared in other discussions.

It might be completely meaningless information.

## update (2024/07/06)

Upload results. [https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/516806#2905904](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/516806#2905904)

## Initial Approach

Compare texts across various criteria  based on a weighted average score according to categories.

### Evaluation Criteria:

```
1. **Clarity**: AI can provide clear answers to specific questions. However, when questions are ambiguous or open to multiple interpretations, AI may not always deliver the optimal response.

2. **Accuracy of Information**: AI answers are based on the data and information provided. Thus, if the source is accurate, the AI's response is accurate. However, AI lacks the capability to discern incorrect information from sources.

3. **Completeness**: AI can provide comprehensive answers to questions, but only within the scope of what it has understood and learned. Unlike humans, AI does not possess the ability to supplement information based on intuition or experience.

4. **Conciseness**: AI is capable of delivering concise responses. However, what qualifies as "concise" can largely depend on context and human subjectivity, making it challenging for AI to always meet human expectations for brevity.

```

### Categories:

- Informational Queries:

Accuracy of Information: Most crucial. If the information sought by the user is inaccurate, the value of the response significantly decreases.
Completeness: Next in importance. Providing all necessary information comprehensively is expected to fully resolve the user's queries.
Clarity: It is also important that accurate information is presented in an understandable manner.
Conciseness: Important, but often secondary to accuracy and completeness. However, irrelevant information should be avoided.

- Dialogue and Engagement Queries:

Clarity: For engaging effectively, it is crucial that responses are easy to understand.
Conciseness: Favored for maintaining fluid dialogue; responses should be brief and clear.
Accuracy of Information: Accuracy remains important in dialogic contexts, but because entertainment elements may be involved, strict accuracy isn't always necessary.
Completeness: Important, but not always necessary to cover every aspect to advance the dialogue.

- Emotional Support and Consultation Queries:

Clarity: Responses that resonate with users' emotions need to be particularly clear.
Accuracy of Information: Reliable information or advice is necessary when providing emotional support.
Completeness: Providing a comprehensive view on the issue helps users feel reassured.
Conciseness: While important, it is somewhat secondary compared to other factors.

- Troubleshooting Queries:

Accuracy of Information: Accurate troubleshooting steps and information are extremely crucial.
Clarity: Solutions must be clear for users to resolve issues.
Completeness: Covering all necessary steps required for problem resolution is demanded.
Conciseness: Useful but considered least crucial among the factors, though irrelevant information should be omitted.

## Experiments :

Utilized ChatGPT-4o for a trial with 500 data points.

- normal_prediction
Accuracy : 0.492

- predict with criteria
Accuracy : 0.514

Example result:

- ground truth and input data

```
  winner_model_a    0
  winner_model_b    1
  winner_tie        0
  ["What is the scientific probability of earth being the only habitable planet in the universe?","I don't think it really matters what some scientists \"think\" because it's very possible it could all be a simulation. And there's actual evidence to back that up.","But what makes that a \"radical\" possibility, when it's the possibility with actual evidence?"]

```

- Predict with ChatGPT-4o

winner model B

```
  ★res_a:
  Clarity: 4
  Accuracy of Information: 4
  Completeness: 5
  Conciseness: 3

  Reasoning:
  - Clarity: Responses are generally clear and appropriate for the questions, but occasionally complex words or concepts are used, requiring specialized knowledge for full understanding.
  - Accuracy of Information: The provided information is accurate and based on the latest scientific findings, although some claims about the simulation hypothesis are philosophical and lack scientific evidence.
  - Completeness: Responses are very comprehensive, considering the issue from multiple perspectives.
  - Conciseness: While detailed, the responses are sometimes lengthy and can feel redundant, so a more concise presentation could improve them.

  ★res_b:
  Clarity: 5
  Accuracy of Information: 5
  Completeness: 5
  Conciseness: 4

  This response is clear and accurate, providing relevant information comprehensively. However, some parts are slightly verbose, thus a conciseness score of 4.

```

- prompt/code

```
import requests
import pandas as pd
from time import sleep
from tqdm import tqdm

def generate_response_for_LMSYS(api_key, prompt):
    url = "https://api.openai.com/v1/chat/completions"
    headers = {
        "Authorization": f"Bearer {api_key}",
        "Content-Type": "application/json",
    }
    data = {
        "model": "gpt-4o",
        "messages": [
            {"role": "system",                  
                "content": "Please evaluate each response on a scale of up to 5 points. Format it as 'Clarity:x, Accuracy of Information:x, Completeness:x, Conciseness:x'. "},         
            {"role": "user", "content": prompt}
        ],
        "temperature": 0.7,
        "max_tokens": 1000
    }

    response = requests.post(url, json=data, headers=headers)
    if response.status_code == 200:
        return response.json()['choices'][0]['message']['content']
    else:
        return "Error: " + response.text    

idx = 150
print(train[["winner_model_a","winner_model_b","winner_tie"]].iloc[idx])

print(train["prompt"].iloc[idx])

print()
print("======================")
print( train["response_a"].iloc[idx])

print()
print("======================")
print( train["response_b"].iloc[idx])

all_prompt = f"""
        Analyze the prompt and responses(response_a, response_b) from two chatbots(model_a, model_b).
        Then predict the human preference of those responses- if it is "winner_model_a", "winner_model_b" or
        "winner_tie". Return the answer as the correspoding preference label "winner_model_a", "winner_model_b" or
        "winner_tie".
        ----------------------------------------------------------------------------------------------------------
        prompt: {train["prompt"].iloc[idx]}
        ----------------------------------------------------------------------------------------------------------
        response_a: {train["response_a"].iloc[idx]}
        ----------------------------------------------------------------------------------------------------------
        response_b: {train["response_b"].iloc[idx]}
        ----------------------------------------------------------------------------------------------------------
        Preference=  """.strip()

res = generate_response_for_LMSYS(api_key, all_prompt)
print(res)

```



---

 # Comments from other users

> ## Valentin Werner
> 
> What was your idea behind this approach?
> 
> At first it seems logical to try this with text generation, apart from the downfall of generation speed, which is way slower than sequence classification. However, you dont want to classify a winner, but probabilities - so every misclassification hurts so much more. 
> 
> I think its pretty interesting to see that GPT-4o with Reasoning does not necessarily outperform / is on-par with a properly finetuned deberta3base 
> 
> 
> 
> > ## suguuuuuTopic Author
> > 
> > Thanks for your comments!
> > 
> > I am going to implement DeBERTa or LLaMA3 as an auxiliary loss. 
> > 
> > The reason is that I hypothesized this will enable the model itself to score based on the Criteria and Categories of the text, ultimately having a positive impact on performance.
> > 
> > I came up with this idea from this discussion. I thought that performance might improve by making this more detailed.
> > 
> > [https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/499756](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/499756)
> > 
> > I'll skip the explanation of the effects of AuxLoss, as it's used in other Kaggle competitions as well.
> > 
> > e.g. [https://www.kaggle.com/competitions/rsna-breast-cancer-detection/leaderboard](https://www.kaggle.com/competitions/rsna-breast-cancer-detection/leaderboard)
> > 
> > I was preparing to do labeling using ChatGPT.
> > 
> > 
> > 
> > > ## nahyat
> > > 
> > > I've learned a lot from this. Thank you.
> > > 
> > > You said that you use Llama3 or Deberta as auxiliary loss, but does auxiliary loss mean that you obtain the output of the main task and the output of the subtask from a single model by branching and use them for the loss?
> > > 
> > > I would appreciate it if you could let me know if you could share your thought and ideas.
> > > 
> > > 
> > > 
> > > ## suguuuuuTopic Author
> > > 
> > > Yes, at first, I was going to use subtask as you said.
> > > 
> > > My just idea, It would be interesting to use the subtask prediction results and lightgbm to predict the final results.
> > > 
> > > 
> > > 


---

> ## suguuuuuTopic Author
> 
> I uploaded results of my experiment. It is written in Japanease. 
> 
> [https://www.kaggle.com/datasets/sugupoko/chatbotarena-output-by-gpt4o](https://www.kaggle.com/datasets/sugupoko/chatbotarena-output-by-gpt4o)
> 
> 
> 
> > ## Shota Yamasaki
> > 
> > 有益な情報をありがとうございます！
> > 
> > カテゴリに応じた加重平均スコアに基づいて、さまざまな基準でテキストを比較することは重要だと理解できました。
> > 
> > この実験で得た結果をこの後どう活かすつもりだったのでしょうか？
> > 
> > 非常に興味深いです。
> > 
> > 
> > 
> > > ## suguuuuuTopic Author
> > > 
> > > I wrote it above!
> > > 
> > > 
> > > 


---



* --- discussion numver 21, the number of votes :22 ---

# Both the A and B responses are [null]

**Takamichi Toda** *Mon May 13 2024 09:43:54 GMT+0900 (日本標準時)* (22 votes)

During the data analysis, I found samples where the responses for both A and B were [null]. 

Most of these cases arewinner_tie, so it would be best to handle them with rules rather than using ML model.

```
import pandas as pd
train_df = pd.read_csv(f"/kaggle/input/lmsys-chatbot-arena/train.csv")

row = train_df[train_df["id"] == 57180984].iloc[0]
res = row[["response_a", "response_b", "winner_model_a", "winner_model_b", "winner_tie"]].to_dict()
print(res)
# {'response_a': '[null]', 'response_b': '[null]', 'winner_model_a': 0, 'winner_model_b': 0, 'winner_tie': 1}

```

On the other hand, there are some cases where both are [null] yet a winner is determined. 

```
row = train_df[train_df["id"] == 867270727].iloc[0]
res = row[["response_a", "response_b", "winner_model_a", "winner_model_b", "winner_tie"]].to_dict()
print(res)
# {'response_a': '[null]', 'response_b': '[null]', 'winner_model_a': 1, 'winner_model_b': 0, 'winner_tie': 0}

```

How should this be interpreted? 

|  | n_sample | id |
| --- | --- | --- |
| winner_tie | 12 | 57180984, 249576331, 563620901, 939431975, 1224714333, 1433968841, 1833691834, 2624561104, 3013893052, 3697544388, 3731007975, 3870030183 |
| winner_model_b | 4 | 2369712796, 2542474454, 3044249115, 3174500072 |
| winner_model_a | 3 | 867270727, 2941706797, 3235570281 |

For now, it seems better to exclude both [null] data from the training data.



---

 # Comments from other users

> ## Lisa DunlapCompetition Host
> 
> While we removed any single turn conversations with null values with both responses, we chose to not filter these out in multi turn conversations.
> 
> Two things to take into consideration when interpreting the data are: (1) nothing prevents users on Chatbot Arena from voting erratically; and (2) users on Chatbot Arena vote one time per conversation (even for multi-turn conversations).
> 
> For example, if someone submits multiple prompts in rapid back-to-back succession, or if there is some sort of platform error, this can introduce null responses into a conversation that also has valid responses, and then it is up to the individual user how they want to rank the full conversations.
> 
> 
> 
> > ## Lisa DunlapCompetition Host
> > 
> > Correction: it looks like there are a few instances of single turn conversations with "[null]" values in the dataset. Since this appears very rarely, we will not be making any changes to the training dataset
> > 
> > 
> > 
> > > ## Takamichi TodaTopic Author
> > > 
> > > [This thread](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/502449) has also been discussed in this thread, and it seems like it will make for an interesting problem setting as a noisy problem.
> > > 
> > > Thank you for your reply.
> > > 
> > > 
> > > 
> > ## Kaizhao Liang
> > 
> > is it safe to assume this edge case will also be in the test set? mostly coming from how we should parse the inputs.
> > 
> > 
> > 
> > > ## Lisa DunlapCompetition Host
> > > 
> > > yes this could appear as a (very rare) edge case in the test set
> > > 
> > > 
> > > 


---

> ## Valentin Werner
> 
> You either ignore these cases completely and add these rules to your prediction post-processing OR you fix the labels to tie and train on that, hoping that your model learns it. 
> 
> 
> 
> > ## Takamichi TodaTopic Author
> > 
> > Thanks for the reply.
> > 
> > I am going to try to rule it out for now.
> > 
> > 
> > 


---



* --- discussion numver 22, the number of votes :21 ---

# Llama 3.1 has just been released

**lightsource<3** *Wed Jul 24 2024 00:08:21 GMT+0900 (日本標準時)* (21 votes)

There is 8b version weights: [https://llama.meta.com](https://llama.meta.com)

HF: [https://huggingface.co/collections/meta-llama/llama-31-669fc079a0c406a149a5738f](https://huggingface.co/collections/meta-llama/llama-31-669fc079a0c406a149a5738f)

Link to a technical article describing the development process: 

[https://scontent.fdxb2-1.fna.fbcdn.net/v/t39.2365-6/452256780_3788187148167392_9020150332553839453_n.pdf?_nc_cat=103&ccb=1-7&_nc_sid=3c67a6&_nc_ohc=XG3_BvYG0wwQ7kNvgEI9-4V&_nc_ht=scontent.fdxb2-1.fna&oh=00_AYAmG3EQLSTDlGlgdUqlvT6Z0uNBXoQcm_bCMhlFzDJ96A&oe=66A5A0DC](url)



---

 # Comments from other users

> ## Nicholas Broad
> 
> If anyone wants to use it in kaggle offline, it requires a newer transformers, and it is already a part of my [offline dataset for hugging face libraries](https://www.kaggle.com/datasets/nbroad/hf-libraries)
> 
> ```
> !pip install --no-deps --no-index /kaggle/input/hf-libraries/transformers/transformers-4.43.1-py3-none-any.whl
> 
> ```
> 
> 
> 
> > ## SAY WHAT
> > 
> > Thank you.
> > 
> > what is the version of torch?
> > 
> > 
> > 
> > > ## Nicholas Broad
> > > 
> > > you can use default in notebook
> > > 
> > > 
> > > 
> > ## YingxiZhang
> > 
> > Thanks for the reminder.
> > 
> > 
> > 


---

> ## Valentin Werner
> 
> 
> 
> Can't stop, won't stop.
> 
> 
> 
> > ## Valentin Werner
> > 
> > Thank god Mistral-Large 2 is closed source
> > 
> > 
> > 


---

> ## aadiAR
> 
> Thankyou for informing !
> 
> 
> 


---

> ## Kishan Vavdara
> 
> 
> 
> 
> 


---

> ## Taimo
> 
> 4bit 8B model has been uploaded by unsloth!
> 
> Base model:
> 
> [https://huggingface.co/unsloth/Meta-Llama-3.1-8B-bnb-4bit](https://huggingface.co/unsloth/Meta-Llama-3.1-8B-bnb-4bit)
> 
> Instruct model:
> 
> [https://huggingface.co/unsloth/Meta-Llama-3.1-8B-Instruct](https://huggingface.co/unsloth/Meta-Llama-3.1-8B-Instruct)
> 
> 
> 
> > ## Rishit Jakharia
> > 
> > Thanks ! For the information 
> > 
> > 
> > 


---

> ## Weiren
> 
> Currently training. Looking at the loss plot for a few steps, doesn't seem to outperform Gemma-2…. Maybe just my hyper params isn't good enough.🤡
> 
> 
> 
> > ## Rishit Jakharia
> > 
> > Please keep us updated if you plan to tune llama 3.1, also what quantization and config are you using, if I may know
> > 
> > 
> > 
> > ## Ivan Vybornov
> > 
> > I've attempted to train it 3 times by now and it does not even seem to outperform llama3 or at least it is not better by a margin.
> > 
> > 
> > 
> > > ## justin1357
> > > 
> > > same, worse than llama3
> > > 
> > > 
> > > 


---

> ## Robert0921
> 
> training, and testing
> 
> 
> 


---

> ## Muhammad Anas
> 
> Sounds great
> 
> 
> 


---

> ## SAY WHAT
> 
> There seems to be some problems with loading.
> 
> Anyway, let the bullets fly.
> 
> 
> 


---



* --- discussion numver 23, the number of votes :19 ---

# Data Understanding: Why prompt is list of strings?

**Siddhantoon** *Mon May 06 2024 20:36:28 GMT+0900 (日本標準時)* (19 votes)

| prompt examples |
| --- |
| ["Is it morally right to try to have a certain percentage of females on managerial positions?","OK, does pineapple belong on a pizza? Relax and give me fun answer."] |
| ["hey","write \"lollipop\" reversed"] |
| ["What's the difference between a sine and a line?","can you explain it even simpilier to me using examples?","how does a sine keep going or whats an analogy using sine the expresses a continuation?","What if AI becomes better than humans at everything. Maybe come up with an analogy involving geometry, thanks"] |

For some the output of model a and b is also list of 2 strings for some it is single string.



---

 # Comments from other users

> ## steubk
> 
> 87% of train samples are chats with single prompt, while others have more prompts and responses
> 
> 
> 


---

> ## namtran
> 
> Thank you for your finding. I will try to extract individual conversations and see if it improves the model.
> 
> 
> 


---

> ## Valentin Werner
> 
> I recommend playing around with the tool in general. This might also gives you a better feeling for the data and competition in general!
> 
> The answer is pretty simple: You are not evaluating individual prompts, but full chats.
> 
> While this opens a new question of "What happens if you evaluate a chat after every prompt" (which is possible) - I don't think it matters for the competition and assume that the data provided is always until the first evaluation.
> 
> 
> 
> > ## SiddhantoonTopic Author
> > 
> > So actually we aren't evaluating a "prompt and response", technically we are evaluating a "chat". This increases the complexity on how long the chat is in the data
> > 
> > 
> > 


---

> ## Rich Olson
> 
> great find.  looking through the data - it seems like this is very common.  
> 
> often the prompts seem disconnected from each-other - but sometimes they are clearly a continuing conversation.
> 
> 
> 


---

> ## Sparsh Tewatia
> 
> Even data is corrupt for around 200 rows, some null values , syntax errors. Will have to check for it in the test data
> 
> 
> 


---



* --- discussion numver 24, the number of votes :18 ---

# This Competition has an Official Discord Channel

**Myles O'Neill** *Fri May 03 2024 04:35:29 GMT+0900 (日本標準時)* (18 votes)

In addition to this competition forum, you can continue the discussion in our official Kaggle Discord Server here: 

# [discord.gg/kaggle](http://discord.gg/kaggle)

The Discord is a great place to ask getting started questions, chat about the nuances of this competition, and connect with potential team mates. Learn more about Discord at our [announcement here](https://www.kaggle.com/discussions/general/429933). Here are a few things to keep in mind though:

1. Discord Competition Channels are 'Public'

Discord channels for specific competitions are considered 'public' spaces where you are allowed to talk about competition details (it will not count as private sharing).

2. Discord Competition Channels are Not Monitored by Staff

Kaggle Staff and Hosts running competitions will not monitor Discord or be available to answer questions in Discord. Always post important questions in the forums.

3. Keep the Good Stuff on the Forums

Please keep important questions, insights, writeups, and other valuable conversation on the Kaggle forums. Discord is intended to be a more casual space to discuss competitions and help each other, we want to keep all the best information on the forums.

4. Remember to never privately share competition code or data

Please remember that private sharing of competition code or data is, as always, not permitted. Code sharing must always be done publicly through the Kaggle forums/notebooks.

I hope you’ll join us to chat on Discord soon!



---

 # Comments from other users

> ## Abel Punnoose
> 
> The best place to learn RLHF
> 
> 
> 


---

> ## Othmane Manessouri
> 
> Even though i'm still on my learning process i'll try to get better at this
> 
> 
> 


---

> ## kartikey bartwal
> 
> Thank You. I absolutely love Kaggle's collaboration mindset 🙌
> 
> 
> 
> > ## Yuwen He
> > 
> > I agree, I can learn a lot here
> > 
> > 
> > 


---



* --- discussion numver 25, the number of votes :17 ---

# More Interesting Observations to Share

**AbaoJiang** *Thu May 30 2024 01:06:45 GMT+0900 (日本標準時)* (17 votes)

Hi everyone,

Continuing [the previous discussion](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/508200), we want to share some more interesting observations.

### Empty Prompts

We all know that there exist missing responses, either None or empty (now  detected with regex ^\s*$). Today, we observe there are 5 samples with at least one empty prompt present during the conversation,

[](https://postimg.cc/q6hgRT8P)

Most of the time, models can continue to respond normally even if an empty prompt is sent by users. Another finding is that some models will throw an error message if an empty prompt is sent,

### Winner is the Model with an Missing Response

For a single-turn conversation, we expect the winner to be the one with a non-missing response. However, there's an interesting sample in which the winner is the model with an empty response, "" . Looking into the prompt, we realize what's going on! The prompt says Please reply with “<|endoftext|>”.

[](https://postimg.cc/GB9kYHnN)

That's all, happy kaggling!



---

 # Comments from other users

> ## Hafiz Nouman
> 
> Thanks for sharing this valuable information with references.
> 
> 
> 


---



* --- discussion numver 26, the number of votes :17 ---

# Less than 1.3 seconds per inference?

**Rishiraj Acharya** *Fri May 03 2024 14:21:19 GMT+0900 (日本標準時)* (17 votes)

There are approximately 25000 rows in test data and 9 hours runtime translates to less than 1.3 seconds per inference. Does this make usage of Large Language Models obsolete for this competition? I might not know of any LLM that runs this fast but I'm open to learning.



---

 # Comments from other users

> ## Raja Biswas
> 
> For my subs, the inference runtimes were as below (T4 x2):
> 
> - deberta-v3-large (~1.5hrs)
> 
> - mistral 7b (~4hr)
> 
> - llama3 8b (~4hr)
> 
> Max sequence length used: 1.8k
> 
> 
> 


---

> ## Siddhantoon
> 
> You can even batch process the data, why run every row sequentially.
> 
> 
> 


---

> ## Fritz Cremer
> 
> I published a deberta-v3-base notebook which predicts in under an hour. I think even deberta-v3-large should be no problem:
> 
> [https://www.kaggle.com/code/fritzcremer/lmsys-deberta-v3-base-baseline](https://www.kaggle.com/code/fritzcremer/lmsys-deberta-v3-base-baseline)
> 
> 
> 


---

> ## Angela
> 
> You are right. It seems that it is unable to utilize prompt engineering for LLM in this competition. 
> 
> 
> 


---



* --- discussion numver 27, the number of votes :17 ---

# How to work with Gemma Keras 1.1_7b instruct _en WITHOUT Google Cloud? On the 1.1_2b_instruct_en No Memory issue.

**Marília Prata** *Fri May 10 2024 10:43:46 GMT+0900 (日本標準時)* (17 votes)

I'm facing some memory issue with Gemma Keras 1.1 -7b- instruct-en.  It appeared that message "Your notebook tried to allocate more memory than is available. It has restarted".   Go to Google Cloud or dismiss it.

I even ran:

os.environ["XLA_PYTHON_CLIENT_PREALLOCATE"]="false"

  os.environ["XLA_PYTHON_CLIENT_MEM_FRACTION"]=".XX"

  os.environ["XLA_PYTHON_CLIENT_ALLOCATOR"]="platform"

Besides, I reduced the number of rows.

When I ran GemmaCausalLM the message that "The notebook tried to allocate more memory than is available" popped-up.

# Is there a way to work with Gemma Keras 1.1- 7b instruct -en WITHOUT  Google Cloud?

For the record, that doesn't occur on the other 7b models (7 billion parameters) that were pinned on this LMSYS competition.

Fortunately, I found Awsaf's code and published my 1st (Gemma 1.1-7b-instruct-en just 34 min. ago on May 10, 2024)

[Gemma 1.1 7B Int8 Load](https://www.kaggle.com/code/awsaf49/gemma-1-1-7b-int8-load) By Awsaf.

Thanks in advance,

Marília. 



---

 # Comments from other users

> ## Adnan Alaref
> 
> Hi [@mpwolke](https://www.kaggle.com/mpwolke) ,try to reduce batch size,restart the kernel
> 
> 
> 
> > ## Marília PrataTopic Author
> > 
> > My  batch_size = 1    Could it be lower? Zero or negative 😆
> > 
> > 
> > 


---

> ## Kaizhao Liang
> 
> I don't think we could load any pretrained model bigger than 1B, since the RAM runs out.
> 
> 
> 
> > ## Marília PrataTopic Author
> > 
> > I don't know how the model works on a submission due to its memory. However, I was facing issues even without submitting. Just at the beginning of the code.
> > 
> > Fortunately, I found Awsaf's code: [Gemma 1.1 7B Int8 Load](https://www.kaggle.com/code/awsaf49/gemma-1-1-7b-int8-load) and published my 1st (Gemma 1.1-7b-instruct-en just 34 min. ago)
> > 
> > Thank you Kaizhao.
> > 
> > 
> > 


---

> ## Matin Mahmoudi ✨
> 
> Try reducing the batch size, using mixed precision (float16), or lowering the memory fraction to handle Gemma Keras 1.1-7b. If that doesn't work, maybe go for a smaller model or use gradient accumulation [@mpwolke](https://www.kaggle.com/mpwolke).
> 
> 
> 
> > ## Marília PrataTopic Author
> > 
> > Hi Matin,
> > 
> > The batch size is only 1.
> > 
> > I changed to Gemma Keras 1.1_2b_instruct_en to reach at the end of the code (instead of the 7b).
> > 
> > Though the hosts pinned the 7b.
> > 
> > Thank you.
> > 
> > 
> > 


---



* --- discussion numver 28, the number of votes :16 ---

# Interpreting the metric & why current baselines are basically guessing

**Valentin Werner** *Tue May 07 2024 23:54:57 GMT+0900 (日本標準時)* (16 votes)

As all currently available baselines have a score > 1.0, I wanted to explore how to interprete this.

You can find my exploration in this notebook: [https://www.kaggle.com/code/valentinwerner/log-loss-what-are-good-scores/notebook](https://www.kaggle.com/code/valentinwerner/log-loss-what-are-good-scores/notebook)

Note that I am making some assumptions for simplicity, such as assuming that bad predictions are evenly distributed (e.g., instead of prediction [1,0,0] you are prediting [0.3, 0.35, 0.35] or [0.2, 0.4, 0.4]).

What I noticed it that:

- accuracy and loss are strongly misaligned and I am making the assumption that well calibrated models will get us a long way until we are able to achieve very good accuracy (which I assume is hard to do for this problem).

- current solutions are all basically guessing, as you can see in the graph below



---

 # Comments from other users

> ## bogoconic1
> 
> I feel that one contributing factor is
> 
> - The user doesn’t understand the responses from the LLM. It can arise from lack of domain knowledge of the topic he/she is trying to ask.
> 
> How does the user know if the answer is good in this case, or which one is better ? From personal experience, I have asked and seen LLM responses like this and I don’t know how to rate them
> 
> 
> 
> > ## Valentin WernerTopic Author
> > 
> > Agreed, I showed the tool many of my colleagues and there is a 50/50 chance that we disagree on what the better answer is. This makes it quite interesting. However, if you look at it in terms of individual model winrates, it must be possible to get scores well above the current levels
> > 
> > 
> > 
> > ## Dr. Gopalashivabalasubramanium Chandrashekaran
> > 
> > Similar to what Valentin said. The win rate will speak for itself for some models. Your thought on the subjective understanding of the user prompting is completely valid. It is an unknown. But maybe a weight can be applied to user prompt data based on grammar/length.
> > 
> > 
> > 


---



* --- discussion numver 29, the number of votes :15 ---

# Get started here!

**Addison Howard** *Tue Apr 09 2024 05:28:18 GMT+0900 (日本標準時)* (15 votes)

New to machine learning and data science? No question is too basic or too simple. Feel free to start your own thread, or use this thread as a place to post any first-timer clarifying questions for the Kaggle community to help you with!

New to Kaggle? Take a look at a few videos to learn a bit more about [site etiquette](https://www.youtube.com/watch?v=aIus8si_Et0), [Kaggle lingo](https://www.youtube.com/watch?v=sEJHyuWKd-s), and [how to enter a competition using Kaggle Notebooks](https://www.youtube.com/watch?&v=GJBOMWpLpTQ). Publish and share your [models on Kaggle Models](https://www.kaggle.com/docs/models#publishing-a-model)!

Looking for a team? Express your interest in joining a team through our [Team Up](https://www.kaggle.com/discussions/product-feedback/341195) feature .

Remember: Kaggle is for everyone. Whether you're teaming up or sharing tips in the competition forum, we expect everyone to follow our Kaggle community guidelines.



---

 # Comments from other users

> ## Roschild.Rui
> 
> Hi i am at a loss -> Why was it possible to submit almost identical inference weights and inference logic without any issues a few days ago, but recently there have been constant submission errors? It seems that the imbalance in Kaggle's computational resource load significantly affects the competition submissions. I would greatly appreciate it if you could answer my question.@Addison Howard
> 
> 
> 
> > ## Cody_Null
> > 
> > Yes, we have much better submissions we aren’t able to get working that were working only a few days ago. An idea of what is going on with the back end of things would be great!
> > 
> > 
> > 


---

> ## Yuliana Setianingrum
> 
> HAY EVERYONE !! Let's Enjoy Our journey in the exciting world of machine learning and data science!
> 
> 
> 


---

> ## Riad
> 
> hi all 😄
> 
> is there anyone want to make a group with me we can help each other to make better models
> 
> my linkdin :- [https://www.linkedin.com/in/riad-almadani-a735a01bb/](https://www.linkedin.com/in/riad-almadani-a735a01bb/)
> 
> 
> 


---

> ## ascender1729.eth
> 
> Excited for my first competition, any beginner tips?
> 
> 
> 


---

> ## Eetu Rantala
> 
> Hi everyone! I'm enjoying Fast.ai practical course which led me to try out kaggle competitions. I hope I can get ok result on this competition with my skills! :) 
> 
> 
> 


---

> ## Kumar Deblin
> 
> Hi Every one!
> 
> 
> 


---

> ## Vishal Maurya
> 
> Kaggle provides CPU and GPU while submission and scoring of notebooks. Just want to know, can we use TPUs? 
> 
> 
> 


---



* --- discussion numver 30, the number of votes :13 ---

# Feel overwhelmed with this competition  

**ducnh279** *Thu Jul 04 2024 04:37:33 GMT+0900 (日本標準時)* (13 votes)

Hi everyone,

Unlike other NLP competitions I've participated in, I believe that decoder-only models might outperform DeBERTa in this one. Running experiments with LLMs is very computationally and financially expensive for me, especially in this competition.

- For DeBERTa (large), I can manage to get LB: 0.993 (tuned) with 6-hour training using 2 x T4 on Kaggle

- For LLMs,  I've just run only one experiment with Mistral 7B (4-bit quantized + LoRA) and got LB: 0.991. 

For fine-tuning LLMs, one experiment is very slow and expensive to finish one fold in 15 hours with 1 A10G on Lightning Studios. If there is no special magic to get 0.9 to 0.95. I believe that by tuning (batch size, learning rate, warm-up steps, prompts), trying training tricks to stablize the training and avoid early performance saturation, or simply being able to run more than 1 epoch, I think I could get closer to LB: <= 0.95.

As a student, I find Kaggle competitions increasingly challenging and computationally expensive, particularly due to the limited access to free hardware. Relying on free GPUs from Kaggle and Colab, I often feel constrained and overwhelmed when competing.

Do you think I need to invest big bucks for this competition to pay off? As a broke student, I might have to hit up the Bank of Mom and Dad for a 'strategic investment'  haha😂



---

 # Comments from other users

> ## kagglethebest
> 
> Same feeling. 😂 I am trying to find a way to get nice score by using Deberta Base on Kaggle GPUs. If my trials are not worked, I will give up this competition.
> 
> 
> 
> > ## ducnh279Topic Author
> > 
> > Don't give up [@judith007](https://www.kaggle.com/judith007)! Let's fight until the last minute!
> > 
> > By the way, I recommend trying DeBERTa large and learning how to utilize two GPUs. I achieved a 0.988 score with DeBERTa large, which is the same score as the first public notebook using the 8-bit quantized LLaMA 8B.
> > 
> > 
> > 


---

> ## Valentin Werner
> 
> 
> 
> 
> 
> > ## Valentin Werner
> > 
> > Jokes aside, always prefer training models on hosted rental services rather than buying an expensive GPU. You can first validate on the slow kaggle GPUs / TPU or Google Collab etc. before going to the rental. The math for buying a 3090TI / 4080 / 4090 for Data Science it is not really mathing. I have a 4090 which is great for experiments, but I still cannot scale to the same experiments as the Kaggle TPU on it. 
> > 
> > It feels really bad being gates by compute resources. Stuff you can try out if renting is not an option: Some cloud providers provide research compute for limited time; you can ask your university / professors if they have compute you can do (maybe try to sell it as extra curicular, present your results in the end for some bonus points; my university had a 4x V100 setup with 128GB total that was mostly idling and my professor almost begged me to train some stuff on there so its used when nobody does research); 
> > 
> > 
> > 
> > > ## ducnh279Topic Author
> > > 
> > > Hahaha your meme tells my story! 
> > > 
> > > After this competition, I would learn about TPU training! Thanks SO much for sharing your experience!
> > > 
> > > 
> > > 


---

> ## Cody_Null
> 
> Glad someone else was able to get 7b models like mistral working in 4bit. Mine had a bug but didn’t seem like it was going to beat the llama models anyway :/ I understand your position though. It does feel that way sometime 
> 
> 
> 
> > ## ducnh279Topic Author
> > 
> > Thanks for your understanding! For sure, 7b models quantized in 4-bit will be definitely degraded in performance. You can use scaling law to set up the hyparams and try training techniques before running on the whole training set. Sorry I can't talk more about this before the competition ends.
> > 
> > 
> > 


---

> ## Taimo
> 
> Kaggle is a good starting point for students.
> 
> For educational purposes, Kaggle should remain such a place even though the size of models continues to be big. 
> 
> Google (Alphabet) should invest in more high-spec hardware for Kaggle.
> 
> 
> 
> > ## ducnh279Topic Author
> > 
> > For educational purposes, Kaggle should remain such a place even though the size of models continues to be big.
> > 
> > Agreed! I learned a lot through Kaggle competitions and the sharings from Kagglers! The "large" in models and datasets are not a too big problem with me! I will definitely continue learning and competing.
> > 
> > Google (Alphabet) should invest in more high-spec hardware for Kaggle.
> > 
> > We all hope so! hahaha
> > 
> > 
> > 


---

> ## xiaotingting
> 
> After I became a graduate student, I was fine and could use the server in the lab. But because I had to submit a paper recently and needed to do additional experiments, and there were other people in the lab using the server, I could only use it when they were not using it. If I want to fine-tune a large model, I really need a card. I currently rent two A100 cards to prepare for the experiments here, and each training takes at least two days. It is more cost-effective to rent it for the whole day, about 200 yuan for two cards a day, and it costs more than a thousand yuan to rent it for a week.
> 
> 
> 
> > ## KeShuang Liu
> > 
> > I was interning at the company and they provided me with two A800s, but due to my technical issues, I was unable to achieve good results.
> > 
> > 
> > 


---



* --- discussion numver 31, the number of votes :13 ---

# CV vs LB thread

**Stochoshi G** *Sat May 04 2024 12:56:33 GMT+0900 (日本標準時)* (13 votes)

Deberta-v3-xsmall: ~1.02 cv / 1.03 lb

Tfidf: ~1.02 cv / ~1.03 lb

Combined: ~1.00 cv / tbd

Siamese Deberta: [https://www.kaggle.com/code/stochoshi/deberta-starter-lmsys](https://www.kaggle.com/code/stochoshi/deberta-starter-lmsys)



---

 # Comments from other users

> ## Kishan Vavdara
> 
> My CV :
> 
>  1.02 Lb -> LB - 0.996
> 
>  0.98 Lb -> LB - 0.971
> 
>  0.96 Lb -> LB - 0.955
> 
>  0.95 Lb -> LB - 0.959
> 
> 
> 


---

> ## Takamichi Toda
> 
> My CV strategy is one hold-out, with a validation rate of 20%.
> 
> At present, it correlates well with the Public LB.
> 
> Best: Local=1.034074/Public LB1.036
> 
> 
> 
> > ## heartkilla
> > 
> > hi, you use random or stratified split?
> > 
> > 
> > 
> > > ## Takamichi Toda
> > > 
> > > random split
> > > 
> > > 
> > > 


---

> ## heartkilla
> 
> Any updates on this?
> 
> 
> 


---



* --- discussion numver 32, the number of votes :11 ---

# Expectation for Kaggle Resources?

**Cody_Null** *Thu Aug 01 2024 08:16:38 GMT+0900 (日本標準時)* (11 votes)

Hi all, my team as well as what seems like others seem to be struggling with submission times. Even submissions that we ran in 6 hours before are now timing out? We have significantly raised our CV in the last few days but have been entirely unable to get results for it due to this compute issue. I was hoping some of the Kaggle staff could help speak to what is going on? I am familiar that close to the end of competitions in the last 2 or 3 days things run a bit slower but we are experiencing 2 times longer inference time than 4 days ago and have been ever since 7 days to go! It would be a shame to put in all this work over the last several months and not get to benefit from putting it all together. 



---

 # Comments from other users

> ## Valentin Werner
> 
> Are you 100% sure you are running exactly the same script? We have been struggling with Resources too, but not along the lines of 50%. Eventhough this wastes a submission, if you have time for it, try the old notebook and version again.
> 
> To me it does not seem reasonable that participation rates raise GPU Processing times. It is not like we are all on the same two T4s. Also all the environments are containers, so they should be clean on every run.
> 
> 
> 
> > ## Cody_NullTopic Author
> > 
> > I totally agree, it is not completely identical but it is a small change and identical in simulated run times. It’s not quite a 50% slowdown but it’s fairly close! What once took 5.5 is now 9+
> > 
> > 
> > 
> > ## Rise_Hand
> > 
> > It's not same as container actually. Some sub obviously need more computer source can finish running faster than the one which need less. So it's just a luck game to be allocated to a better machine tbh
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > Agreed, over the lifecycle of every chip performance may vary. This also goes for room temperature at servers etc. 
> > > 
> > > The point, I am making about containerization is that when you submission is over you have a clean GPU, its not like you will share compute etc. - However, you can and will get worse chips. Its impossible for the kaggle team to have all GPUs available perform exactly the same. 
> > > 
> > > 
> > > 


---

> ## yechenzhi1
> 
> Try to reduce your max-length? I've encountered a similar issue, and I suspect that the test data may be longer than what we used for training.
> 
> 
> 


---

> ## Attacker
> 
> People's participation rate rises before the competition closes, so the server becomes unstable.
> 
> 
> 
> > ## Cody_NullTopic Author
> > 
> > That is true but I don’t notice anything different from this comp than others but I have never seen a 50% slowdown of submissions before :/ Of course we can’t expect Kaggle to have it be seamless especially when they are providing these GPUs for free but I would like a little more clarity on what is going on and if we should expect it to change before the deadline.
> > 
> > 
> > 


---

> ## Korey Ma
> 
> I am afraid that my new submissions will time out🫠
> 
> 
> 
> > ## Valentin Werner
> > 
> > 
> > 
> > 
> > 


---



* --- discussion numver 33, the number of votes :10 ---

# Has anyone tried lora variants like lora+, rslora, dora, and the latest lora-ga, lora-pro, and do they work better ?

**ShelterW** *Tue Jul 30 2024 04:27:50 GMT+0900 (日本標準時)* (10 votes)

I hear they're closer to full fine-tuning, so has anyone tried it in this competition? I tried dora and it worked just as well.

### Refer:

[1] LoRA: Hu, E. J., Shen, Y., Wallis, P., Allen-Zhu, Z., Li, Y., Wang, S., … & Chen, W. (2021). Lora: Low-rank adaptation of large language models. arXiv preprint arXiv:2106.09685.

[2] LoRA+: Hayou, S., Ghosh, N., & Yu, B. (2024). LoRA+: Efficient Low Rank Adaptation of Large Models. arXiv preprint arXiv:2402.12354.

[3] VeRA: Kopiczko, D. J., Blankevoort, T., & Asano, Y. M. (2023). Vera: Vector-based random matrix adaptation. arXiv preprint arXiv:2310.11454.

[4] LoRA-FA: Zhang, L., Zhang, L., Shi, S., Chu, X., & Li, B. (2023). Lora-fa: Memory-efficient low-rank adaptation for large language models fine-tuning. arXiv preprint arXiv:2308.03303.

[5] LoRA-drop: Zhou, H., Lu, X., Xu, W., Zhu, C., & Zhao, T. (2024). LoRA-drop: Efficient LoRA Parameter Pruning based on Output Evaluation. arXiv preprint arXiv:2402.07721.

[6] AdaLoRA: Zhang, Q., Chen, M., Bukharin, A., He, P., Cheng, Y., Chen, W., & Zhao, T. (2023). Adaptive budget allocation for parameter-efficient fine-tuning. arXiv preprint arXiv:2303.10512.

[7] DoRA: Liu, S. Y., Wang, C. Y., Yin, H., Molchanov, P., Wang, Y. C. F., Cheng, K. T., & Chen, M. H. (2024). DoRA: Weight-Decomposed Low-Rank Adaptation. arXiv preprint arXiv:2402.09353.

[8] Delta-LoRA: Zi, B., Qi, X., Wang, L., Wang, J., Wong, K. F., & Zhang, L. (2023). Delta-lora: Fine-tuning high-rank parameters with the delta of low-rank matrices. arXiv preprint arXiv:2309.02411.

[9] LoRA-GA: Wang, S., Yu, L., & Li, J. (2024). LoRA-GA: Low-Rank Adaptation with Gradient Approximation. arXiv preprint arXiv:2407.05000.

[10] LoRA-Pro: Wang, Z., & Liang, J. (2024). LoRA-Pro: Are Low-Rank Adapters Properly Optimized?. arXiv preprint arXiv:2407.18242.



---

 # Comments from other users

> ## James Day
> 
> I tried several of them with marginal success:
> 
> - LoRA+ - Seemed to converge faster earlier in training, but didn't make any difference after processing tens of thousands of examples (converged  to equally good model). Might be helpful for small datasets, but doesn't seem too useful for this competition.
> 
> - DoRA - Saw slight accuracy improvement vs. LoRA in early experiment back before I was tuning all linear layers, albeit at the expense of a 2x increase in training runtime. After various other changes (tuning all linear layers + some other things that might have a performance impact), the slowdown from using DoRA is even bigger, like 20x. Had to abandon this because my hardware isn't powerful enough to properly train even a single model with DoRA before the end of the competition and the gain would probably be small.
> 
> - AdaLoRA - Seemed to converge slower than normal LoRA (worse sample efficiency). Final model was worse than traditional LoRA baseline. Might be possible to get it working well with additional hyperparameter tuning, but continuing to experiment with this didn't seem like a good use of GPU time.
> 
> 
> 
> > ## CPMP
> > 
> > I tried DORA and have similar experience: 2x slowdown for no clear gain.
> > 
> > 
> > 


---

> ## Ashwani
> 
> I tried using RSLORA, DORA. 
> 
> RSLORA gave me performance improvements. 
> 
> DORA was taking way too much time (8-9x) hence didn't use it. 
> 
> 
> 
> > ## justin1357
> > 
> > In my exp, rs-lora did not help
> > 
> > 
> > 


---

> ## justin1357
> 
> LoRA-GA is the best in theory, it simulates the grad of finetune. But in the case of large dataset, all the methods are almost the same.
> 
> 
> 


---



* --- discussion numver 34, the number of votes :10 ---

# Llama3.1 works not as good as expect

**justin1357** *Wed Jul 24 2024 13:44:46 GMT+0900 (日本標準時)* (10 votes)

After first 1000 steps, i found its performence is worse than gemma-2 slightly.



---

 # Comments from other users

> ## Rise_Hand
> 
> I got a very bad result according to llama3.1 while using the ft method of QLoRA+SFT. CV = 0.914
> 
> 
> 


---

> ## Nicholas Broad
> 
> Make sure your tokenizer uses the [correct bos token](https://huggingface.co/meta-llama/Meta-Llama-3.1-8B-Instruct/discussions/29)
> 
> 
> 
> > ## justin1357Topic Author
> > 
> > still bad performance
> > 
> > 
> > 


---

> ## Xinyuan Qiao
> 
> I tested it in [@emiz6413](https://www.kaggle.com/emiz6413) notebook with exact same parameter, the evaluation log loss is 0.958, the gemma2 version was 0.927.
> 
> 
> 


---

> ## sayoulala
> 
> Thanks for share it. That's great, it looks like I'll be able to save a lot on my electricity bill, hahaha!
> 
> 
> 
> > ## william.wu
> > 
> > You're safe for the 1st place. It's tough to make improvements😭
> > 
> > 
> > 


---

> ## justin1357Topic Author
> 
> After 4000 steps, its significantly worse than gemma-2 haha
> 
> 
> 


---

> ## Lorry Zou
> 
> Thank you for saving our time and TPU quota😁
> 
> 
> 


---

> ## Yixiao Yuan
> 
> Same here.
> 
> 
> 


---



* --- discussion numver 35, the number of votes :10 ---

# How long does it tke to be granted access to Llama3 on Kaggle? [Solved: 24 hours]

**CPMP** *Thu Jul 11 2024 19:49:54 GMT+0900 (日本標準時)* (10 votes)

I got access immediately yesterday on Meta's site, but my request is still pending here.

Edit: I got access after 24 hours, which is reasonable. It is just that I got access on Meta immediately which sets optimistic expectations.



---

 # Comments from other users

> ## samson
> 
> Six days left for me. Access is not granted still. Thats why I got weights on HF
> 
> 
> 
> > ## CPMPTopic Author
> > 
> > Did you get access from Meta's site before asking for access here?
> > 
> > 
> > 
> > > ## samson
> > > 
> > > Yes, I did. BTW, I finally go it. It took them 7 days to give me an access
> > > 
> > > 
> > > 
> > > ## william.wu
> > > 
> > > OMG, I just requested the access yesterday… Is there any public llama3.1 models on Kaggle?
> > > 
> > > 
> > > 
> > > ## william.wu
> > > 
> > > Okay, I found one [https://www.kaggle.com/datasets/gmhost/llama31instruct](https://www.kaggle.com/datasets/gmhost/llama31instruct)
> > > 
> > > 
> > > 


---

> ## Allie K.
> 
> Good question. 
> 
> I have been waiting since last Friday morning, constantly updating the number of days of waiting (now it's 6) and repeating my questions to Kaggle team.
> 
> Perhaps you, with your authority, will be able to push things forward.🙂 
> 
> 
> 
> > ## CPMPTopic Author
> > 
> > I don't think I have more weight than anyone here.
> > 
> > 
> > 
> > > ## Allie K.
> > > 
> > > Apparently you do have!😀
> > > 
> > > As a magic, the access is here, after "only" 6 days.
> > > 
> > > 
> > > 
> > > ## CPMPTopic Author
> > > 
> > > Did you post? If yes then I will agree with you.
> > > 
> > > 
> > > 


---

> ## Psi
> 
> you can get it on HF, no need to apply here on kaggle
> 
> 
> 
> > ## CPMPTopic Author
> > 
> > I have access on HF and on Meta. I am asking why it is long here.
> > 
> > 
> > 


---

> ## RB
> 
> Hello , similar post here - [https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/518813](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/518813) 
> 
> and a workaround  [https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/518813#2913166](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/518813#2913166)
> 
> 
> 
> > ## CPMPTopic Author
> > 
> > I downloaded the model, no worries. I am asking a specific question.
> > 
> > 
> > 


---

> ## Valentin Werner
> 
> Welcome to the competition!
> 
> I already posted this before, but took 10 minutes for me a weekend.. 
> 
> 
> 


---

> ## Shelton
> 
> Nice work!
> 
> 
> 


---

> ## Nguyễn Anh Tú
> 
> Why i always get the error "Incorrect path_or_model_id: '/kaggle/input/llama-3/transformers/8b-hf/1'. Please provide either the path to a local folder or the repo_id of a model on the Hub" when using "tokenizer = AutoTokenizer.from_pretrained("/kaggle/input/llama-3/transformers/8b-hf/1")" ? Please helps me. Thanks.
> 
> 
> 
> > ## Valentin Werner
> > 
> > You have not been granted access for llama3 on Kaggle yet. Make sure to apply for access on meta and kaggle.
> > 
> > 
> > 
> > > ## Nguyễn Anh Tú
> > > 
> > > To solve that problem, I use another pretrain model from my another notebook. But I got the error "Submission Scoring Error" when I submitted my notebook, I thought that I set the wrong format for my submission.csv. Then, I read the sample_submission.csv and change the the value of ['winner_model_a', 'winner_model_b', 'winner_tie'] columns with my y_predict. The worst thing is my notebook ran successful but when I submitted again I got the error "Notebook Threw Exception", please help me!
> > > 
> > > 
> > > 
> > > ## XXX
> > > 
> > > Submission Scoring Error: Your notebook generated a submission file with incorrect format. Some examples causing this are: wrong number of rows or columns, empty values, an incorrect data type for a value, or invalid submission values from what is expected.
> > > 
> > > above is from kaggle debugging tips.
> > > 
> > > I think may be you can check the value of your submission🤔
> > > 
> > > 
> > > 


---

> ## Feisx Song
> 
> helpful tips!
> 
> 
> 


---



* --- discussion numver 36, the number of votes :10 ---

# LB Experiment: Modify Prediction Temperature

**Rich Olson** *Wed May 08 2024 10:31:30 GMT+0900 (日本標準時)* (10 votes)

I just put together a new notebook to see if adjusting the confidence of my predictions can improve LB performance:

[https://www.kaggle.com/code/richolson/lb-experiment-modify-prediction-temperature](https://www.kaggle.com/code/richolson/lb-experiment-modify-prediction-temperature)

The answer seems to be yes (a little).

The model for this notebook is identical to TF-IDF approach I used here:

[https://www.kaggle.com/code/richolson/lmsys-tf-idf-boosted-trees](https://www.kaggle.com/code/richolson/lmsys-tf-idf-boosted-trees) (LB 1.038)

The notebook works by adjusting the "temperature" of predictions.  Raw scores are divided by the temperature factor before being converted to probabilities.

In this case - increasing the temperature moves predictions closer to .33 (decreasing confidence).

Decreasing the temperature moves scores out towards 0 or 1 (increasing confidence).

I did a bunch of submissions.  Here are the resulting LB scores:

| Temp. Adjustment | LB |
| --- | --- |
| 1.3 | 1.044 |
| 1.0 | 1.038 (unchanged - as expected) |
| 0.85 | 1.036 (improved!) |
| 0.7 | 1.036 (improved!) |
| 0.5 | 1.052 |

So - it seems like the existing confidence of my model was close-to-optimal - but not quite.  Based on the clustering of scores - I doubt there is a lot more improvement to be made.

Adjusting the temperature of your predictions is quite easy:

```
#1. get raw logits
y_pred_raw = model.predict(combined_test_tfidf[-test.shape[0]:], raw_score = True)

#2. adjust temperature
adjusted_logits = y_pred_raw / temperature_factor

#3. convert to probs using softmax (from scipy.special)
preds_test = softmax(adjusted_logits, 1)

```

If this is interesting - you should also check out [@valentinwerner](https://www.kaggle.com/valentinwerner)'s notebook on this topic:

[https://www.kaggle.com/code/valentinwerner/log-loss-what-are-good-scores](https://www.kaggle.com/code/valentinwerner/log-loss-what-are-good-scores)

-Rich



---

 # Comments from other users

> ## Takamichi Toda
> 
> Thank you for suggesting this useful post-processing.
> 
> I also tried this post-processing, and the results were very good!!
> 
> When I looked at the relationship between temperature and score in the validation data, I found that it matched well with the LB results.
> 
> | Temp. Adjustment | LB |
> | --- | --- |
> | 0.8 | 1.036 |
> | 0.9 | 1.028 |
> | 1.0 | 1.025 |
> | 1.2 | 1.022 |
> | 1.4 | 1.024 |
> 
> (The vertical axis is logloss)
> 
> The temperature of 1.2, which had the highest score on the LB, was also close to the best in validation.
> 
> 
> 


---



* --- discussion numver 37, the number of votes :9 ---

# Why are there winners for the same prompt and response?

**JunHua Liao** *Mon May 13 2024 22:47:54 GMT+0900 (日本標準時)* (9 votes)

Why is prompt, response_a, and response_b the same, and there is a situation where model_a wins or model_b wins? Shouldn't it be winner_tie?



---

 # Comments from other users

> ## Valentin Werner
> 
> Does it make sense? No. Did the user click it? Yes.
> 
> 
> 


---

> ## Sergey Saharovskiy
> 
> [@feattar](https://www.kaggle.com/feattar) thanks for posting your findings, I will leave it here:
> 
> 
> 
> > ## Valentin Werner
> > 
> > 
> > 
> > 
> > 


---

> ## Asher B.
> 
> According to the blog [https://huyenchip.com/2024/02/28/predictive-human-preference.html](https://huyenchip.com/2024/02/28/predictive-human-preference.html)
> 
> shared in this discussion: [https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/499847](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/499847)
> 
> These are the noises and we may improve our model by droping these instances. Thanks for sharing!
> 
> 
> 
> > ## JunHua LiaoTopic Author
> > 
> > Thanks for sharing!
> > 
> > 
> > 
> > ## Kishan Vavdara
> > 
> > I think dropping them won't help much, test data may contain similar instances. If the model predicts tie for such instances with high prob, then such instances will be penalized more increasing log loss. Solution would be ensembles :)  
> > 
> > 
> > 
> > > ## Asher B.
> > > 
> > > Thanks for correction. I think dropping should be a good idea in production, but in this competition, that's ture! 
> > > 
> > > 
> > > 
> > > ## Valentin Werner
> > > 
> > > I am not sure if I agree - if we are unsure about the test data (much like we would be in producton), shoud we not strive to create a model that is robust, in the sense of predicting the objective truth?
> > > 
> > > It might be worth testing if we should provide more balanced predictions on these labels, like [0.3, 0.2, 0.5] - as first model might be preferred due to position bias - while tie is the objective truth on these labels.
> > > 
> > > 
> > > 


---



* --- discussion numver 38, the number of votes :9 ---

# Prometheus 2 for Evaluating Language Models

**Groz** *Tue May 07 2024 04:01:59 GMT+0900 (日本標準時)* (9 votes)

Today, I stumbled upon a GitHub repository that seems tailor-made for this competition. Prometheus 2, available in two sizes, 7B and 8x7B, claims to achieve state-of-the-art results in language model evaluation, Whats really intriguing is its claim that the 7B model outperforms Lama-2 70B and is on par with Mixtral 8x7B.

Unfortunately, I don't have the time to personally verify these claims or participate in the competition. 

Hopfully this comes in handy. Good luck everyone!

Paper: [https://github.com/prometheus-eval/prometheus-eval](https://github.com/prometheus-eval/prometheus-eval)

Offical Implementation [https://github.com/prometheus-eval/prometheus-eval/](https://prometheus-eval.github.io/prometheus-eval/). 



---

 # Comments from other users

> ## Valentin Werner
> 
> Both of the urls you have linked lead to the competition page instead - looking forward to checking out the model!
> 
> 
> 
> > ## GrozTopic Author
> > 
> > Thanks, i adjusted the link accordingly
> > 
> > 
> > 


---

> ## Nicholas Broad
> 
> [https://huggingface.co/prometheus-eval](https://huggingface.co/prometheus-eval)
> 
> 
> 


---



* --- discussion numver 39, the number of votes :8 ---

# [???] Crazy lb 0.707 run in just 1h

**justin1357** *Sun Aug 04 2024 04:34:19 GMT+0900 (日本標準時)* (8 votes)

It's impossible to get this score by modeling, is it leak?



---

 # Comments from other users

> ## heartkilla
> 
> It is either a leak or a huge breakthrough in preference modeling and the guy is one step away from creating GPT-6
> 
> 
> 


---

> ## sayoulala
> 
> I believe it's very likely. My training set loss couldn't even reach that score. As of now, his score has risen to 0.6 again… I hope Kaggle officials can handle this fairly.
> 
> 
> 


---

> ## sayoulala
> 
> This is incredibly hard to accept.I think there might have been a data leak. Kaggle officials should address this issue; otherwise, it wouldn't be fair.   [@sohier](https://www.kaggle.com/sohier) [@addisonhoward](https://www.kaggle.com/addisonhoward)
> 
> 
> 


---

> ## Psi
> 
> very likely a leak given the score, he had short subs for weeks, now revealing the full leak apparently
> 
> 
> 
> > ## NguyenThanhNhan
> > 
> > i felt pretty demotivated now, after burning so much computes for this comp
> > 
> > 
> > 
> > > ## Psi
> > > 
> > > I feel particularly bad because we reported a leak early in this competition which is why the scoring changed.
> > > 
> > > And now the top scores were all very close approaching similar limits, so an exciting finish was ahead of us.
> > > 
> > > And now this… hope Kaggle can find some way to salvage this somehow. [@sohier](https://www.kaggle.com/sohier) [@addisonhoward](https://www.kaggle.com/addisonhoward) 
> > > 
> > > 
> > > 


---

> ## Ashwani
> 
> I honestly hope its not a leak but some brilliant out of the mind solution. Fingers crossed 
> 
> 
> 


---

> ## Anh Pham
> 
> hilarious :D 
> 
> 
> 


---



* --- discussion numver 40, the number of votes :8 ---

# Data Analysis with Chatbot Arena-like Chat Renderer

**AbaoJiang** *Mon May 27 2024 17:00:34 GMT+0900 (日本標準時)* (8 votes)

Hi everyone,

This is the first time I join an NLP competition. I'm so excited because I need to learn everything from scratch! The very first step is to analyze the data. To facilitate model comparison side by side, instead of scrolling up and down to analyze responses from two models, I write a simple static chat renderer with Chatbot Arena-like UI (co-author by ChatGPT). Following is a screenshot of one chat,

[](https://postimg.cc/Tyyhq5RC)

This renderer supports,

Pair comparison between responses from two models.
Markdown rendering powered by [<md-block>](https://md-block.verou.me/).
- e.g., strong and italic fonts, unordered and ordered lists, etc.

Unicode rendering.
- Characters like emojis can be shown.

[](https://postimg.cc/VdffWZ1K)

Also, winner is displayed at the bottom! I hope this can make raw text analysis more handy.

In addition, I also implement the win rate and battle count heatmaps in [the official paper](https://arxiv.org/pdf/2403.04132). We can use this to find frequent model pairs (i.e., battle counts) and which model has the higher win rate (e.g., gpt-4-1106-preview has only 17.42% lose rate).

[](https://postimg.cc/ThswTMDB)

For detailed implementation, please refer to [LMSYS - Detailed EDA](https://www.kaggle.com/code/abaojiang/lmsys-detailed-eda/notebook).

I'll share more analysis and insights during this interesting learning journey. Hope you like it!



---

 # Comments from other users

> ## Hafiz Nouman
> 
> Amazing Improvement keep it up 
> 
> Review my dataset and give some suggestions on it how I can improve my work
> 
> 
> 


---



* --- discussion numver 41, the number of votes :8 ---

# Chatbot Arena's Rules

**steubk** *Thu May 09 2024 14:01:52 GMT+0900 (日本標準時)* (8 votes)

It has been noticed that the train set consists of conversations rather than single prompts and responses. ([https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/500633)](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/500633)).

These are the rules of the chatbot arena ( [https://chat.lmsys.org/](https://chat.lmsys.org/) ) :

- Ask any question to two anonymous models (e.g., ChatGPT, Claude, Llama) and vote for the better one!

- You can chat for multiple turns until you identify a winner.

- Votes won't be counted if model identities are revealed during the conversation.

As a rough approximation, you might think that the last question has a winner while all the previous ones are ties.

Hope this helps!



---

 # Comments from other users

> ## Valentin Werner
> 
> This is highly important because this means that the last prompt and responses are more valuable than the first ones.
> 
> If you are truncating these information, you should truncate the start, not the end!
> 
> 
> 
> > ## Shreshth Sharma
> > 
> > Ideally, the model difference is generated by the prompt asked first and the response generated at the end. But don't you think that the responses generated in between also preserve important information since if a human makes the final selection, he/she will also consider the thinking process of LLM? Since reaching the right answer with unexplainable thinking itself will result in less credibility of the model.
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > Models might be able to learn which prompt and response combination was the one that actually mattered to the user. I can only speak for myself, that I always voted once I was "that response is better", kind of disregarding everything else beforehand
> > > 
> > > 
> > > 


---



* --- discussion numver 42, the number of votes :7 ---

# Time out always

**Rise_Hand** *Wed Jul 31 2024 18:18:40 GMT+0900 (日本標準時)* (7 votes)

why I always met timeout these day with same infer logic



---

 # Comments from other users

> ## Attacker
> 
> People's participation rate rises before the competition closes, and then the server becomes unstable.
> 
> 
> 


---

> ## Cody_Null
> 
> Yep same thing with our solutions
> 
> 
> 


---

> ## JM
> 
> GPUs running hot and slowing down in last few days probably 😅
> 
> 
> 


---

> ## Krupal Patel
> 
> i also facing same problem with LLMs notebooks.
> 
> 
> 


---

> ## justin1357
> 
> Same, a waste of submission times
> 
> 
> 
> > ## justin1357
> > 
> > Each GPU's performance is different, which cause this prob
> > 
> > 
> > 


---

> ## Roschild.Rui
> 
> Hi HAN, our team is also at a loss -> Why was it possible to submit almost identical inference weights and inference logic without any issues a few days ago, but recently there have been constant submission errors? It seems that the imbalance in Kaggle's computational resource load significantly affects the competition submissions.
> 
> 
> 


---

> ## JamshaidSohail
> 
> Guys. My 15 submissions wasted. Are you able to figure it out ? How to get out of it ?
> 
> 
> 


---

> ## hwz13
> 
> 是的，gpu运行时间太长了
> 
> 
> 


---



* --- discussion numver 43, the number of votes :7 ---

# Combine Gemma-2 9b & Llama-3 8b

**G John Rao** *Fri Jul 26 2024 17:50:20 GMT+0900 (日本標準時)* (7 votes)

Hi everyone, 

I have the two highest-scoring LB notebooks together in each device of T4 GPU.

LB: 0.945

[notebook](https://www.kaggle.com/code/jaejohn/lmsys-combine-gemma-2-9b-llama-3-8b)



---

 # Comments from other users

> ## xiaotingting
> 
> The effect is better after integrating the two models, but is there any way to fuse the two models other than directly adding them together?
> 
> 
> 
> > ## G John RaoTopic Author
> > 
> > You can surely explore weighted averaging, stacking, bagging, etc. I am sure it'll improve the predictions. 
> > 
> > 
> > 


---

> ## Akeryu Ryuu
> 
> I tried this and the results weren't that good, lb of 1.15. And with each submission taking about 8~9 hours each, tuning the submission weights to lb is hard so hopefully you have better luck than me.
> 
> 
> 
> > ## Valentin Werner
> > 
> > Results this bad might indicate that you did not align indices properly. You may want to sort by index before ensembling
> > 
> > 
> > 
> > > ## Akeryu Ryuu
> > > 
> > > Thank you for the advice but I don't really believe that's the problem because I was joining the submissions by id before ensembling. 
> > > 
> > > This is the code I used
> > > 
> > > ```
> > > gemma_sub = pd.read_csv("gemma_submission.csv")
> > > llama_sub = pd.read_csv("llama_submission.csv")
> > > 
> > > merged_submission = pd.merge(gemma_sub, llama_sub, on='id', suffixes=("_1", "_2"))
> > > 
> > > merged_submission["winner_model_a"] = (merged_submission["winner_model_a_1"] + merged_submission["winner_model_a_2"])/2
> > > merged_submission["winner_model_b"] = (merged_submission["winner_model_b_1"] + merged_submission["winner_model_b_2"])/2
> > > merged_submission["winner_tie"] = (merged_submission["winner_tie_1"] + merged_submission["winner_tie_2"])/2
> > > 
> > > final_submission = merged_submission[["id", "winner_model_a", "winner_model_b", "winner_tie"]]
> > > 
> > > ```
> > > 
> > > 
> > > 
> > > ## Valentin Werner
> > > 
> > > Did you validate individual performance of these models? Have you maybe mixed up the input format you used for training with another input format? Or maybe you have mixed up the IDs during inference?
> > > 
> > > Mathematically it is EXTREMELY unlike that two models that perform below / at .950 together go to 1.15. In general, to achieve 1.1x your models need to be overconfident in wrong labels.
> > > 
> > > 
> > > 
> > > ## Akeryu Ryuu
> > > 
> > > Thanks to your comment, I decided to double-check my setup. After about half an hour of searching, I discovered that I hadn't loaded the fine-tuned LoRA weights for the Gemma model. It turns out I missed those two lines while copying the code. So, a big thank you for pointing this out.
> > > 
> > > 
> > > 


---

> ## Ravshan Kutkovin
> 
> Can you explain more about Combine Gemma-2 9b & Llama-3 8b?
> 
> 
> 
> > ## G John RaoTopic Author
> > 
> > Another user did a good job explaining everything, here: [https://www.kaggle.com/code/nabojyotipandey/dual-model-inference-gemma2-9b-llama3-8b](https://www.kaggle.com/code/nabojyotipandey/dual-model-inference-gemma2-9b-llama3-8b)
> > 
> > 
> > 


---



* --- discussion numver 44, the number of votes :7 ---

# 7b OOM while 8b works fine, is this strange?

**Cody_Null** *Wed Jun 26 2024 05:48:42 GMT+0900 (日本標準時)* (7 votes)

I am trying to compare the performance of different base models, for example we can compare base mistral 7B model quantized to 8bit and compare this to the llama 3 8B model also quantized to 8bit. I am noticing I get OOM errors for the 7B model (and others) but not the llama3 8b? I understand they can have different architectures with different memory requirements and that their size is not fully dependent on the number of parameters but just to be sure does anyone else find this strange? 



---

 # Comments from other users

> ## Valentin Werner
> 
> It cannot be due to size - Mistral 7b 8 bit takes 6.87 GB,  Llama 3 8B 8 bit takes 7.05 GB (see: [https://huggingface.co/spaces/hf-accelerate/model-memory-usage)](https://huggingface.co/spaces/hf-accelerate/model-memory-usage)). From what I can see they also have the same hidden sizes and dimensions, so embeddings for Mistral should not take more RAM than for Llama
> 
> Are you getting the error while loading? This might be due to kaggle infrastructure. For fair comparisons you should always load from a freshly restarted environment (as torch.cuda.empty_cache has not the same effect from my experience)
> 
> 
> 
> > ## Cody_NullTopic Author
> > 
> > Glad I am not crazy, I will circle back and try it again today just to double check I have not made some silly mistake. I will update this if I find anything.
> > 
> > 
> > 


---

> ## Cody_NullTopic Author
> 
> Just now realized I totally put this in the wrong thread: 
> 
> Update: I have found the reason. The top here causes an OOM error while the bottom works fine.
> 
> `
> 
> BitsAndBytes configuration
> 
> bnb_config =  BitsAndBytesConfig(
> 
>     load_in_8bit=True,
> 
>     bnb_8bit_compute_dtype=torch.float16,
> 
>     bnb_8bit_use_double_quant=False)
> 
> bnb_config = BitsAndBytesConfig(
> 
>     load_in_8bit=True,
> 
>     bnb_8bit_quant_type="nf8",
> 
>     bnb_8bit_use_double_quant=True,
> 
>     bnb_8bit_compute_dtype=torch.bfloat16)
> 
> `
> 
> 
> 
> > ## Valentin Werner
> > 
> > I was wondering lol 
> > 
> > still got 4 upvotes on the other one 😉
> > 
> > 
> > 
> > > ## Cody_NullTopic Author
> > > 
> > > lol as long as it is useful I guess haha figured I might as well let this side be complete. 
> > > 
> > > 
> > > 


---



* --- discussion numver 45, the number of votes :7 ---

# Additional Data Issues to Note

**AbaoJiang** *Wed May 29 2024 01:05:17 GMT+0900 (日本標準時)* (7 votes)

Hi everyone,

After more EDA in my [LMSYS - Detailed EDA](https://www.kaggle.com/code/abaojiang/lmsys-detailed-eda?scriptVersionId=180273328), I find additional data issues to report and discuss with you.

### Not Only null But Also Empty Responses

As pointed out in [this forum](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/502303), we know that there exists null response issue. Here, I want to share another similar issue that responses from models are empty strings. I currently check if there's at least one model response equal to "" during one conversation, and the answer is yes. 

[](https://postimg.cc/75R2GD0h)

As illustrated above, we can observe that,

There exists no samples with None/empty prompts.
There exist 120+ rows with None responses for both A and B.
There exist 30+ rows with empty responses for both A and B.

You can also test strings like space only (e.g., " ", "    "), new line only (e.g., \n), etc.

### Unintentional Mixed Prompts and Responses?

[](https://postimg.cc/F1xDBP2p)

When exploring missing values, we find another interesting chat example shown above. As can be seen, model A gpt-4-0613 responds an empty string, but model B responds normally. Also, the ending of the prompt is the same as the response.

Out of curiosity, we feed the same prompt to Chatbot Arena in two forms,

#### a. Feed this Prompt As Is

[](https://postimg.cc/7fzm9sPK)

#### b. Feed this Prompt without QAs at the End of Prompt

[](https://postimg.cc/qg9pnynr)

As can be seen, model A in the first case might take QA information at the end of the prompt as a response. In the second case, model B provides a similar answer without QA information in the prompt.

So, our questions are

What's the difference between null responses and empty responses?
Is it possible that there exist samples which unintentionally mixes responses into prompts?

Please feel free to share your thoughts on these topics, thanks!



---

 # Comments from other users

> ## dragon zhang
> 
> thanks for sharing.  The score is changing. Is metric changed or test data?
> 
> 
> 
> > ## AbaoJiangTopic Author
> > 
> > Hi, 
> > 
> > There exists data leakage issue, so the solution file is modified and notebooks are re-scored. You can refer to [this forum](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/506137). Hope this helps.
> > 
> > 
> > 


---

> ## Dr. Gopalashivabalasubramanium Chandrashekaran
> 
> Interesting! I was avoiding checking the text data columns because of this. 
> 
> Qualitative response analysis will be tricky. What if the user asked a question the model could not answer such as outside of the regulations that the model is put under? 
> 
> However, since there are 50k+ rows, I would think dropping these null values wouldn't affect training a model too intensely.
> 
> It gives me idea that some type of ensembled model where user prompt is filtered for potential to generate a null response.
> 
> 
> 


---



* --- discussion numver 46, the number of votes :6 ---

# Holy...did I just see a 0.707 on lb?

**Ya Xu** *Sun Aug 04 2024 04:31:59 GMT+0900 (日本標準時)* (6 votes)

And that's his only submission today, which means it's most likely took him less than 2 hours to do the inference. Seems someone just completely broke this competition and did it alone.

Good news: just need 48 hours to see the solution. I can't help my curiosity.



---

 # Comments from other users

> ## Cody_Null
> 
> Yeah super strange, must have found the dataset used in public LB by accident? 
> 
> 
> 
> > ## SeshuRaju 🧘‍♂️
> > 
> > 
> > Similar to [PetFinder Competition](https://www.kaggle.com/c/petfinder-adoption-prediction/discussion/125436) [@cody11null](https://www.kaggle.com/cody11null) - i feel this 1st solution will be treated similar way or discard his solution by Kaggle 
> > 
> > I believe, we only have 50 hours left. Instead of panicking, I'll trust that Kaggle will handle it. It's better to focus on making wise choices and selecting the best two submissions.
> > 
> > 
> > 
> > ## Kamau
> > 
> > 
> > must have found the dataset used in public LB by accident?
> > 
> > My thoughts too. I hope Kaggle addresses this asap
> > 
> > 
> > 


---

> ## SeshuRaju 🧘‍♂️
> 
> is it happen in any other competitions, its my first time seeing the last min leak at end of competition.
> 
> 
> 
> > ## flg
> > 
> > It is last minute if you hide it. Make some early submissions with only part of the leak used to hide your score, then submit full leak shortly before the end. We probably won't know though until Kaggle checks it ..
> > 
> > 
> > 
> > > ## SeshuRaju 🧘‍♂️
> > > 
> > > Make sense Make some early submissions with only part of the leak used to hide your score [@ferdinandlimburg](https://www.kaggle.com/ferdinandlimburg) 
> > > 
> > > 
> > > 


---



* --- discussion numver 47, the number of votes :6 ---

# Notebook timeout problem 

**JamshaidSohail** *Thu Aug 01 2024 21:47:25 GMT+0900 (日本標準時)* (6 votes)

Hi. The notebook which was working extremely fine in the past few days. Now is timing out on submission. Please, it would be nice to fix this. [@sohier](https://www.kaggle.com/sohier) [@paultimothymooney](https://www.kaggle.com/paultimothymooney) 



---

 # Comments from other users

> ## sayoulala
> 
> I have the same problem…
> 
> 
> 
> > ## JamshaidSohailTopic Author
> > 
> > Glad to see the response from no.1 in this competition. The submissions are getting wasted and no new ideas are being able to be tested out :/
> > 
> > 
> > 
> > > ## sayoulala
> > > 
> > > Submit a few more times and it should run successfully. It might be that the Kaggle system is not very stable.
> > > 
> > > 
> > > 
> > > ## Roschild.Rui
> > > 
> > > Tried around 10 times, finally success 1 crazy!
> > > 
> > > 
> > > 
> > > ## JamshaidSohailTopic Author
> > > 
> > > Guys. I am still getting timeouts. Have wasted 15 submissions.
> > > 
> > > 
> > > 


---

> ## Attacker
> 
> These days, kaggle seems to be effectively closed a week before the competition ends…
> 
> 
> 


---



* --- discussion numver 48, the number of votes :6 ---

# How to tokenize prompts and responses efficiently

**irishu** *Sun Jul 28 2024 13:56:19 GMT+0900 (日本標準時)* (6 votes)

# Experiment

I have tried the following three methods so far, and the first has performed the best in LB.

### Methods

tokenize up to the max_tokens by joining strings like prompt + responseA + responseB
allocate one-third of the max_tokens to each sentence and tokenize up to the limit
allocate the number of tokens in the appropriate ratio(ex;1:2:2)

### Conditions

- using Gemma-2 9b 4-bit QLoRA

- max_tokens = 1024

- using only the last prompt and responses 

- 1 epoch using all train data

- referring to the excellent work [[Training] Gemma-2 9b 4-bit QLoRA fine-tuning](https://www.kaggle.com/code/emiz6413/training-gemma-2-9b-4-bit-qlora-fine-tuning)

# Question

### Don't you think there is a more efficient way than the simple method1?

Looking at the distribution of the number of tokens in the prompt and response (only the last one), it appears that around 10% of them contain more than 1024 tokens in total. That is, in some cases, response B may not contain enough information.

### How much would a larger max_tokens improve the score?

I have not been able to test this yet due to computational resources.



---

 # Comments from other users

> ## irishuTopic Author
> 
> I changed max_tokens to 2048 in learning and inference and the score improved.
> 
> Now I am wondering if I should adjust the token length with padding.
> 
> 
> 


---



* --- discussion numver 49, the number of votes :6 ---

# Damn Ties! 

**cm391** *Thu Jul 25 2024 05:02:47 GMT+0900 (日本標準時)* (6 votes)

The labels used in this competition are assigned by a diverse group of annotators and by its very name preference based. We can see from the following two examples the difficulty with correctly predicting a tie can be tricky.

perhaps Morphalumpaliciousness simply isn't long enough??

two sentences too many??

how you guys dealing with this sort of noise? I cannot seem to get better than random for predicting the draws…



---

 # Comments from other users

> ## Hadi Ai
> 
> I wonder if we could tell something about the annotators from their prompts -- and use that in a smaller model just to predict the tie class; then ensemble that with whatever one is doing… Anyway not much time left for exploration in this competition :-)
> 
> 
> 


---

> ## justin1357
> 
> Tie is really hard to predict… As a human, actually I can't tell when it will be tie as well. Everyone's standard is different and this standard will even change as time went by. I prefer to trust model…
> 
> 
> 


---



* --- discussion numver 50, the number of votes :6 ---

# [question]9h time limit 

**Roschild.Rui** *Thu Jul 25 2024 17:26:58 GMT+0900 (日本標準時)* (6 votes)

Will the organizers rerun our submission on the test set, or will we receive a PV score as long as we successfully submit and have an LB score? 

I saw some situations that when the running time was out of 9 hours the notebook was still running and got a lb score



---

 # Comments from other users

> ## Valentin Werner
> 
> Private scores are already calculated during your submission. So if you got a LB score, your submission is fine.
> 
> 
> 


---

> ## Rise_Hand
> 
> Yes, thus we should be very careful to ensemble our models or make any post processing
> 
> 
> 


---



* --- discussion numver 51, the number of votes :6 ---

# CUDA OOM when ensemble Gemma2 and Llama3

**Lorry Zou** *Tue Jul 16 2024 00:39:47 GMT+0900 (日本標準時)* (6 votes)

Hi everyone, I'm trying to ensemble gemma2 and llama3. My strategy is load data -> load gemma2 model -> gemma2 inference -> load llama3 model -> llama3 inference -> ensemble. I use T4*2 and my code is mainly based on [@kishanvavdara](https://www.kaggle.com/kishanvavdara) 's inference notebook.

My issue is: When I try to load llama3 model after gemma2 inference, I encounter CUDA OOM. I try to clear memory by removing gemmas from the two GPUs (I load one gemma model on each GPU) using gemma_model.cpu(); del gemma_model; torch.cuda.empty_cache(), but it doesn't help. Only GPU 0 is freed and GPU 1 is still using 8.9GB memory. 

Is there any way to release all the memory from both GPUs? Or perhaps reduce of size of the models?



---

 # Comments from other users

> ## no fit just luck
> 
> I would like to share a simple method. You can use '%%writefile' to create a '.py' file and then run this file by "!python file_name.py" to generate your submission. Specifically, you can create two py files for gemma and llama. In each of the file, you can save the model output as a csv file. At last, you can load them and do your ensemble. 
> 
> The key point is that by using  "!python file_name.py", the memory will be clean. Hope this can solve your problem.
> 
> 
> 
> > ## Lorry ZouTopic Author
> > 
> > Yeah I just converted the whole notebook to python script and it works well with releasing memory. I didn't know we can even directly submit a python script LOL.
> > 
> > 
> > 


---

> ## Priyanshu Joshi
> 
> Make sure you are correctly clearing all references to the model and intermediate tensors.
> 
> ```
> import gc
> 
> gemma_model.cpu()
> del gemma_model
> torch.cuda.empty_cache()
> gc.collect()
> 
> ```
> 
> Ensure your inference environment has no other processes using the GPUs. Sometimes background processes can consume significant memory. Use gradient checkpointing to trade computational cost for memory usage. This saves memory by recomputing some parts of the model during the backward pass. Experiment with batch size and max_length as Veletin mentioned in his comment. You can try [model parallelism](https://huggingface.co/docs/transformers/v4.15.0/parallelism).
> 
> 
> 


---

> ## Lorry ZouTopic Author
> 
> I'm wondering why only GPU 0's memory can be released after inference. Maybe only one of the model is actually used during inference? The code:
> 
> `@torch.no_grad()
> 
> [@torch.cuda.amp.autocast](https://www.kaggle.com/torch.cuda.amp.autocast)()
> 
> def gemma_inference(df, model, device, batch_size=cfg.batch_size, max_length=cfg.max_length):
> 
>     a_win, b_win, tie = [], [], []
> 
> ```
> for start_idx in range(0, len(df), batch_size):
>     end_idx = min(start_idx + batch_size, len(df))
>     tmp = df.iloc[start_idx:end_idx]
>     input_ids = tmp["input_ids"].to_list()
>     attention_mask = tmp["attention_mask"].to_list()
>     inputs = pad_without_fast_tokenizer_warning(
>         gemma_tokenizer,
>         {"input_ids": input_ids, "attention_mask": attention_mask},
>         padding=True,
>         max_length=max_length,
>         pad_to_multiple_of=None,
>         return_tensors="pt",
>     )
>     outputs = model(**inputs.to(device))
>     proba = outputs.logits.softmax(-1).cpu()
> 
>     a_win.extend(proba[:, 0].tolist())
>     b_win.extend(proba[:, 1].tolist())
>     tie.extend(proba[:, 2].tolist())
> 
>     df["winner_model_a"] = a_win
>     df["winner_model_b"] = b_win
>     df["winner_tie"] = tie
>     return df` and
> 
> ```
> 
> with ThreadPoolExecutor(max_workers=2) as executor:
>     gemma_results = executor.map(gemma_inference, (gemma_sub_1, gemma_sub_2), (gemma_model_0, gemma_model_1), (device_0, device_1))
> 
> I also tried batch_size=4 and 2, there's no difference.
> 
> 
> 
> > ## Valentin Werner
> > 
> > are you actually using gc.collect() - i had it before where it wouldnt be released until gc.collect() was done. exatly like ShelterW described in their comment.
> > 
> > 
> > 
> > > ## Lorry ZouTopic Author
> > > 
> > > Yes I'm suing gc.collect(), but it doesn't work: 
> > > 
> > > gemma_model_0.to('cpu')
> > > del gemma_model_0
> > > gc.collect()
> > > gemma_model_1.to('cpu')
> > > del gemma_model_1
> > > gc.collect()
> > > with torch.no_grad():
> > >     torch.cuda.set_device('cuda:0')
> > >     torch.cuda.empty_cache()
> > >     torch.cuda.set_device('cuda:1')
> > >     torch.cuda.empty_cache()
> > > 
> > > 
> > > 


---

> ## ShelterW
> 
> When I used the Gemma2 and Llama3 ensemble, it was even worse.
> 
> ```
> import torch
> import gc
> del proba, model_0, model_1, test, data, aug_data
> gc.collect()
> torch.cuda.empty_cache()
> 
> ```
> 
> 
> 
> > ## Lorry ZouTopic Author
> > 
> > I believe there's something remaining in the memory and we forgot to delete it…😆
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > This gets both GPUs down to below 300 MB. Else turn down max_length and / or batch size
> > > 
> > > 
> > > 
> > ## Allen Wang
> > 
> > Yes, I have the same problem as you. Is there any way to solve it
> > 
> > 
> > 


---



* --- discussion numver 52, the number of votes :6 ---

# Why LLAMA3 dominates the leaderboards, not deberta.

**kagglethebest** *Fri Jul 05 2024 22:41:58 GMT+0900 (日本標準時)* (6 votes)

When I looked at the public notebook, I was surprised to find that LLAMA3 had the highest score, not Deberta. I have the impression that there are competitions about text classification tasks (let's say this competition is also text classification tasks), and basically Deberta is the optimal solution, at least not by a large margin.

I think there could be two reasons for this:

We haven't found a more suitable categorical loss function for deberta.
Decoder Only models such as LLAMA are more sensitive to the text output by LLMs.

ps: Please let me know if anyone uses Deberta to exceed the score of the best LLAMA notebook.



---

 # Comments from other users

> ## Valentin Werner
> 
> I think your second reason definetly applies. But you should also acknowledge that Llama3-8B has 20x amount of parameters compared to DeBERTa and was pre-trained accordingly. It will be able to represent language much better. Simply adding an classification head will make up the difference between encoding and decoding.
> 
> If I am not mistaken, the architectural differences between encoder-only (DeBERTa) and decoder-only (LLama) for seq classification are marginal, as the decoder are no longer in need to generate the next tokens auto-regressively and instead will generate the classification, just like encoders do.
> 
> Often, the amount of parameters only makes a small difference towards a better score, however, as this problem his very nuanced (even a human could not predict the dataset very well), the sheer amount of parameters helps learning these nuances. This problem is simply too complex for DeBERTa, in my opinion.
> 
> 
> 
> > ## Cristóbal Mackenzie
> > 
> > This makes sense, since I gave a couple of shots using TinyLlama and absolutely failed. Amount of parameters seems to be key for learning anything at all in this problem.
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > I heard some people had some success with Deberta XS regarding "anything at all". But my best DeBERTa (Large) got barely below 1.0, which already included some secret sauce
> > > 
> > > 
> > > 
> > > ## justin1357
> > > 
> > > Could llama be much better?
> > > 
> > > 
> > > 


---



* --- discussion numver 53, the number of votes :6 ---

# submissions get timeout?

**yechenzhi1** *Sun May 19 2024 11:28:12 GMT+0900 (日本標準時)* (6 votes)

Hi, I'm new to kaggle. I've submitted several times, all all my submissions failed due to timeout, but when I run it in my local Kaggle environment with T4*2 the inference time is as follows:

And I got a warning like this:

2024-05-19 01:36:52.192095: E external/local_xla/xla/stream_executor/cuda/cuda_dnn.cc:9261] Unable to register cuDNN factory: Attempting to register factory for plugin cuDNN when one has already been registered

  2024-05-19 01:36:52.192192: E external/local_xla/xla/stream_executor/cuda/cuda_fft.cc:607] Unable to register cuFFT factory: Attempting to register factory for plugin cuFFT when one has already been registered

  2024-05-19 01:36:52.309490: E external/local_xla/xla/stream_executor/cuda/cuda_blas.cc:1515] Unable to register cuBLAS factory: Attempting to register factory for plugin cuBLAS when one has already been registered

But I'm sure GPU is used during the inference.

Any help would be appreciated. 



---

 # Comments from other users

> ## yechenzhi1Topic Author
> 
> thanks everyone helped! Setting batch size=1 solved my problem😃
> 
> 
> 


---

> ## yechenzhi1Topic Author
> 
> Another question is that, when we score in the public leaderboard, is the test dataset about 25000 * 0.3 rows? And when tested in the private leaderboard, it's about 25000 * 0.7 rows?
> 
> 
> 
> > ## Kishan Vavdara
> > 
> > Yes, that's correct! 
> > 
> > 
> > 
> > ## Rich Olson
> > 
> > I'll add that assuming this is like most contests - you're notebook is always run for the entire private / public test set.  It's just the scores for the private data portion of the scores is revealed at the end of the contest.
> > 
> > 
> > 


---

> ## lijiang3859
> 
> Hey, [@yechenzhi1](https://www.kaggle.com/yechenzhi1). Thanks for your sharing! I also got this warning:
> 
> ```
>   warnings.warn(
> 2024-07-06 05:05:32.818151: E external/local_xla/xla/stream_executor/cuda/cuda_dnn.cc:9261] Unable to register cuDNN factory: Attempting to register factory for plugin cuDNN when one has already been registered
> 2024-07-06 05:05:32.818272: E external/local_xla/xla/stream_executor/cuda/cuda_fft.cc:607] Unable to register cuFFT factory: Attempting to register factory for plugin cuFFT when one has already been registered
> 2024-07-06 05:05:32.956771: E external/local_xla/xla/stream_executor/cuda/cuda_blas.cc:1515] Unable to register cuBLAS factory: Attempting to register factory for plugin cuBLAS when one has already been registered
> 
> ```
> 
> However, my program does not raise bugs. Is there any influence on it?  By setting batch_size=1, the warning is gone?
> 
> 
> 
> > ## yechenzhi1Topic Author
> > 
> > We can ignore this warning.
> > 
> > 
> > 


---

> ## lijiang3859
> 
> I think I also have the same issue with model=llama3-8B. Here is my script:
> 
> ```
> results = []
> df = pd.read_csv(args.test_file, dtype={'prompt': str, "response_a":str, "response_b":str})
> df.fillna("''", inplace=True)
> df.replace('null', "'null'", inplace=True)
> 
> eval_dataset = Dataset.from_pandas(df)
> length =  len(eval_dataset)
> for i in tqdm(range(length)): # batch_size = 1
>     data = eval_dataset[i]
>     idx = data["id"]
>     resp_a = template.format(data['prompt'], data['response_a'])
>     resp_b = template.format(data['prompt'], data['response_b'])
>     resp_tokens = tokenizer(
>         [resp_a, resp_b],
>         max_length=args.max_total_length,
>         padding=True,
>         truncation=True,
>         return_tensors="pt",
>     )
>     # concated responses to save inference time -> batch_size =2
>     output = model(resp_tokens)
> 
> ```
> 
> Here is some other settings to speed up the inference process:
> 
> use bf116=True for model initialization.
> use autocast() and
> 
> Is there any other process to speed up the inference? I have tested it with 25000 samples, it is very risky to excel the total training budget with 9hrs.
> 
> 
> 
> > ## yechenzhi1Topic Author
> > 
> > [https://www.kaggle.com/code/emiz6413/llama-3-8b-38-faster-inference](https://www.kaggle.com/code/emiz6413/llama-3-8b-38-faster-inference)  you can check this notebook to see if it can help.
> > 
> > 
> > 


---

> ## Valentin Werner
> 
> One Remark, the test data has 25000 samples, so this will 10x your runtime. Technically that is still less than 540 minutes, but it is a lot slower
> 
> 
> 
> > ## yechenzhi1Topic Author
> > 
> > yes, so the prediction time should be 40x10 minutes, that's about 7 hours,  so it shouldn't be timeout.
> > 
> > 
> > 


---

> ## Rich Olson
> 
> how many rows are you testing prediction with?
> 
> (when you score - it scores against 25,000)
> 
> 
> 
> > ## yechenzhi1Topic Author
> > 
> > I tested 2500 rows, it was about 40 minutes.
> > 
> > 
> > 
> > > ## Rich Olson
> > > 
> > > well - I can't think of anything obvious.  just assuming you aren't doing anything that takes a bunch of time before inference? (training / pre-processing / generating embeddings)?
> > > 
> > > if you run out of ideas - I would try to test the workflow as close as possible to submission.
> > > 
> > > I would load 25k rows from "train" into your "test" dataframe (and drop columns / etc to make it look like test).
> > > 
> > > Then - I would save a version of your notebook.  That will run it like it was getting submitted.
> > > 
> > > You should then be able to look at the logs (even if it times out before finishing).
> > > 
> > > Might want to try adding some logging / debug statements before doing.
> > > 
> > > 
> > > 


---



* --- discussion numver 54, the number of votes :6 ---

# is 'Both are bad' = 'Tie' ? 

**waechter** *Fri May 17 2024 02:38:26 GMT+0900 (日本標準時)* (6 votes)

Hello, 

In [https://chat.lmsys.org/](https://chat.lmsys.org/) (data source) there is 4options :

👈 A is better
👉 B is better
🤝 Tie
👎 Both are bad

Since we only have 3options, I'm wondering if 'Both are bad' is a Tie,  or if these are filtered out

Thanks !



---

 # Comments from other users

> ## Addison Howard
> 
> "Both are Bad" and "Tie" have been merged in this competition.
> 
> 
> 


---



* --- discussion numver 55, the number of votes :6 ---

# DeBERTa is not learning patterns?

**Valentin Werner** *Mon May 06 2024 18:08:22 GMT+0900 (日本標準時)* (6 votes)

Hello everybody - I am currently facing the issue that my starter notebook always predicts label 0 (which is most prevalent in the subset of the dataset that I am using).

I did not have this experience in the past, where even though labels are balanced, the model is not learning.

Did you experience the same and were you able to solve it?



---

 # Comments from other users

> ## Rich Olson
> 
> I had the same experience with deberta:
> 
> [https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/501848](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/501848)
> 
> Short version: Things didn't converge for me until I started training with more data.  
> 
> Definitely had that "huh - this isn't work" feeling training on a small subset.  Got LB 1.030 after training on all the data.
> 
> Notebook here:
> 
> [https://www.kaggle.com/code/richolson/deberta](https://www.kaggle.com/code/richolson/deberta) (copy and paste as you please)
> 
> 
> 
> > ## Valentin WernerTopic Author
> > 
> > Interesting! 1.030 is definetly an improvement, did you also evaluate accuracy? wondering whether it is still in the 30s/40s..
> > 
> > 
> > 
> > > ## Rich Olson
> > > 
> > > Well - my validation on 20% of train is:
> > > 
> > > Log Loss: 1.0217662463425792
> > > 
> > > Accuracy: 0.48329853862212946
> > > 
> > > Considering my LB score is a little lower - I'd guess mid 40s at best.
> > > 
> > > Since the amount of train data seems to be a factor - wondering if tossing a bunch more train at it might help. (there are some datasets…)
> > > 
> > > Considering run-time is about 3 hours - could maybe double the train data.  I haven't really looked at if I can do anything to speed things up yet though.
> > > 
> > > 
> > > 
> > > ## Gaurav Rawat
> > > 
> > > Nice how do the loss curves look they seems to be like fluctuating with no end . Also the accuracy you got at what step earlier or later epochs . As I see that also fluctuates 
> > > 
> > > 
> > > 
> > > ## Rich Olson
> > > 
> > > so - in another notebook that uses deberta - I've gone up to 1000 LGBM iterators - and it still seems like loss is slowly falling… (and LB score improving…)
> > > 
> > > [https://www.kaggle.com/code/richolson/deberta-tf-idf-word2vec-length](https://www.kaggle.com/code/richolson/deberta-tf-idf-word2vec-length) (LB 1.011 on last run)
> > > 
> > > I've added tf-idf, word2vec and length features in that one - so hard to say what's going on…  taking it as a suggestion I may need to use something more than LGBM to fully use the deberta embeddings…
> > > 
> > > 
> > > 


---

> ## Huang Jing Stark
> 
> Facing same issue here, my eval_loss is not decreasing 
> 
> 
> 


---

> ## Valentin WernerTopic Author
> 
> Code in case you care
> 
> Config:
> 
> ```
> class CFG:
>     model = "microsoft/deberta-v3-small"
>     add_tokens = ["<[PROMPT]>","<[RESP_A]>","<[RESP_B]>","<[...]>","\n"]
>     output_dir="."
>     learning_rate=2e-5
>     per_device_train_batch_size=2
>     per_device_eval_batch_size=2
>     num_train_epochs=2
>     weight_decay=0.01
>     evaluation_strategy="epoch"
>     save_strategy="epoch"
>     max_length=2048
>     warmup_ratio=0.1
>     fp16=True
> 
> ```
> 
> Tokenizer (note that I also tried without new tokens and got same result)
> 
> ```
> # Prepare Tokenizer
> tokenizer = AutoTokenizer.from_pretrained(CFG.model)
> 
> new_tokens = set(CFG.add_tokens) - set(tokenizer.vocab.keys())
> tokenizer.add_tokens(list(new_tokens))
> 
> def tokenize(examples):
>     """use with huggingface datasets"""
>     return tokenizer(
>         examples["train_input"], 
>         truncation=True,
>         max_length=CFG.max_length
>     )
> 
> data_collator = DataCollatorWithPadding(tokenizer=tokenizer)
> 
> [... dataset preparation ...]
> 
> ```
> 
> Model loading (note that I also tried without num_labels and got same result):
> 
> ```
> # Initialize model
> model = AutoModelForSequenceClassification.from_pretrained(
>     CFG.model,
>     num_labels=3
> )
> model.resize_token_embeddings(len(tokenizer))
> 
> ```
> 
> Metric used:
> 
> ```
> accuracy = evaluate.load("accuracy")
> 
> def compute_metrics(eval_pred):
>     predictions, labels = eval_pred
>     predictions = np.argmax(predictions, axis=1)
>     return accuracy.compute(predictions=predictions, references=labels)
> 
> ```
> 
> Training:
> 
> ```
> training_args = TrainingArguments(
>     output_dir=CFG.output_dir,
>     learning_rate=CFG.learning_rate,
>     per_device_train_batch_size=CFG.per_device_train_batch_size,
>     per_device_eval_batch_size=CFG.per_device_eval_batch_size,
>     num_train_epochs=CFG.num_train_epochs,
>     weight_decay=CFG.weight_decay,
>     evaluation_strategy=CFG.evaluation_strategy,
>     save_strategy=CFG.save_strategy,
>     fp16=CFG.fp16
> )
> 
> trainer = Trainer(
>     model=model,
>     args=training_args,
>     train_dataset=ds["train"],
>     eval_dataset=ds["test"],
>     tokenizer=tokenizer,
>     data_collator=data_collator,
>     compute_metrics=compute_metrics,
> )
> 
> trainer.train()
> 
> ```
> 
> 
> 
> > ## Ho Dinh Trieu
> > 
> > hi [@valentinwerner](https://www.kaggle.com/valentinwerner),does the train takes long? 
> > 
> > 
> > 
> > > ## Valentin WernerTopic Author
> > > 
> > > No, I sample 10% of the training data and only train 2 epochs. Takes about 35 min on kaggle GPU.
> > > 
> > > I also noticed that other notebooks have the same issue.
> > > 
> > > 
> > > 
> > > ## Gaurav Rawat
> > > 
> > > What was the best loss you got from the baseline not getting it past 1 right now and seems not converging at this moment for me . 😀 
> > > 
> > > 
> > > 
> > > ## Valentin WernerTopic Author
> > > 
> > > Same for me, I also tried rephrasing the task but cannot make it lear at all.
> > > 
> > > Loss is stuck at 1.07 or so; which is what you get when you just predict the distribution
> > > 
> > > 
> > > 


---



* --- discussion numver 56, the number of votes :6 ---

# Predictive Human Preference: From Model Ranking to Model Routing (Idea for build a baseline)

**KhanhVD** *Fri May 03 2024 17:28:13 GMT+0900 (日本標準時)* (6 votes)

This is [cool blog](https://huyenchip.com/2024/02/28/predictive-human-preference.html) from Chip Huyen about Predictive Human Preference I think it can help for this competition and give some idea to build baseline model

# Bradley-Terry algorithm

Given a history of match outcomes, the Bradley-Terry algorithm finds the model scores that maximize the likelihood of these match outcomes, turning model scoring into a maximum likelihood estimation problem. The input, for each training example, is the models that participate in the match. The output is the outcome of the match. Assuming there’s no draw, the outcome of a match is either 0 (a wins) or 1 (b wins).

[https://huyenchip.com/assets/pics/predictive-preference/3-bradley-terry.png](https://huyenchip.com/assets/pics/predictive-preference/3-bradley-terry.png)

# Predicting Human Preference For Each Prompt

If a ranking algorithm is about figuring out which model is better overall, predictive human preference is about figuring out which model is better for each prompt. If we know in advance that for a particular prompt, GPT-3.5 works just as well as GPT-4, and GPT-3.5 is cheaper, we can route that prompt to GPT-3.5 instead. Or if we know that Mistral-7B works just as well as GPT-4 and Mistral-7B is faster, we can route our query to Mistral-7B instead.

## Experiment setup

We can treat predictive human preference as a binary classification task. Given a match between 2 models, predict which one wins. If the probability of model_a winning is around 0.5, it can be considered a tie. If a Bradley-Terry model takes only (model_a, model_b) as the input, a preference predictor takes (prompt, model_a, model_b) as the input.

[https://huyenchip.com/assets/pics/predictive-preference/4-preference-predictor.png](https://huyenchip.com/assets/pics/predictive-preference/4-preference-predictor.png)

The architecture of my preference predictor looks like this. The model encoder and preference predictor are neural networks that can be trained independently or together. We can use BERT, Roberta, Deberta,.. or other encoder model as my prompt encoder.

[imagehttps://huyenchip.com/assets/pics/predictive-preference/5-predictive-preference-architecture.png](https://huyenchip.com/assets/pics/predictive-preference/5-predictive-preference-architecture.png)





* --- discussion numver 57, the number of votes :5 ---

# Llama 3.1 7b vs Gemma 9b (sft)?

**SeshuRaju 🧘‍♂️** *Sun Jul 28 2024 02:44:32 GMT+0900 (日本標準時)* (5 votes)

Local cv for Gemma is better than Llama 3.1 -> is it same for you too?

- same settings as sft, qlora, 4bit, same batch size.

Gemma 9b:  

  Step 10: loss = 2.3923

  Step 20: loss = 2.0361

  Step 30: loss = 1.4534

  Step 40: loss = 1.6852

  Step 50: loss = 1.3092

LLama 3.1 7b:

  Step 10: loss = 2.6542

  Step 20: loss = 3.2993

  Step 30: loss = 2.4278

  Step 40: loss = 2.0152

  Step 50: loss = 2.3515



---

 # Comments from other users

> ## Helmut12
> 
> By looking through the Code page, I think Gemma should be better for this competition.
> 
> 
> 


---

> ## sayoulala
> 
> The training loss alone is not enough to determine which is not performing well.
> 
> 
> 


---

> ## Ashwani
> 
> In my limited experiments, gemma9b is performing better than llama3.1 and llama3. 
> 
> Both llama3.1 & llama3 are giving similar performance with llama3.1 marginally better. 
> 
> 
> 
> > ## Merlyn Wang
> > 
> > Same here.
> > 
> > 
> > 


---

> ## CPMP
> 
> This is train loss or validation loss?
> 
> 
> 
> > ## SeshuRaju 🧘‍♂️Topic Author
> > 
> > it's training loss in the post [@cpmpml](https://www.kaggle.com/cpmpml) 
> > 
> > validation loss per epoch wise.
> > 
> >   for local cv - Llama 3.1 - 1.097 and Gemma - 0.981
> > 
> > 
> > 
> > > ## CPMP
> > > 
> > > 1.09 is a model that did not learn. Something is wrong here IMHO.
> > > 
> > > 
> > > 


---



* --- discussion numver 58, the number of votes :5 ---

# CV vs LB，Will there be significant fluctuations？

**sayoulala** *Sun Jul 14 2024 12:02:54 GMT+0900 (日本標準時)* (5 votes)

Hello everyone, what do you think about the trends of CV (Cross-Validation) and LB (Leaderboard) in this competition's challenge? Will there be significant fluctuations, similar to recent competitions?



---

 # Comments from other users

> ## Valentin Werner
> 
> The obligatory post towards the end of each competition. 
> 
> I cannot really answer your question, but I can say that we definetly managed to overfit models on CV before. However, in a lot of cases we have pretty good LB and CV correlation. This is something I often did not have in competitions with large shakeup.
> 
> 
> 
> > ## sayoulalaTopic Author
> > 
> > Then you probably haven't participated in the competitions hosted by THE LEARNING AGENCY LAB on Kaggle, haha."
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > DAIGT was wild, but I do not recall people feeling good about their CV - LB correlation in it. 
> > > 
> > > After a quick search, I found this, which agrees with what I remember [https://www.kaggle.com/competitions/llm-detect-ai-generated-text/discussion/458477](https://www.kaggle.com/competitions/llm-detect-ai-generated-text/discussion/458477)
> > > 
> > > But I also remember this gem which aged like fine milk: [https://www.kaggle.com/competitions/llm-detect-ai-generated-text/discussion/462235](https://www.kaggle.com/competitions/llm-detect-ai-generated-text/discussion/462235)
> > > 
> > > 
> > > 


---

> ## xiaotingting
> 
> It depends on the difference in the distribution of the training set and the test set. I can only say that there may be a big difference between the leaderboard score and the cross-validation score.
> 
> 
> 


---

> ## Dlond Mike
> 
> don't worry my friend,u are the first in LB:)
> 
> 
> 


---



* --- discussion numver 59, the number of votes :5 ---

# Request for Kaggle Llama 3 access under review for over 6 days [Solved]

**Allie K.** *Mon Jul 08 2024 20:18:16 GMT+0900 (日本標準時)* (5 votes)

On Friday early morning MDT I submitted request for Llama 3 and Llama 2 access first via Meta website (of course with the same email address as I have on Kaggle) and I was granted the access in a minute.

Immediately I successfully submitted request to access Llama 3 model via Kaggle. 

Now, after more than 6 days, the request is still "pending a review from the authors".

As it can be seen from the discussion under the model, I am not alone in this desperate situation.

[@addisonhoward](https://www.kaggle.com/addisonhoward) is the access to the model on Kaggle somehow restricted? 

In this case all the competition wouldn't be fair at all. It isn't fair even now, because I couldn't make submission with Llama 3 for 3 days due to problems on Kaggle side.  

Edited:

And suddenly, after "only" 6 days a magic happened and the access is granted.

The magic seems to be triggered by another discussion thread.



---

 # Comments from other users

> ## CPMP
> 
> Reading this only now. It is wrong that your post did not have effect until mine. 
> 
> 
> 


---

> ## RB
> 
> I downloaded Transformer weights for Gemma (since they are not [yet available on Kaggle](https://www.kaggle.com/models/google/gemma-2/discussion/516164)) You can do the same for Llama as well 
> 
> Following code will save weights in /kaggle/working directory of your kernel. You do need read access token from Huggingface and your request must be approved there.
> 
> Typically I found process is much faster when the models are released, so apply even if you are not planning to use it. 
> 
> ```
> import os
> os.environ["HF_HUB_ENABLE_HF_TRANSFER"] = "1"
> 
> from kaggle_secrets import UserSecretsClient
> user_secrets = UserSecretsClient()
> secret_value_0 = user_secrets.get_secret("HF_TOKEN")
> 
> from huggingface_hub import  snapshot_download, login
> login(token=secret_value_0, add_to_git_credential=False)
> 
> ## Download model from HuggingfaceHub
> ## https://huggingface.co/google/gemma-2-9b-it/tree/main
> 
> snapshot_download(repo_id="google/gemma-2-9b-it", 
>                   revision="main", 
>                   repo_type="model",
>                   allow_patterns="*",
>                   local_dir = "/kaggle/working/", 
>                   ignore_patterns="consolidated.safetensors")
> 
> ```
> 
> 
> 
> > ## BladeRunner
> > 
> > This approach seems to only support models with weight files under 20GB, because of the capacity cap of /kaggle/working/, I wonder how it should be handled for models 13b and above?😀
> > 
> > 
> > 
> > > ## RB
> > > 
> > > You can download in /tmp directory - I think there's 50+ GB space available there. 
> > > 
> > > From /tmp you can upload to a Kaggle Dataset with [Kaggle API  ](https://github.com/Kaggle/kaggle-api/blob/main/docs/README.md#datasets)
> > > 
> > > 
> > > 


---

> ## sayoulala
> 
> [https://www.kaggle.com/datasets/junglebeastds/llama3instruct](https://www.kaggle.com/datasets/junglebeastds/llama3instruct) .Someone upload the model here
> 
> 
> 


---

> ## Allie K.Topic Author
> 
> Big thanks to everybody who suggested me (and hopefully not only to me) a solution how to solve the unpleasant situation. I could start submitting.
> 
> Anyway I hope that Kaggle team will restore the broken Llama 3 access pipeline in a reasonable time, not only after the competition ends. 
> 
> 
> 


---

> ## Pamin
> 
> Same, 3 days ago.
> 
> 
> 


---

> ## hn
> 
> Same here actually. 
> 
> 
> 


---

> ## Valentin Werner
> 
> This is wild, it has been approved for me within 10 minutes on a weekend
> 
> 
> 


---

> ## Xinyuan Qiao
> 
> Just do it again, I got same situation before.
> 
> 
> 


---

> ## Arindam Roy
> 
> Same here 
> 
> 
> 


---

> ## samson
> 
> You can get an access via [meta's webpage](https://llama.meta.com/) or directly on [huggingface](https://huggingface.co/meta-llama/Meta-Llama-3-8B), then download the weights and upload all the stuff as a private dataset on Kaggle. Its much faster! Basically minutes (I have submitted a request for model access via Kaggle 4 days ago and still waiting)
> 
> 
> 


---



* --- discussion numver 60, the number of votes :5 ---

# Facing "CUDA out of memory" error during fine-tuning Llama3 model

**Tabassum_Nova** *Fri May 31 2024 18:06:44 GMT+0900 (日本標準時)* (5 votes)

I tried to fine-tune Llama3 model inspired by [fine-tune-llama-3-for-sentiment-analysis](https://www.kaggle.com/code/lucamassaron/fine-tune-llama-3-for-sentiment-analysis) notebook. But I was facing the following error:

torch.cuda.OutOfMemoryError: CUDA out of memory. Tried to allocate 224.00 MiB. GPU 0 has a total capacty of 14.75 GiB of which 11.06 MiB is free. Process 3258 has 14.73 GiB memory in use. Of the allocated memory 14.04 GiB is allocated by PyTorch, and 509.85 MiB is reserved by PyTorch but unallocated. If reserved but unallocated memory is large try setting max_split_size_mb to avoid fragmentation.  See documentation for Memory Management and PYTORCH_CUDA_ALLOC_CONF

I have already followed the solution suggested in [this discussion](https://www.kaggle.com/discussions/getting-started/140636). But these did not help. This is the link of [my notebook](https://www.kaggle.com/code/tabassumnova/lmsys-fine-tuning-llama3-8b/notebook)

Can anyone please suggest what I should do to avoid this error?



---

 # Comments from other users

> ## Ivan Vybornov
> 
> Enable gradient_checkpointing and use paged_adamw_8bit instead of a 32bit version. If does not work, try applying lora to less target_modules, for instance finetuning just ["q_proj", "k_proj", "v_proj", "o_proj"] ain't bad.
> 
> 
> 
> > ## Tabassum_NovaTopic Author
> > 
> > Thank you. Enabling gradient _checkpointing works. Training has started 😁
> > 
> > 
> > 


---

> ## Valentin Werner
> 
> If you are not using it already, use batch size 1. Maybe use T4 x2 
> 
> in general, kaggle GPU might be too slow for the amount and length of training data
> 
> 
> 
> > ## Tabassum_NovaTopic Author
> > 
> > I solved the issue. But it’s taking a long time to train. I am using Kaggle GPU T4x2. Could you please suggest any other option to train the model other than kaggle notebook? I don’t have any personal GPU
> > 
> > 
> > 
> > > ## Kishan Vavdara
> > > 
> > > There are many options , you can rent A100, Rtx4090 or any other GPU instances at [Vastai](https://vast.ai/),  [Runpod](https://www.runpod.io/), or other cloud host platforms,  train your model and then delete the instance. You can also start google cloud free trial, it will give you 300$ credits for 3 months. I think colab pro also gives access to A100 and V100 Gpu's. Personally, I found vastai to be more convenient and cheap. 
> > > 
> > > 
> > > 
> > > ## Tabassum_NovaTopic Author
> > > 
> > > Thank you for your suggestions
> > > 
> > > 
> > > 
> > > ## lijiang3859
> > > 
> > > I trained offline in my server, but it still requires memory. How can I solve it? 
> > > 
> > > If I submit this to notenotebook in the system, will the code still run on the same device I am using for inference? (so sad)
> > > 
> > > 
> > > 


---

> ## Kishan Vavdara
> 
> Try reducing LoRA config 'rank', it will reduce trainable params, in your notebook i see you're using 64 rank, try 4, 8, or 16.  And you can also try reducing max_length. 
> 
> 
> 
> > ## Tabassum_NovaTopic Author
> > 
> > I tried with rank 4, max_seq_length = 512; Still getting the same error
> > 
> > 
> > 


---

> ## kartikey bartwal
> 
> Are you doing your work on some other platform other thank kaggle notebooks or google colab ? I don't think such problem should've arrived with their TPU's
> 
> 
> 
> > ## Tabassum_NovaTopic Author
> > 
> > The training issue is solved. But it’s training too slowly. I have not tried with TPU. Could you please suggest any solution too solve this training speed?
> > 
> > 
> > 
> > > ## Tabassum_NovaTopic Author
> > > 
> > > Yeah I understand 
> > > 
> > > 
> > > 


---



* --- discussion numver 61, the number of votes :5 ---

# Can I win only using Kaggle resources?

**Areej Malkawi** *Mon Jun 10 2024 03:35:55 GMT+0900 (日本標準時)* (5 votes)

The data of this competition are huge, I saw many public notebooks that used some pre-trained models for inference and I tried to use a pre-trained model to train the given competition data but I'm facing memory\score trade-off, am I supposed to use something more than Kaggle GPU\ TPU quota to overcome memory issues? as well as getting high LB score?

can I win or be at the top of LB without using external resources?



---

 # Comments from other users

> ## Ebi
> 
> 
> can I win or be at the top of LB without using external resources?
> 
> I think it's almost impossible. And this applies to most Kaggle competitions, because in most cases, you need to do a lot of experiment cycles.  
> 
> In fact, I've been participating for about three years using a CPU-only laptop and a cheap cloud service like Colab, but I've only managed to get a silver medal. I bought an RTX 4090 a few months ago and was able to get a gold medal right away, which gives me an advantage in this competition too.  
> 
> 
> 
> > ## Hassan Abedi
> > 
> > Yeah, for most NLP competitions, having a good GPU with lots of VRAM makes a big difference. 
> > 
> > 
> > 
> > ## Valentin Werner
> > 
> > Note that renting a GPU starts (in Germany) around 50 cent / hour - let's say a training takes 8 hours, thats 4€. You will do some iterations, so you will definetly spent more money, BUT a 4090 is about 1800€ in Germany - so you can do about 450 trainings (or 3600 hours of training!!) on a rented GPU. If you want to try something before doing such a heavy investment, you could start like that.
> > 
> > Further, since Kaggle provides you 30 GB of VRAM (vs. about 23 GB on a Windows PC with a 4090), you can try all the things before going into investment. The big blocker with kaggle GPUs is speed, not possibilities.
> > 
> > 
> > 


---

> ## tanaka
> 
> Hmm I understood,  it seems quite difficult to compete in these competitions without using external resources.
> 
> However, I feel that suddenly buying a GPU is a high hurdle.
> 
> it seems best to try out various options like Colab or other GPU rental servers, and then decide whether to buy or rent a GPU.
> 
> [Vast.ai](http://vast.ai/) seems to be a popular option, doesn't it 🤔?
> 
> - [https://vast.ai/](https://vast.ai/)
> 
> - [https://cloud-gpus.com/](https://cloud-gpus.com/)
> 
> - [https://gist.github.com/devinschumacher/87dd5b87234f2d0e5dba56503bfba533](https://gist.github.com/devinschumacher/87dd5b87234f2d0e5dba56503bfba533)
> 
> - [https://getdeploying.com/reference/cloud-gpu](https://getdeploying.com/reference/cloud-gpu#paperspace)
> 
> 
> 
> > ## Ebi
> > 
> > I have never used vast.ai, but I personally like  [jarvislabs.ai](https://jarvislabs.ai/). 
> > 
> > It is easy and fast to create an instance and access it via SSH. I think the price is also very cheap. I mainly used it until I switched to a home server.
> > 
> > 
> > 


---

> ## Andreas Bisi
> 
> Considering past NLP competitions, you would need external resources to finish in the gold-medal area. However, I believe with a TF-IDF solution (on kaggle hardware) it's doable to finish in the bronze-medal area with some luck…
> 
> 
> 


---



* --- discussion numver 62, the number of votes :5 ---

# Unspecified exception, only when submitted (later = Submission Scoring error)

**RickPack** *Tue May 21 2024 01:00:22 GMT+0900 (日本標準時)* (5 votes)

My [Python notebook](https://www.kaggle.com/code/rickpack/python-average-prob-per-word-no-gpu) and [R notebook](https://www.kaggle.com/code/rickpack/r-average-prob-per-word-no-gpu/) run without issue but when I submit them, I get a "Notebook Threw Exception" error that is only visible on the Submissions screen. The log shows no errors.

Does anyone have a potential solution?

R:             [https://www.kaggle.com/code/rickpack/r-average-prob-per-word-no-gpu/](https://www.kaggle.com/code/rickpack/r-average-prob-per-word-no-gpu/)

Python:   [https://www.kaggle.com/code/rickpack/python-average-prob-per-word-no-gpu](https://www.kaggle.com/code/rickpack/python-average-prob-per-word-no-gpu)

[@sohier](https://www.kaggle.com/sohier), [@addisonhoward](https://www.kaggle.com/addisonhoward) 



---

 # Comments from other users

> ## David.Ricardo.H.X
> 
> i got the same problem
> 
> 
> 


---

> ## RickPackTopic Author
> 
> Reopening this [@sohier](https://www.kaggle.com/sohier), [@addisonhoward](https://www.kaggle.com/addisonhoward) in hopes of getting thoughts, please? Both the R and Python notebooks are failing with a Submission Scoring Error after minor modifications. I see that the row sums of the probabilities are not always exactly 1 (e.g., 1.002, 0.999, 1.000). If that could be the problem, could you please see if you can comment on what might repair that problem? I have tried various kinds of rounding and standardizing as you will see in code. Thank you!
> 
> R:           [https://www.kaggle.com/code/rickpack/r-average-prob-per-word-no-gpu?scriptVersionId=179034682](https://www.kaggle.com/code/rickpack/r-average-prob-per-word-no-gpu?scriptVersionId=179034682)
> 
> Python:  [https://www.kaggle.com/code/rickpack/python-average-prob-per-word-no-gpu?scriptVersionId=179035436](https://www.kaggle.com/code/rickpack/python-average-prob-per-word-no-gpu?scriptVersionId=179035436)
> 
> 
> 
> > ## Fae Gaze
> > 
> > [@rickpack](https://www.kaggle.com/rickpack) , I think that the reason that the issue of row sum of the probabilities suggested that you may have a normalization issue. Also different scores of R and python may suggest that they handle the data differently. I mean, even if the same statistical methods or the same algorithm, their implementation in r and Python libraries can differ in terms of numerical precision or optimizations. 
> > 
> > 
> > 


---

> ## RickPackTopic Author
> 
> Fixed! I have not studied why but I appeared to not get a prediction for every record. By left joining test on my predictions and imputing predictions where missing, both notebooks produced unimpresssive scores. Interesting that little differences between the notebooks yielded different scores.
> 
> 
> 
> > ## Fae Gaze
> > 
> > [@rickpack](https://www.kaggle.com/rickpack) , I suggest that the columns used to join datasets are correctly specified and contain matching data formats. After the join, I think it is better to identify any rows where predictions are missing
> > 
> > 
> > 
> > > ## RickPackTopic Author
> > > 
> > > Thank you for your reply. I did not have any NA values in the data frame because of a replacement the code included. However, this version justworked ([https://www.kaggle.com/code/rickpack/r-average-prob-per-prompt-word-no-gpu?scriptVersionId=185084007](https://www.kaggle.com/code/rickpack/r-average-prob-per-prompt-word-no-gpu?scriptVersionId=185084007)) after I included a 3rd decimal place (zeros!) in the assignment of values to the 3 target columns where NA occurs. Compare to this version that failed to generate a score ([https://www.kaggle.com/code/rickpack/r-average-prob-per-prompt-word-no-gpu?scriptVersionId=184945388](https://www.kaggle.com/code/rickpack/r-average-prob-per-prompt-word-no-gpu?scriptVersionId=184945388))
> > > 
> > > 
> > > 


---



* --- discussion numver 63, the number of votes :5 ---

# Is the Kaggle provided compute enough to join this competition?

**Andreas Bisi** *Tue May 28 2024 13:29:59 GMT+0900 (日本標準時)* (5 votes)

After participating in the Home Credit competition, I am looking forward to joining a new one. The objective of this new competition seems interesting. From a quick look at public notebooks, it appears that two popular models are LightGBM and Llama 3 8B. For the latter, is it possible to do any fine-tuning on Kaggle, or will I need to rent A100 instances?



---

 # Comments from other users

> ## Ivan Vybornov
> 
> I would not recommend finetuning on kaggle, from my experience finetuning llama with QLoRA on TPU is extremely painful timewise therefore I had to rent a RTX 4090, which does the job roughly for 8 hours.
> 
> 
> 
> > ## Dr. Gopalashivabalasubramanium Chandrashekaran
> > 
> > Thank you for your input. In your experience, how much more time will fine tuning on kaggle take vs your RTX 4090's 8 hours? Will it take 2-3x longer? I don't want to rent a RTX 4090 lol
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > Agreed on paying for Experiments. I think 2-4x is realistic. If I remember correctly, peft llama3 for some epochs took about 20 hours on kaggle and ca 8 hours on 4090. Main reason is that you can only use 2x T4 for this, which are even slower.
> > > 
> > > 
> > > 


---

> ## Kishan Vavdara
> 
> You can use kaggle TPU's for finetuning. 
> 
> 
> 


---

> ## bogoconic1
> 
> I would not advise using Kaggle compute to fine tune, unless you don’t have another choice. Quick experiments with small turnaround is beneficial in a competition and using a faster GPU like A100 helps. Also, in Kaggle, you only have 30 GPU hours + 20 TPU hours (if you know how to use it) per week
> 
> 
> 


---

> ## Valentin Werner
> 
> If you are only playing to win, then it might not work on kaggle compute. If you are here to learn, embrace the challenge and try to come up with solutions that work with the kaggle compute.
> 
> 
> 


---



* --- discussion numver 64, the number of votes :5 ---

# Is Microsoft phi3 allowed?

**Kishan Vavdara** *Thu May 30 2024 22:56:48 GMT+0900 (日本標準時)* (4 votes)

I noticed in some competitions that the host specifies certain dates after which models released are not allowed. This competition was launched on May 2nd, and phi3 was released on April 23rd under the MIT license. So, could you [@sohier](https://www.kaggle.com/sohier) [@paultimothymooney](https://www.kaggle.com/paultimothymooney) please confirm if we can use that model? 



---

 # Comments from other users

> ## Kishan VavdaraTopic Author
> 
> Hello, [@mylesoneill](https://www.kaggle.com/mylesoneill) [@addisonhoward](https://www.kaggle.com/addisonhoward) Could you please confirm? I can't find that anywhere on competition page.  
> 
> 
> 
> > ## Addison Howard
> > 
> > Hi Kishan,
> > 
> > The Kaggle team cannot make license or rule interpretations for you or our hosts. I will note, however, that the only competition with a specified date relating to model releases is the AIMO competition, and that rule does not apply to other competitions.
> > 
> > 
> > 
> > > ## Kishan VavdaraTopic Author
> > > 
> > > Thank you so much for clarifying. Indeed, I read that somewhere in the AIMO competition rules.
> > > 
> > > 
> > > 
> > > ## Valentin Werner
> > > 
> > > If you dont mind me asking, did you find phi to perform similarly well to llama3?
> > > 
> > > 
> > > 
> > > ## Kishan VavdaraTopic Author
> > > 
> > > I haven't done extensive experiments with phi3 yet, but I've found it to be much better than other models of similar size. So far, it hasn't performed on par with llama-3. The best score I've achieved with till now is 0.994 and i think can still push further.    
> > > 
> > > 
> > > 


---



* --- discussion numver 65, the number of votes :5 ---

# Deberta Baseline - LB 1.075

**Fritz Cremer** *Fri May 03 2024 21:45:56 GMT+0900 (日本標準時)* (5 votes)

I made a very quick deberta-v3-base baseline:

[https://www.kaggle.com/code/fritzcremer/lmsys-deberta-v3-base-baseline/notebook](https://www.kaggle.com/code/fritzcremer/lmsys-deberta-v3-base-baseline/notebook)

Currently, it only uses a small fraction of the train data and doesn't get a great score. But this is how the code for a deberta submission could look like.

Possible improvements:

- Utilize all data

- K Fold cross-validation

- Swap the responses for more data

- Formulate the loss differently

Especially the last one. I think it could make sense to have a two stage model. In the first stage, just predict if a response won a duel or not (without providing the other response), in the second stage, using two such predictions + hand crafted features to predict the better response. I think this looks like a very interesting competition, with not one straight forward path.

Let me know what you think!



---

 # Comments from other users

> ## Nicholas Broad
> 
> Just so you know, this is basically just random guessing.
> 
> ```
> from sklearn.metrics import log_loss
> log_loss([1], [[1/3, 1/3, 1/3]], labels=[0,1,2])
> 
> # 1.0986122886681098
> 
> ```
> 
> 
> 
> > ## Valentin Werner
> > 
> > The Notebook exactly replicates the label distribution. It seems that a basic starter with huggingface Trainer is not able to learn from the data.
> > 
> > 
> > 
> > ## Fritz CremerTopic Author
> > 
> > [@nbroad](https://www.kaggle.com/nbroad) Yes, I know. It was more like a general setup to fit a model for this task with huggingface. I found that the training was very unstable, on some runs the model learned more than just the label distribution (e.g. on LB the notebook has 1.075 with the submitted version), and on others it failed completely. But then again, it is not a well tuned approach at all, just a quick first day approach 😄
> > 
> > 
> > 


---



* --- discussion numver 66, the number of votes :4 ---

# What a bad score!!! I am puzzled whether it is reasonable?

**Turbo** *Tue Jul 30 2024 13:28:30 GMT+0900 (日本標準時)* (4 votes)

I encountered inference score bad problem.

I used gemma-2 to classify and got local cv(20% data) = 0.9366, lb=0.968.

Also, I used llama-3 to regression and got local cv(20% data) = 0.916, lb=0.934.

What a bad result!!!.

Inspired by [@jsday96](https://www.kaggle.com/jsday96), so I tried to both inference on kaggle and local. The results are shown below. The results are train data head 10. The difference is very small. I am puzzled whether it is reasonable?



---

 # Comments from other users

> ## KeShuang Liu
> 
> After reading your discussion, I tested my model, which was very useful to me. I don't know why my local prediction is so different from the prediction on Kaggle, which leads to a big difference between cv and lb. I think this is the reason. This gave me new ideas. Thank you very much for your discussion.
> 
> 
> 
> > ## TurboTopic Author
> > 
> > Hey, the results have big difference. Maybe some bugs in the code which you need to check.
> > 
> > 
> > 


---

> ## Helmut12
> 
> I think that may be normal in kaggle competition. Is this related to overfitting of the data? Like there is a significant pattern in our test set. I heard that there is a huge discrepancy between LB and the final result in a previous competition because of overfitting.
> 
> 
> 


---

> ## justin1357
> 
> cv is lower than lb, that's normal.
> 
> 
> 
> > ## TurboTopic Author
> > 
> > low 0.02. Others said the results of cv and lb are very small.
> > 
> > 
> > 
> > > ## justin1357
> > > 
> > > In my exp, cv low 0.02 too
> > > 
> > > 
> > > 


---



* --- discussion numver 67, the number of votes :4 ---

# Llama3.1-8B May Release Soon

**Yixiao Yuan** *Tue Jul 23 2024 09:55:14 GMT+0900 (日本標準時)* (4 votes)

According to the latest leaks, the upcoming llama3.1 8b model is expected to outperform the current Gemma2, delivering significant improvements over previous versions llama3. The model is anticipated to be released before the competition ends. Given its naming convention, LLama3.1 should seamlessly integrate with the existing LLama3 framework.



---

 # Comments from other users

> ## Valentin Werner
> 
> 
> 
> 
> 


---

> ## sayoulala
> 
> Oh,My electricity bill is going to exceed the limit again.
> 
> 
> 


---

> ## Yixiao YuanTopic Author
> 
> Llama3.1 is released.
> 
> [https://huggingface.co/collections/meta-llama/llama-31-669fc079a0c406a149a5738f](https://huggingface.co/collections/meta-llama/llama-31-669fc079a0c406a149a5738f)
> 
> 
> 


---

> ## Valentin Werner
> 
> Can you please share the source alongside the screenshot? I am quite interested in the numbers I am seeing, and sources are always extremely important for leaks like this.
> 
> 
> 
> > ## Yixiao YuanTopic Author
> > 
> > [https://x.com/iScienceLuvr/status/1815519917715730702](https://x.com/iScienceLuvr/status/1815519917715730702)
> > 
> > 
> > 
> > ## naturalseeker
> > 
> > [https://www.reddit.com/r/LocalLLaMA/comments/1e9qpgt/meta_llama_31_models_available_in_hf_8b_70b_and/](https://www.reddit.com/r/LocalLLaMA/comments/1e9qpgt/meta_llama_31_models_available_in_hf_8b_70b_and/)
> > 
> > 
> > 


---

> ## Dlond Mike
> 
> ….LLMs' game
> 
> 
> 


---



* --- discussion numver 68, the number of votes :4 ---

# Train LLMs efficently in multi chip environment [GPU/TPU]

**Simon Veitner** *Wed May 29 2024 16:24:01 GMT+0900 (日本標準時)* (4 votes)

Hello guys,

I shared a customizable notebook that let's you train LLMs with FSDP and potentially TP technique on multiple GPU/TPU chips.

The architecture was inspired by [first place solution in LLM science exam.](https://www.kaggle.com/competitions/kaggle-llm-science-exam/discussion/446422)

Note that the score of the notebook is rather bad but can be easily improved by adjusting preproccesing/modelling etc etc.

[See the notebook here](https://www.kaggle.com/code/simonveitner/fsdp-with-scalax)





* --- discussion numver 69, the number of votes :4 ---

# TF-IDF + Word2Vec = FTW [LB 1.026]

**Rich Olson** *Thu May 09 2024 15:54:49 GMT+0900 (日本標準時)* (4 votes)

I've posted a new notebook that shows to combine TF-IDF with Word2Vec to get an LB of 1.026:

[https://www.kaggle.com/code/richolson/tf-idf-word2vec-ftw-lb-1-026](https://www.kaggle.com/code/richolson/tf-idf-word2vec-ftw-lb-1-026)

This builds on my prior TF-IDF only notebook (LB 1.038):

[https://www.kaggle.com/code/richolson/lmsys-tf-idf-boosted-trees](https://www.kaggle.com/code/richolson/lmsys-tf-idf-boosted-trees)

As previously - I'm using LGBMClassifier for deciphering things…

In one version of the notebook - I just used Word2Vec - and it alone was good for LB 1.038 (same as TF-IDF):

[https://www.kaggle.com/code/richolson/tf-idf-word2vec-ftw?scriptVersionId=176534641](https://www.kaggle.com/code/richolson/tf-idf-word2vec-ftw?scriptVersionId=176534641)

(this might actually be the more interesting bit - as I don't think anyone has shared a notebook using Word2Vec for this competition yet)

Since both TF-IDF and Word2Vec each score 1.038 on the LB separately - but manage 1.026 together - they presumably are generating features that are a little unique.

I've seen some other notebooks combining TF-IDF with other simple features (like text length) to boost score.  It might be that tossing in Word2Vec can boost things further.





* --- discussion numver 70, the number of votes :4 ---

# Why So Little

**eli plutchok** *Wed May 08 2024 13:44:26 GMT+0900 (日本標準時)* (4 votes)

Hello Everyone, 

I'm new to kaggle. I'm wondering why the competition organizers gave us a data set of just ~60K items when they surely must have a lot more from the same place. Should I expect them to release more at a later date, or are they just trying to make it extra challenging for us?

(The LMSYS arena leaderboard is based on over 900k votes: [https://chat.lmsys.org/?leaderboard](https://chat.lmsys.org/?leaderboard))



---

 # Comments from other users

> ## Valentin Werner
> 
> There are many reasons why a company may not want to disclose all of their data. I think 60k samples are more than what we often see for challenges. This is already a size where you are taking a small subset to test things first.
> 
> 
> 
> > ## eli plutchokTopic Author
> > 
> > Ok, I get it. They don't want people to have their proprietary data. But still, they won't get the best pre-trained models by withholding the data. Do they care mainly about the code used to train the models? I guess, my dumb question is: what is the primary objective of, LMSYS, the company sponsoring this? 
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > They are licensed the winning solutions (see Rules #A1). These companies are often able to transfer solutions to their own data themselves. 
> > > 
> > > However, company motivation for challenges may vary: For example, they maybe want to proof a concept or make a study whether things are achievable. Opening such a challenge to kaggle is smart because doing the same thing internally will often be more expensive and less diverse in solution approaches.
> > > 
> > > 
> > > 


---



* --- discussion numver 71, the number of votes :4 ---

# Do we need the class "tie"?

**Anh Bui** *Fri May 03 2024 15:50:05 GMT+0900 (日本標準時)* (4 votes)

I have a question about why there is a class 'tie', when based on the probabilities (winner_model_a/winner_model_b) = (0.5, 0.5), it can be determined whether the two models have a 'tie'.



---

 # Comments from other users

> ## Marília Prata
> 
> Hi Anh Bui (bibanh),
> 
> On the original dataset instead of "winner_tie"  they have "winner" column (where the Rows are: model_a, model_b, tie AND tie (bothbad)
> 
> Battles No ties
> 
> battles_no_ties = battles[~battles["winner"].str.contains("tie")]
> 
> Battles without ties
> 
> visualize_battle_count(battles_no_ties, "Battle Count for Each Combination of Models (without Ties)")
> 
> Counting ties
> 
> visualize_battle_count(battles[battles['winner'].str.contains("tie")], "Tie Count for Each Combination of Models")
> 
> [https://colab.research.google.com/drive/1KdwokPjirkTmpO_P1WByFNFiqxWQquwH#scrollTo=PbTdhkLQp113](https://colab.research.google.com/drive/1KdwokPjirkTmpO_P1WByFNFiqxWQquwH#scrollTo=PbTdhkLQp113)
> 
> That's what the authors wrote:
> 
> "Statistics
> 
> "The authors allowed the user to declare a tie between the pairs of models. To collect additional data, later in the tournament they also allowed the user to declare a tie in which both models were bad. There were a significant portion of tied outcomes."
> 
> I hope it could help to clarify. I didn't read anything else about the ties on that Notebook or in their paper too.
> 
> 
> 


---

> ## bogoconic1
> 
> I would think it is necessary for reason (B)
> 
> A tie could mean
> 
> (A) The user rates both responses as equally good
> 
> (B) The user rates both responses as equally bad. The 2 models can answer in different ways, of which both responses are hallucinated (by making up completely different facts etc) or not answering the question
> 
> For (B) I’m pretty sure the 2 classes will not be predicted as (0.5, 0.5) 🧐
> 
> 
> 


---

> ## Rich Olson
> 
> For my first submission - I tried filling in "winner_tie" with all 0's.
> 
> That got me a score of 11.73 (almost last-place).  At least - I'm assuming "winner_tie" being 0's was a factor.
> 
> For my next entry - I'm going to try to fill in winner_tie based on the confidence of A or B winning.  Hopefully this improves things…
> 
> In the train data - it seems ties are very common (about 1 out of 3).
> 
> 
> 


---



* --- discussion numver 72, the number of votes :4 ---

# [Starter] Deberta-v3 Train & Inference code

**Heroseo** *Sat May 04 2024 18:55:29 GMT+0900 (日本標準時)* (4 votes)

# Intro

Hi, I wanted to share good train and inference notebooks. :)

- Pytorch Train & Inference

- Only prompt was used.

- I recommend adjusting token_lengh for your GPU memory.

- There are many things to try.

# Notebooks - v3

- Train : [[Train] LMSYS / Deberta-v3 starter code🔥](https://www.kaggle.com/code/piantic/train-deberta-v3-starter-code)

- Inference : [[Inference] LMSYS / Deberta-v3 starter code🔥](https://www.kaggle.com/code/piantic/inference-deberta-v3-starter-code)

# End

There is a lot of room for improvement. Please add more cool ideas. :)

Thank you!

p.s. It feels strange to share notebooks with Kaggle after a long time.





* --- discussion numver 73, the number of votes :3 ---

# External datasets

**Dlond Mike** *Tue Jul 23 2024 13:03:53 GMT+0900 (日本標準時)* (3 votes)

I want to know whether the additional datasets make sense…anyone tried them?just  someone share in the discussion



---

 # Comments from other users

> ## justin1357
> 
> Not work… I think it's because the source is different, so distribution is not the same
> 
> 
> 
> > ## Songling
> > 
> > [@justin1357](https://www.kaggle.com/justin1357) Yes, I have also tried external data, and it is the same situation. I am curious about what other methods are there.
> > 
> > 
> > 
> > ## Xinyuan Qiao
> > 
> > It do works, try not just mix it together
> > 
> > 
> > 
> > > ## SAY WHAT
> > > 
> > > Other methods?
> > > 
> > > 
> > > 


---



* --- discussion numver 74, the number of votes :3 ---

# shake up ?

**Songling** *Tue Jul 23 2024 11:13:27 GMT+0900 (日本標準時)* (3 votes)

Friends, do you think there will be major changes in the private leaderboard of this llm game? I think it will be relatively stable.



---

 # Comments from other users

> ## sayoulala
> 
> I think so too.
> 
> 
> 


---

> ## Dlond Mike
> 
> Nope…it seems like all of us use LLM like gemma2-9b and llama3-8b.
> 
> 
> 


---



* --- discussion numver 75, the number of votes :3 ---

# [Need Help] Running Gemma 2 9b in Keras on 2xT4s

**Pranshu Bahadur** *Mon Jul 22 2024 12:28:59 GMT+0900 (日本標準時)* (3 votes)

Hey guys!

I made this notebook to train Gemma 2 9b on TPUs.

But the competition doesn't allow TPUs for submission….which is a bit awkward haha

So I'm enlisting your help to figure this out!

Would really appreciate any feedback, I am looking to learn!

Training nb (~3 hrs for 1 epoch):

[https://www.kaggle.com/code/pranshubahadur/tf-gemma-2-9b-lmsys-training-tpu](https://www.kaggle.com/code/pranshubahadur/tf-gemma-2-9b-lmsys-training-tpu)

Unsolved inference nb:

[https://www.kaggle.com/code/pranshubahadur/unsolved-inference-tf-gemma-2-9b-lmsys](https://www.kaggle.com/code/pranshubahadur/unsolved-inference-tf-gemma-2-9b-lmsys)



---

 # Comments from other users

> ## Pranshu BahadurTopic Author
> 
> Update: Inference works now, out of tpu quota will update on saturday
> 
> 
> 
> > ## Somesh88
> > 
> > what did you do to make inference run?
> > 
> > 
> > 
> > > ## Pranshu BahadurTopic Author
> > > 
> > > mainly device allocation followed by a custom prediction loop and set_floatx('float16')
> > > 
> > > no quantization was needed 
> > > 
> > > you can check out my inference nb linked above
> > > 
> > > 
> > > 


---



* --- discussion numver 76, the number of votes :3 ---

# Are external data helpful? 

**Andreas Bisi** *Sun Jun 23 2024 18:27:18 GMT+0900 (日本標準時)* (3 votes)

Has anyone used the [LMSYS - Additional 33k Labelled Conversations](https://www.kaggle.com/datasets/abdullahmeda/lmsys-additional-33k-labelled-conversations) dataset? If yes, are the CV and LB results yielded better or worse? Do you have suspicions of overfitting?



---

 # Comments from other users

> ## lllleeeo
> 
> The cv is significantly lower Don't know about the lab yet Worried about overfitting…….
> 
> 
> 


---

> ## YingxiZhang
> 
> not work.😭
> 
> 
> 


---

> ## justin1357
> 
> In my experiment, not work…sad
> 
> 
> 


---

> ## sayoulala
> 
> May I ask where did you get this data from?
> 
> 
> 
> > ## Andreas BisiTopic Author
> > 
> > There' not mine - I found them on an early discussion
> > 
> > 
> > 
> > > ## sayoulala
> > > 
> > > Thank you for your response. I'll try adding it to the training set and see if it makes a difference.
> > > 
> > > 
> > > 
> > > ## yechenzhi1
> > > 
> > > Hi, did you test the external data? 
> > > 
> > > 
> > > 


---



* --- discussion numver 77, the number of votes :3 ---

# Clean Text

**TheStoneMX** *Sun Jul 14 2024 07:21:59 GMT+0900 (日本標準時)* (3 votes)

Hi there all,

I have been trying different text-cleaning techniques, but they do not work… can someone share? or is there no text cleaning on these types of corpus?

Or what other ways to increase the score besides the Ensemble models?

Thanks!

Like:

```
import pandas as pd
import re
from datasets import Dataset

def load_and_clean_data(filepath):
    # Load dataset
    df = pd.read_csv(filepath)

    # Remove duplicates
    df.drop_duplicates(inplace=True)

    # Handle missing values (replace NaN with empty string)
    df.fillna("", inplace=True)

    # Clean text function
    def clean_text(text):
        # Convert to string in case of any non-string values
        text = str(text)

        # Remove unwanted characters
        text = re.sub(r'[\[\]\'"]', '', text)  # Corrected regular expression

        # Remove punctuation and special characters except periods, commas, apostrophes, and double quotes
        text = re.sub(r'[^\w\s\.,\'\"]', '', text)       
        text = text.lower() # Convert to lowercase
        text.strip()  # strip leading/trailing spaces

        # Remove URLs and Email Addresses
        text = re.sub(r'\b(?:https?://|www\.)\S+\b', '', text)
        text = re.sub(r'\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,}\b', '', text)
         # Remove numbers
        text = re.sub(r'\d+', '', text)

        return text

    # Clean text columns
    df['prompt'] = df['prompt'].apply(clean_text)
    df['response_a'] = df['response_a'].apply(clean_text)
    df['response_b'] = df['response_b'].apply(clean_text)

    return df

# Load and clean the data
df_cleaned = load_and_clean_data("../input/lmsys-chatbot-arena/train.csv")

# Convert to Hugging Face Dataset
ds = Dataset.from_pandas(df_cleaned)

# Print the first row 
print(ds[:1])

```



---

 # Comments from other users

> ## Bharat Raghavan
> 
> It seems to me like your code manages to clean up the text properly, unless you want to clean it further; in that case, what text-cleaning techniques are you talking about?
> 
> As for increasing the score, depending on the approach, hyperparameter tuning can be beneficial. However, I would just recommend that you be wary of overfitting when considering your approach to hyperparameter tuning.
> 
> 
> 


---



* --- discussion numver 78, the number of votes :3 ---

# How much data to train Llama 3?

**ano** *Thu Jul 11 2024 08:00:45 GMT+0900 (日本標準時)* (3 votes)

How much data are you using for training Llama 3? I use half of all the given training data for training and the other half as validation data, with cv: 0.968, lb: 0.979.

I want to know about the relationship between the amount of training data and accuracy. I remember reading a discussion somewhere that said using all the data for training does not change the score, but I lost track of that discussion.



---

 # Comments from other users

> ## James Day
> 
> Hesitant to share details about my experiments until the end of the competition, but it is possible to achieve significant accuracy improvements by scaling from tens of thousands of training examples to hundreds of thousands, so I would not expect your models to be saturating at 50% of the data we received from the competition organizers. Using more than 200% is better than 80%. I never scaled down to only training on 50%.
> 
> Broadly speaking, my intuition is that adding more data is almost always beneficial (albeit with diminishing returns) so long as that data is sufficiently high quality (not too repetitive, mislabeled, or different from the test data) and your model has sufficiently high capacity to learn from that data (which shouldn't be a problem for Llama 3 8B with a decent LoRA config).
> 
> 
> 
> > ## anoTopic Author
> > 
> > Thank you for the valuable information! It seems I was mistaken in thinking that a small amount of training data would be sufficient. I'll try optimizing by adding training data (including external data) and changing the parameters.
> > 
> > 
> > 
> > ## Cody_Null
> > 
> > You have already shared a friendly amount of information so feel free to hold back, are you generating new data from the training data?
> > 
> > 
> > 
> > > ## James Day
> > > 
> > > I don't want to elaborate on where my extra data came from until the end of the competition. 🤐
> > > 
> > > 
> > > 
> > > ## Sparsh Tewatia
> > > 
> > > Thats enough for the smart one to know. 😀
> > > 
> > > 
> > > 


---



* --- discussion numver 79, the number of votes :3 ---

# Multi GPU support

**Varun Jagannath** *Mon Jul 08 2024 14:28:09 GMT+0900 (日本標準時)* (3 votes)

Since we have two GPU's of T4, how to fine-tune LLM for multi GPU capability. Any suggestions or tutorials for sequence classification





* --- discussion numver 80, the number of votes :3 ---

# Why is this competition less popular than AES2?

**sule** *Fri Jul 05 2024 04:32:15 GMT+0900 (日本標準時)* (3 votes)

Sorry I am new so it is not obvious to me. 

AES2 had 2700 participants, this one probably will not reach more than 2000 at the end.

Is it due to summer holidays?

Or maybe competition requiring  a stronger compute?

The topic certainly does not seem niche, maybe even less niche than AES2?

I am not aware of any organizational mistakes?

Maybe all my assumptions are wrong, I would like to hear your thoughts.



---

 # Comments from other users

> ## Enter your display name
> 
> Because this competition requires much more computational resources.😭
> 
> 
> 
> > ## suleTopic Author
> > 
> > thanks for reply!
> > 
> > 
> > 


---

> ## Ravi Ramakrishnan
> 
> Perhaps we would see some additional competition here as the AES challenge is now over [@zvonimirsucic](https://www.kaggle.com/zvonimirsucic) 
> 
> 
> 
> > ## suleTopic Author
> > 
> > I hope so too, I started too late for AES2
> > 
> > 
> > 


---



* --- discussion numver 81, the number of votes :3 ---

# Does calibration matter?

**yechenzhi1** *Tue Jul 02 2024 19:06:56 GMT+0900 (日本標準時)* (3 votes)

Hello everyone,

As VALENTIN WERNER mentioned in a [previous discussion](https://www.kaggle.com/code/valentinwerner/log-loss-what-are-good-scores/notebook), good calibration can greatly enhance log loss scores. Despite experimenting with various calibration techniques, such as temperature adjustments and training a binary classifier for hard examples, I haven't achieved satisfactory results. I've been pondering this issue for a while. Should I perhaps shift my focus to other strategies, like ensemble methods or exploring newer models? Thanks in advance!



---

 # Comments from other users

> ## James Day
> 
> I haven't had any success trying to make my predictions better calibrated as a post-processing step either. Platt scaling, isotonic regression, and model stacking all seem to do more harm than good.
> 
> A while ago ChatGPT suggested I investigate how well calibrated my predictions are by calculating "Expected Calibration Error" as an additional cross-validation metric and generating "reliability diagrams". My code for doing that and sample results for my best ensemble (0.899 LB) are included below. It seems the confidence values are really well correlated with the probability of the top guess being correct, so there's not much that post-processing logic can do to help. Perhaps my models are slightly biased towards being a little under confident, but my best attempts at correcting for that at inference time score within 0.001 (CV) of just using the raw predictions. Perhaps if the underlying models were weaker the post-processing would be more beneficial.
> 
> ```
> def compute_ece(predictions, labels, num_bins=25):
>     bin_boundaries = np.linspace(0, 1, num_bins + 1)
>     ece = 0.0
>     total_samples = len(labels)
> 
>     confidences = []
>     accuracies = []
> 
>     for bin_lower, bin_upper in zip(bin_boundaries[:-1], bin_boundaries[1:]):
>         bin_indices = np.where((predictions >= bin_lower) & (predictions < bin_upper))[0]
>         if len(bin_indices) == 0:
>             continue
> 
>         bin_confidence = predictions[bin_indices].max(axis=1).mean()
>         bin_accuracy = (labels[bin_indices] == predictions[bin_indices].argmax(axis=1)).mean()
> 
>         bin_size = len(bin_indices)
>         ece += (bin_size / total_samples) * np.abs(bin_confidence - bin_accuracy)
> 
>         confidences.append(bin_confidence)
>         accuracies.append(bin_accuracy)
> 
>     return ece, confidences, accuracies
> 
> ece, confidences, accuracies = compute_ece(all_predictions, np.array(labels))
> print(f'Expected Calibration Error (ECE): {ece:.4f}')
> 
> from matplotlib import pyplot as plt
> 
> plt.plot([0, 1], [0, 1], linestyle='--')
> plt.scatter(confidences, accuracies, marker='o')
> plt.xlabel('Confidence')
> plt.ylabel('Accuracy')
> plt.title('Reliability Diagram')
> plt.show()
> 
> ```
> 
> 
> 
> > ## Yu Chengzhi
> > 
> > Thank you for sharing! How can I ensemble different methods? Is it just the mean of probabilities from various models?
> > 
> > 
> > 
> > > ## yechenzhi1Topic Author
> > > 
> > > You can adjust the weight of each model's probability, for example, preds = 0.8 * model_a_preds + 0.2 * model_b_preds.
> > > 
> > > 
> > > 
> > ## yechenzhi1Topic Author
> > 
> > Thanks for your reply! I guess I will focus on the training process or try some new ideas.
> > 
> > 
> > 


---

> ## Valentin Werner
> 
> Your models are already minimizing their loss, so post processing predictions will give no good results from my experience. However, when trainings transformers, parameters such as label smoothing may help to achieve better calibration (as the model is basically asked to predict 0.9 instead of 1.0 with an alpha of 0.1 etc.) - However, in general the data is confusing that this is one of the few challenges where my models basically never predict > 0.85 because it is so hard to be that confident.
> 
> When I wrote the discussion and linked notebook, I assumed that models would heavily overfit and strongly favour some classes, which does not seem to be the case.
> 
> Calibration definetly does matter, but it should probably be something you do during the training, rather than afterwards.
> 
> 
> 


---



* --- discussion numver 82, the number of votes :3 ---

# Training outside kaggle

**Ahmad Al-Husainy** *Sun Jun 16 2024 04:30:02 GMT+0900 (日本標準時)* (3 votes)

Hello, this is my first competition, and I'm curious to know if it's possible to train large pre-trained models in an external environment and then simply upload the weights for submission. 



---

 # Comments from other users

> ## Lorry Zou
> 
> You definitely can do that. It's also what I'm doing. However, since this competition requires internet-off submission, I'm sure I will run into some issues…
> 
> 
> 
> > ## Valentin Werner
> > 
> > Just load it as a kaggle dataset or kaggle model!
> > 
> > You only have to make sure the models you are using are open source. 
> > 
> > 
> > 
> > > ## Ivel afred
> > > 
> > > Does this mean that your model needs to be public on Kaggle? Or it's okay to just make it public on Hugging Face.
> > > 
> > > 
> > > 
> > > ## Valentin Werner
> > > 
> > > It can be private on kaggle, just available for you. You dont have to make it public on huggingface either. Its just important that the model that you finetune is also available for others. (e.g., DeBERTa or Llama are open source; GPT-4 is not - if you finetune GPT-4 for the competition, that would be not fair and you would have to make your GPT-4 tuned model available for everybody in the competition instead (I think))
> > > 
> > > 
> > > 
> > > ## Ivel afred
> > > 
> > > thanks, that helps me a lot
> > > 
> > > 
> > > 
> > ## Ahmad Al-HusainyTopic Author
> > 
> > Thank you for your comment. I want to clarify my approach: I'm currently using Google Colab for model development. When I attempt to train the models on Kaggle, I encounter GPU memory issues and other problems related to the Kaggle environment it self, even though the same code runs smoothly on Colab. I'm considering training the model in Colab and then extracting the best model weights. My plan is to rebuild the model on Kaggle, load the weights, predict on the test dataset, and submit my results. Additionally, the environment on Colab is more extensive than on Kaggle, so training on Kaggle could potentially exceed the 9-hour limit.
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > That is the correct approach
> > > 
> > > 
> > > 


---

> ## Marília Prata
> 
> I think it depends on each competition rules. Though I'm not certain. Maybe Paul Mooney, Sohier Dane or Addison Howard could answer that.
> 
> By the way, welcome to your 1st competition.
> 
> 
> 


---



* --- discussion numver 83, the number of votes :3 ---

# What is the trick...

**TheStoneMX** *Sun Jun 16 2024 01:19:44 GMT+0900 (日本標準時)* (3 votes)

I find almost impossible to fine-tune with the recurses that we get from Kaggle, and at home not enough GPU memory.

What are people using?

External providers? Google, Azure, My Pods, etc.

Any suggestions?

What are people doing, on these type of competitions, Text cleaning, stop words removal, Stemming and lemmatization, etc.

Thanks for any tips guys.



---

 # Comments from other users

> ## Ravi Ramakrishnan
> 
> [@oscarrangel](https://www.kaggle.com/oscarrangel) I recommend you to try out [runpod.io](https://www.runpod.io/)
> 
> They offer excellent GPUs at moderately affordable prices and across various payment plans and options
> 
> 
> 
> > ## TheStoneMXTopic Author
> > 
> > Yes, thanks. That is what I started to use, but they have secure cloud and community cloud. I am using community one. Is that correct?
> > 
> > 
> > 


---

> ## Cody_Null
> 
> I have been in this position before myself. The best option (in my opinion) would be cloud resources. It is up to you how much you are willing to spend and what experiments are worth it and I know there are a lot of platforms to choose from and price may vary based off what you need and your area. Some popular ones are runpod, vast.ai, google cloud, and then depending on your personal situation AWS or Azure may be more accessible but those first 3 are more likely and worth researching. No doubt I have missed some, but a good starting point. 
> 
> 
> 


---



* --- discussion numver 84, the number of votes :3 ---

# Criteria and Approaches

**PierreSylvain** *Sun Jun 16 2024 01:53:09 GMT+0900 (日本標準時)* (3 votes)

Choosing the right answer from two options can be tricky. A study found that when people have to choose between two equally good options, they usually pick the one that’s easier to explain and defend (Slovic, P. (1975). Choice between equally valued alternatives. Journal of Experimental Psychology: Human Perception and Performance, 1(3), 280–287. [https://doi.org/10.1037/0096-1523.1.3.280](https://psycnet.apa.org/doi/10.1037/0096-1523.1.3.280)).

In real life, figuring out the best answer means checking off a few key boxes:

Accuracy

- Is the answer correct? This can be tough if you don’t know the answer yourself.

Clarity

- Is the answer easy to understand?

Coherence

- Is the answer well-structured and makes sense?

Detail

- Is the answer thorough? Do you need a detailed answer or just a brief one?

Sources

- Does the answer have references or sources? Are they reliable and up-to-date?

Objectivity

- Is the answer unbiased and neutral?

Practicality

- Is the answer useful and easy to apply?

Of course, it’s rare to find an answer that ticks all these boxes perfectly. Usually, it’s a mix of these factors that help you decide. For example, one answer might be super detailed but hard to understand, while another might be clear but not very deep.

Here are some tips for evaluating answers:

- How long is the text?

- How varied is the vocabulary?

- How is the sentence structure?

- What’s the cosine similarity score?

- What’s the sentiment analysis?

- Use a model to check text quality.

- Use a multi-criteria model to judge the text (accuracy, clarity, relevance, etc.)

There are plenty of other ways to evaluate, but for now, I need to code what I just wrote.



---

 # Comments from other users

> ## Valentin Werner
> 
> I tried a lot (almost exactly the features you describe) what you just wrote, my XGB model came out at 1.024 for the CV and 1.032 on LB. I hope your Code will yield better results!
> 
> 
> 


---



* --- discussion numver 85, the number of votes :3 ---

# Notebook threw exception

**Kaizhao Liang** *Thu May 16 2024 05:57:49 GMT+0900 (日本標準時)* (3 votes)

locally on the sample test csv, it runs fine. But submission throws exception without any useful feedback on the error log. shouldn't have been OOM since it's running BS = 1.



---

 # Comments from other users

> ## Valentin Werner
> 
> I had a similar error - for me this was what fixed it: 
> 
> ```
>  row.prompt.replace("null", "'null'")
>  row.response_a.replace("null", "'null'")
>  row.response_b.replace("null", "'null'")
> 
> ```
> 
> 
> 
> > ## Kaizhao LiangTopic Author
> > 
> > ah that could be the edge case it was discussing the other threads, let me give it a try thanks!
> > 
> > 
> > 
> > > ## RickPack
> > > 
> > > Please let us know if that worked.
> > > 
> > > 
> > > 


---

> ## jiangli59
> 
> I also met the same problem. Any update?
> 
> 
> 
> > ## jiangli59
> > 
> > If you use Llama-8b, I think it may raise this error due to out-of-memory. Sad! So, this error could be the source of oom?
> > 
> > 
> > 


---

> ## RickPack
> 
> i experienced similar today with an R notebook. Wondering if the submission needs to be rounded to two decimal places. What a does BS mean?
> 
> 
> 
> > ## Kaizhao LiangTopic Author
> > 
> > batch size = 1
> > 
> > 
> > 
> > ## Kaizhao LiangTopic Author
> > 
> > It also runs two hours before hitting that error, so clearly some edge cases that have not been exposed. Could be something due to parsing. But the error itself is not helpful for debugging at all.
> > 
> > 
> > 
> > > ## Alex Golubev
> > > 
> > > You can try to take a sample (e.g. 10k) from train and run your script on it. Probably you have a chance to hit the same error. Btw, what is the error message?
> > > 
> > > 
> > > 


---



* --- discussion numver 86, the number of votes :3 ---

# One-Feature Decision Tree

**AbaoJiang** *Wed Jun 05 2024 00:50:58 GMT+0900 (日本標準時)* (3 votes)

Hi everyone,

We've seen many showing that features based on the length difference between response A and B are useful. So, I try to run a quick experiment using DecisionTreeClassifier fed with only a single feature [here](https://www.kaggle.com/code/abaojiang/lmsys-detailed-eda?scriptVersionId=181492294). Following illustrates the decision tree of one fold,

[](https://postimg.cc/Y4YBzCJS)

As can be observed, the model learns the relationship between the length difference feature and winners,

On the right side, the winners are model A, which have longer responses.
In the middle, ties are the majority.
On the left side, the winners are model B.

The approach yields local CV score of 1.0588 with StratifiedKFold, which can't beat our naive baseline. This just another way to explore this important relationship (related to verbosity bias). Hope you find this interesting!



---

 # Comments from other users

> ## Valentin Werner
> 
> Interesting way to show feature value.
> 
> Length is the most valuable feature I found so far, but completely ignores the quality of the answer. I created a feature, that was actually among top 4 of my features, which looks into whether a model says something along the lines of "As an AI I cannot help you with that". This type of qualitative evaluation will be what is needed beyond the structural features such as length (and sadly also the reason why we have to go back go embeddings for some parts).
> 
> 
> 
> > ## AbaoJiangTopic Author
> > 
> > Hi [@valentinwerner](https://www.kaggle.com/valentinwerner),
> > 
> > Thanks for your reply.
> > 
> > I only try structural features so far, and nothing can beat the naive baseline based on the response length difference bucket. Though verbosity bias do exist, there still have much information to be extracted in different ways (e.g., contextual embeddings). Tbh, I'm an NLP newbie, and try to share what I discover during this learning journey. Thanks for your insightful sharing!
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > What baseline are you referring to?
> > > 
> > > Thanks for sharing your insights, its always appreciated!
> > > 
> > > 
> > > 
> > > ## AbaoJiangTopic Author
> > > 
> > > Hi [@valentinwerner](https://www.kaggle.com/valentinwerner),
> > > 
> > > Sorry for the late reply. I mean the naive baseline in the section Length Difference Bucket Mean Prediction of my EDA notebook!
> > > 
> > > 
> > > 


---

> ## KTibow Personal
> 
> A decision tree seemed like an odd choice, so I tried some polynomial regressions. It basically just ends up saying "bigger responses are better".
> 
> 
> 
> > ## AbaoJiangTopic Author
> > 
> > Hi,
> > 
> > The reason why I choose DT is that I want to do comparison with the naive baseline based on the manual binning of response length difference. Because DT itself learns to bin the length difference automatically, I just share that we can observe the similar property from different angles.
> > 
> > Anyway, thanks for your sharing.
> > 
> > 
> > 
> > ## Vishal Maurya
> > 
> > Hii [@ktibow](https://www.kaggle.com/ktibow), thanks for sharing this. Could you share the R2-score of these polynomial models above, I just want to know that how strong and significant relationships are there.
> > 
> > 
> > 


---



* --- discussion numver 87, the number of votes :3 ---

# Question about rule(fine tuning the LLM)

**eigenquant** *Sat Jun 08 2024 19:37:15 GMT+0900 (日本標準時)* (3 votes)


- Is it okay to do fine tuning the LLM with personal gpu(outside from kaggle) and use it for this competition?



---

 # Comments from other users

> ## Valentin Werner
> 
> Yes, as long as the LLM and Data you are using is Open source (e.g., MIT, Apache 2.0). You can also rent GPUs and train there, its all fair play.
> 
> 
> 
> > ## eigenquantTopic Author
> > 
> > thanks for your confirm
> > 
> > 
> > 


---

> ## yulonghui
> 
> I want to know What kind of data we can use for fine-tuning?
> 
> 
> 


---



* --- discussion numver 88, the number of votes :3 ---

# Deberta -> LGBM [1.30 LB]

**Rich Olson** *Sat May 11 2024 10:04:01 GMT+0900 (日本標準時)* (3 votes)

Just shared my Deberta-feature-extraction -> LGBM notebook here:

[https://www.kaggle.com/code/richolson/deberta](https://www.kaggle.com/code/richolson/deberta)

Score is 1.030 on the LB.

I train / submit on the same run.  Runtime is about 3 hours on P100.  Most of that is Deberta doing feature extraction (LGBM train / inference is comparatively fast).

Submission is probably about 90 minutes longer (since feature extraction needs to be done on test also).

I'm using deberta-base (presumably this would run faster with a smaller model).

One note - I'll typically do quick-test-runs with 1-5k prompts to see if things are generally working.  That was enough for TF-IDF to show some results.  For whatever reason - this produced zero results with Deberta.

Once I started training on 10k+ samples - then things started to converge for me.

So - if your Deberta model isn't doing anything - maybe try more data…

I also have a related kitchen-sink notebook that's currently scoring:

[https://www.kaggle.com/code/richolson/deberta-tf-idf-word2vec](https://www.kaggle.com/code/richolson/deberta-tf-idf-word2vec)





* --- discussion numver 89, the number of votes :2 ---

# QA: About Deadline

**Robert0921** *Sat Aug 03 2024 12:03:32 GMT+0900 (日本標準時)* (2 votes)

About Deadline, Do I just need to submit before FSD (Final Submission Deadline), or need to wait for public score to come out before FSD? Because this involves a difference of 8~9 hours running time…

Timeline

May 2, 2024 - Start Date.

July 29, 2024 - Entry Deadline. You must accept the competition rules before this date in order to compete.

July 29, 2024 - Team Merger Deadline. This is the last day participants may join or merge teams.

August 5, 2024 - Final Submission Deadline.



---

 # Comments from other users

> ## SeshuRaju 🧘‍♂️
> 
> 
> [@robert0921](https://www.kaggle.com/robert0921) need to wait for public score to come out before FSD, We will see private leaderboard once FSD finish.
> 
> 
> 


---



* --- discussion numver 90, the number of votes :2 ---

# Why I did not get the corresponding checkpoint when I continued training from the checkpoint and reset save_steps? My save_steps=5000 before, and now I changed it to 200, but after 200 steps, I did not get the corresponding checkpoint.

**KeShuang Liu** *Sun Jul 28 2024 21:09:52 GMT+0900 (日本標準時)* (2 votes)

training_args = TrainingArguments(

    output_dir=config.output_dir,

    overwrite_output_dir=True,

    report_to="none",

    num_train_epochs=config.n_epochs,

    per_device_train_batch_size=config.per_device_train_batch_size,

    gradient_accumulation_steps=config.gradient_accumulation_steps,

    per_device_eval_batch_size=config.per_device_eval_batch_size,

    logging_steps=10,

    eval_strategy="epoch",

    save_strategy="steps", 

    save_steps=200,        # 每5000步保存一次

    # eval_steps=2000, 

    optim=config.optim_type,

    fp16=True,

    learning_rate=config.lr,

    warmup_steps=config.warmup_steps,

    resume_from_checkpoint="/liukeshuang/lora_model/gemma_bnb_4_g8/checkpoint-2873"

)



---

 # Comments from other users

> ## Piotr Gabrys
> 
> [EDIT] It's uncertain whether this code solves the problem.
> 
> Hi! You can do it like this:
> 
> ```
> training_args = TrainingArguments(
> output_dir=config.output_dir,
> overwrite_output_dir=True,
> report_to="none",
> num_train_epochs=config.n_epochs,
> per_device_train_batch_size=config.per_device_train_batch_size,
> gradient_accumulation_steps=config.gradient_accumulation_steps,
> per_device_eval_batch_size=config.per_device_eval_batch_size,
> logging_steps=10,
> eval_strategy="epoch",
> save_strategy="steps",
> save_steps=200, # 每5000步保存一次
> # eval_steps=2000,
> optim=config.optim_type,
> fp16=True,
> learning_rate=config.lr,
> warmup_steps=config.warmup_steps
> 
> trainer = Trainer(
>         model=model,
>         args=training_args,
>         train_dataset=dataset['train'],
>         eval_dataset=dataset['test'],
>         tokenizer=tokenizer,
>     )
> 
> trainer.train("/liukeshuang/lora_model/gemma_bnb_4_g8/checkpoint-2873")
> 
> ```
> 
> reference: [https://github.com/huggingface/transformers/issues/7198](https://github.com/huggingface/transformers/issues/7198)
> 
> Hope that helps!
> 
> 
> 
> > ## KeShuang LiuTopic Author
> > 
> > Thanks for your reply, I will try
> > 
> > 
> > 
> > > ## Piotr Gabrys
> > > 
> > > Has it worked?
> > > 
> > > 
> > > 
> > > ## KeShuang LiuTopic Author
> > > 
> > > I used [@nbroad](https://www.kaggle.com/nbroad) method and it works fine.
> > > 
> > > 
> > > 


---

> ## Nicholas Broad
> 
> It's because you are resuming from checkpoint. It will use your old value when you resume. I think you can overwrite training_args.bin in your checkpoint to have the new values and it should work
> 
> 
> 


---

> ## Dlond Mike
> 
> same issue
> 
> 
> 


---



* --- discussion numver 91, the number of votes :2 ---

# Are We Really on the Right Track?

**Lorry Zou** *Sun Jul 21 2024 23:33:24 GMT+0900 (日本標準時)* (2 votes)

From the competition description:

"This challenge aligns with the concept of "reward models" or "preference models" in reinforcement learning from human feedback (RLHF). Previous research has identified limitations in directly prompting an existing LLM for preference predictions. These limitations often stem from biases such as favoring responses presented first (position bias), being overly verbose (verbosity bias), or exhibiting self-promotion (self-enhancement bias)."

Looks like the competition host encourage us to try reinforcement learning but everyone is still fine-tuning existing LLMs.🙂🙃



---

 # Comments from other users

> ## CPMP
> 
> RLHF is a supervised learning method.  Labels are provided by humans, and are quite similar to the labels we have in this competition.
> 
> Not sure what you suggest we do differently.
> 
> 
> 


---

> ## Dlond Mike
> 
> yep….cause it's really perform great.it's a game for rich.(GPU :))
> 
> 
> 


---

> ## chan peter
> 
> I tried out rlhf model and use the reward score as input and build a simple classifier, it work out great, but running the rlhf model is too time comsuing and I joined comp a bit late, don't have enough time to optimize it to pass the time limit.
> 
> 
> 


---



* --- discussion numver 92, the number of votes :2 ---

# LMSYS: Research Papers Relevant for this Competition

**C R Suthikshn Kumar** *Fri Jul 26 2024 13:21:46 GMT+0900 (日本標準時)* (2 votes)

Refer to the LMSYS - Chatbot Arena Human Preferences Predictions Competition:

[https://www.kaggle.com/competitions/lmsys-chatbot-arena/](https://www.kaggle.com/competitions/lmsys-chatbot-arena/)

Wishing all the best for participants in this competition. I am sharing useful reference papers, articles :

W Chiang et al., Chatbot Arena: An Open Platform for Evaluating LLMs by Human Preference, [https://arxiv.org/abs/2403.04132](https://arxiv.org/abs/2403.04132)
Chatbot Arena: Benchmarking LLMs in the Wild with Elo Ratings

by: Lianmin Zheng*, [https://lmsys.org/blog/2023-05-03-arena/](https://lmsys.org/blog/2023-05-03-arena/)
Introducing Hard Prompts Category in Chatbot Arena

by: Tianle Li, [https://lmsys.org/blog/2024-05-17-category-hard/](https://lmsys.org/blog/2024-05-17-category-hard/)
MSYS-Chat-1M: A Large-Scale Real-World LLM Conversation Dataset, [https://huggingface.co/datasets/lmsys/lmsys-chat-1m](https://huggingface.co/datasets/lmsys/lmsys-chat-1m)
A Survey on Human Preference Learning for Large Language Models

Ruili Jiang, et al, [https://arxiv.org/html/2406.11191v2](https://arxiv.org/html/2406.11191v2)
Align LLMs with Reinforcement Learning from Human Feedback: AI Learns Best with Rewards

by Maddie Lupu, [https://medium.com/@madalina.lupu.d/align-llms-with-reinforcement-learning-from-human-feedback-595d61f160d5](https://medium.com/@madalina.lupu.d/align-llms-with-reinforcement-learning-from-human-feedback-595d61f160d5)


---

 # Comments from other users

> ## Aadit Shukla
> 
> Thank you for sharing these valuable resources [@crsuthikshnkumar](https://www.kaggle.com/crsuthikshnkumar) and best of luck to all participants in the LMSYS competition!
> 
> 
> 


---

> ## Muhammad Ehsan
> 
> Great resources, [@crsuthikshnkumar](https://www.kaggle.com/crsuthikshnkumar) ! 
> 
> Your post provides valuable references for those diving into human preference predictions in chatbots. The papers and articles listed offer deep insights into evaluating and aligning LLMs with human preferences. Best of luck to everyone participating in the competition.
> 
> 
> 


---



* --- discussion numver 93, the number of votes :2 ---

# Can anyone share some trick about kaggle competitions?

**YEI0907** *Sat Jul 27 2024 01:54:10 GMT+0900 (日本標準時)* (2 votes)

Hello everyone, this is my first time competing on Kaggle. Here are some of my questions, and I really hope someone can answer them for me

How to perform hyperparameter optimization? Random method or Bayesian method?

Have you adopted cross validation methods for large language models such as Llama and Gemma. Should we choose the model with the lowest loss fold for inference after cross validation, or train the model on all data?

How to effectively avoid 'CUDA OUT of Memory'?, Sometimes my training code is consistent with some public notebooks, and even the config is consistent, but there are still "CUDA OUT of Memory" issues, even if the length is kept at 1024. In addition, my GPU is A100-80g

Is QLora really more effective than FB16 fine-tuning?

How to increase inference time more effectively

I would greatly appreciate it if someone could answer my question



---

 # Comments from other users

> ## justin1357
> 
> 
> In many competiiton you can use optuna to search hyperparameters automatically, but in this one, not. My solution is to tune them by hand and check if it will work better by experiment.
> Cross Val is great but we don't have so much money and time to do a 5-fold training, in this competition, the relation between cv and   lb is stable, so you can just use like 20% of full data as your val data.
> check your code, its more likely caused by bug.
> Yes in this competition.
> You mean 'reduce infer time'? There are some way to optimize your speed like flash-attn, deepspeed, and so on…
> 
> 
> > ## YEI0907Topic Author
> > 
> > thanks! good luck to  you ,my friend
> > 
> > 
> > 


---



* --- discussion numver 94, the number of votes :2 ---

# Larger model, better result?

**Dylan Liu** *Fri Jul 26 2024 18:25:10 GMT+0900 (日本標準時)* (2 votes)

I tried to train gemma2-27b but it's valid score is not better than that of 9b. What's your experience?



---

 # Comments from other users

> ## justin1357
> 
> Better is greater.. You can compare them in poe, and then you will find they are totally different. Zero Shot.
> 
> 
> 


---

> ## ShelterW
> 
> What method do you use？SEQ_CLS?
> 
> 
> 
> > ## Dylan LiuTopic Author
> > 
> > yes SEQ_CLS
> > 
> > 
> > 


---



* --- discussion numver 95, the number of votes :2 ---

# [Need help] How to custom Head for AutoModelForSequenceClassification with LoRA?

**Bao Loc Pham** *Sat Jul 20 2024 13:52:51 GMT+0900 (日本標準時)* (2 votes)

I've a model look like this

```
Gemma2ForSequenceClassification(
  (model): Gemma2Model(
    (embed_tokens): Embedding(256000, 3584, padding_idx=0)
    (layers): ModuleList(
      (0-41): 42 x Gemma2DecoderLayer(
        (self_attn): Gemma2SdpaAttention(
          (q_proj): Linear4bit(in_features=3584, out_features=4096, bias=False)
          (k_proj): Linear4bit(in_features=3584, out_features=2048, bias=False)
          (v_proj): Linear4bit(in_features=3584, out_features=2048, bias=False)
          (o_proj): Linear4bit(in_features=4096, out_features=3584, bias=False)
          (rotary_emb): Gemma2RotaryEmbedding()
        )
        (mlp): Gemma2MLP(
          (gate_proj): Linear4bit(in_features=3584, out_features=14336, bias=False)
          (up_proj): Linear4bit(in_features=3584, out_features=14336, bias=False)
          (down_proj): Linear4bit(in_features=14336, out_features=3584, bias=False)
          (act_fn): PytorchGELUTanh()
        )
        (input_layernorm): Gemma2RMSNorm()
        (post_attention_layernorm): Gemma2RMSNorm()
        (pre_feedforward_layernorm): Gemma2RMSNorm()
        (post_feedforward_layernorm): Gemma2RMSNorm()
      )
    )
    (norm): Gemma2RMSNorm()
  )
  (score): Linear(in_features=3584, out_features=3, bias=False)
)

```

After applied LoRA, the model look like this

```
PeftModelForSequenceClassification(
  (base_model): LoraModel(
    (model): Gemma2ForSequenceClassification(
      (model): Gemma2Model(
        (embed_tokens): Embedding(256000, 3584, padding_idx=0)
        (layers): ModuleList(
         ....
            )
            (mlp): Gemma2MLP(
              ....
            )
            ...
          )
        )
        (norm): Gemma2RMSNorm()
      )
      (score): ModulesToSaveWrapper(
        (original_module): Linear(in_features=3584, out_features=3, bias=False)
        (modules_to_save): ModuleDict(
          (default): Linear(in_features=3584, out_features=3, bias=False)
        )
      )
    )
  )
)

```

Because of score module is just a simple fully connected layer, I want to make it more complex,

I tried to replace the head like this

```
CustomGemmaForSequenceClassification(
  (model): GemmaModel(
    (embed_tokens): Embedding(256000, 3584, padding_idx=0)
    (layers): ModuleList(
      (0-41): 42 x GemmaDecoderLayer(
        ...
        )
        (mlp): GemmaMLP(
        ...
        )
        (input_layernorm): GemmaRMSNorm()
        (post_attention_layernorm): GemmaRMSNorm()
      )
    )
    (norm): GemmaRMSNorm()
  )
  **(score): Sequential(
    (0): Linear4bit(in_features=7168, out_features=3584, bias=True)
    (1): Linear(in_features=3584, out_features=3, bias=False)
  )**
)

```

But after applied peft and LoRA, there is an error 

```
p.requires_grad_(requires_grad)
RuntimeError: only Tensors of floating point dtype can require gradients

```

I already put lora module_to_save=["score"] like this [huggingface tutorial](https://huggingface.co/docs/peft/en/developer_guides/custom_models) but seem not working yet



---

 # Comments from other users

> ## CPMP
> 
> Why use LORA on a matrix of rank 3?
> 
> The classification head linear layer has a rank of at most 3 because its dimension is 3584x3. 
> 
> TL;DR it does not make sense to apply LORA to the classification head.
> 
> 
> 
> > ## Bao Loc PhamTopic Author
> > 
> > [@cpmpml](https://www.kaggle.com/cpmpml) 
> > 
> > thank for your comment, the rank 3 you mean is the number of class.
> > 
> > - Yes, I don't want to apply LORA to the classification head.
> > 
> > I just apply these code like the huggingface tutorial
> > 
> > ```
> > lora_config = LoraConfig(
> >     r=config.lora_r,
> >     lora_alpha=config.lora_alpha,
> >     # only target self-attention
> >     target_modules=config.target_modules,
> >     layers_to_transform=[i for i in range(42) if i >= config.freeze_layers],
> >     lora_dropout=config.lora_dropout,
> >     bias=config.lora_bias,
> >     task_type=TaskType.SEQ_CLS,
> > )
> > model = AutoModelForSequenceClassification.from_pretrained(
> >     config.checkpoint,
> >     num_labels=3,
> >     torch_dtype=torch.float16,
> >     device_map="auto",
> >     quantization_config=quantization_config
> > )
> > model.config.use_cache = False
> > model = prepare_model_for_kbit_training(model)
> > model = get_peft_model(model, lora_config)
> > print(model)
> > 
> > print(model.print_trainable_parameters())
> > 
> > ```
> > 
> > the AutoModelForSequenceClassification class will create a simple neural network with 3 output.
> > 
> > but I want to replace with CustomModelForSequenceClassification with my custom head.
> > 
> > 
> > 
> > > ## Ashwani
> > > 
> > > you can specify the target_modules in which you want to apply LoRA. target_modules=["query", "key", "value"] specifies that LoRA should only be applied to the attention modules, effectively excluding the classification head.
> > > 
> > > 
> > > 
> > > ## CPMP
> > > 
> > > 
> > > the rank 3 you mean is the number of class.
> > > 
> > > The rank is  the rank of the matrix. LoRA is about approximating a high rank matrix with a low rank matrix. That's the lora_r parameter of LoRA. 
> > > 
> > > What I am saying is that applying LoRA to the classification head only makes sense with lora_r smaller than 3.
> > > 
> > > 
> > > 


---



* --- discussion numver 96, the number of votes :2 ---

# Gemma2 9b's inference time is much longer that Llama3 8b?

**Dylan Liu** *Wed Jul 17 2024 15:55:30 GMT+0900 (日本標準時)* (2 votes)

With same submission code, my Llama3 8b model takes ~4h to finish the inference, but my Gemma2 9b takes ~8h. Are you experiencing the same?



---

 # Comments from other users

> ## Ashwani
> 
> I haven't seen such difference. For me its 25% more time in gemma than lamma. 
> 
> If you want to further reduce inference time, check dynamic padding for each batch. 😀
> 
> 
> 


---

> ## Sparsh Tewatia
> 
> 2 billion parameters more at work my friend.
> 
> 
> 
> > ## Dylan LiuTopic Author
> > 
> > 2 billion parameters? I thought it was 1b different. But even so, double inference time is still not much explainable.
> > 
> > 
> > 
> > > ## Sparsh Tewatia
> > > 
> > > gemma always claims less parameter if you count it shows 10.2 billion parameters , also LLAMA 3 uses grouped query attention , and has around 120 K tokens in tokenizer while Gemma uses self attention and has 250 K tokens in tokenizer which can explain the difference in speed.
> > > 
> > > 
> > > 


---

> ## Yichuan Gao
> 
> I would check the data type for both weights and compute_dtype. If you are using bfloat16 in compute, it will be MUCH slower since T4 does not support bfloat16, and need to emulate it by other methods. In my experience, Gemma2 9b and Mistral 7b inference time does not have much a difference (3~4h range), provides using 4bit weights and float16 dtype.
> 
> 
> 


---

> ## Valentin Werner
> 
> For me, also training time with same parameters is 50% slower than Llama3-8b which seems insane. But its all in the architecture, as Sparsh pointed out.
> 
> 
> 
> > ## Robert0921
> > 
> > For LoRa, even though Gemma2 is more accurate than Llama3, I was unable to achieve better results due to the 9-hour time limit.
> > 
> > 
> > 


---

> ## Robert0921
> 
> Not only inference, but also training takes longer, because 9b>8b？
> 
> 
> 


---



* --- discussion numver 97, the number of votes :2 ---

# Is label smoothing beneficial in LLM fine-tuning?

**Yichuan Gao** *Sat Jul 13 2024 12:02:54 GMT+0900 (日本標準時)* (2 votes)

I'm using LoRA to fine-tune a Gemma2ForSequenceClassification model.

I'm wondering if add label smoothing is a good or bad thing in this process. Since if I add smoothing of 0.2 (i.e., label is [0.8, 0.1, 0.1] ), I'm getting a eval_loss higher than LB score (0.98 vs 0.96), maybe smoothing made my model less confident than it could be?

Could anyone share some experience on this topic? Would you add it, and if you do, how much is a sweet spot?



---

 # Comments from other users

> ## Valentin Werner
> 
> Normally if you are doing a task with < 60% accuracy and try to minimize loss, label smoothing should be helping, as its better to have less confident but correct classification rather than super confident wrong predictions. However, if your model is well calibrated without label smoothing, you should simply not use it. It helped a lot in my earlier experiments with DeBERTa though..
> 
> 
> 
> > ## Yichuan GaoTopic Author
> > 
> > Thanks for this information! I'll try to apply less smoothing now :)
> > 
> > 
> > 


---

> ## yechenzhi1
> 
> Same here, label smoothing is not beneficial for me.
> 
> 
> 


---



* --- discussion numver 98, the number of votes :2 ---

# Time constraint for private leaderboard [Solved]

**raconion** *Fri Jul 05 2024 11:15:47 GMT+0900 (日本標準時)* (2 votes)

There are roughly 25,000 rows in the test set. Among them, 26% are used for public lb while the rest 74% are used for private lb. 

Since in Overview section, the time constraint is 9 hrs, does this mean that our notebook has to finish the inference for 74%*25,000 =18,500 rows in the test set? Or this time constraint is for public lb and will be scaled according to the number of rows when it comes to private lb?

[@addisonhoward](https://www.kaggle.com/addisonhoward) [@mylesoneill](https://www.kaggle.com/mylesoneill) Would really appreciate if you can clarify this!

Update:

Our notebook will be run for all 25k rows but only 26% shown on public lb. Thanks for the comment [@lizhecheng](https://www.kaggle.com/lizhecheng) 

This comment also clarify this issue: [link](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/516995#2904512)



---

 # Comments from other users

> ## Enter your display name
> 
> As long as you can see your public score, your private score has also been calculated, but you just can't see it for now. Thus you don't need to worry about that.
> 
> 
> 
> > ## jiangli59
> > 
> > I vote for that. Is it possible to extend the time budget over 9 hrs? Or, Do we have other opinions to solve that? My code is extremely overwhelmed for the inference budget.  
> > 
> > 
> > 
> > > ## raconionTopic Author
> > > 
> > > I don't think the time constraint can be extended unless the competition host decides so. There are way arounds though such as all kinds of efficient inference techniques.
> > > 
> > > 
> > > 


---



* --- discussion numver 99, the number of votes :2 ---

# Submission Scoring Error

**RomanZubarev** *Wed Jun 12 2024 20:49:41 GMT+0900 (日本標準時)* (2 votes)

Hi! I'm a newbie and it's my first time participating in a competition here. Can anyone tell me why I get "Submission Scoring Error"? Everything seems to be under the rules and expectations of the result.

[2024-06-12 14-44-23.png](https://storage.googleapis.com/kaggle-forum-message-attachments/2868474/20808/2024-06-12 14-44-23.png)

---

 # Comments from other users

> ## Ahmad Al-Husainy
> 
> Was the notebook execution successful, or did it fail? If it succeeded, the only other possible reason I can think of, aside from what other Kagglers mentioned about probabilities summing up to more than one, could be the data format in the columns . If the notebook failed, you should check the execution logs, which will show you where it failed. 
> 
> 
> 


---

> ## Valentin Werner
> 
> You can try setting index=False during saving the csv, that caused problems for me before I think.
> 
> Is it because (winner_model_a + winner_model_b + winner_tie) > 1?
> 
> I don't think this should matter, as the log loss implementation is a wrapper for sklearn, where this is not an issue from my experiments
> 
> 
> 


---

> ## Masayuki Takahashi
> 
> Is it because (winner_model_a + winner_model_b + winner_tie) > 1?
> 
> 
> 
> > ## Anya
> > 
> > Good remind! I found my submission data has this problem.
> > 
> > 
> > 


---



* --- discussion numver 100, the number of votes :2 ---

# Download Llama3 Models from Kaggle?

**Valentin Werner** *Mon Jun 17 2024 12:41:39 GMT+0900 (日本標準時)* (2 votes)

Is there a way for me to download the Llama3 Models that were trained by others from Kaggle? I am talking about the model that is used in all the top scoring public notebooks. When I click on the dataset, I only see a placeholder file with about 30 MB of data.



---

 # Comments from other users

> ## Kishan Vavdara
> 
> They are lora weights, you can take llama-3 model from kaggle and add lora weights for further training/inference. 
> 
> 
> 
> > ## Valentin WernerTopic Author
> > 
> > Ah, I have never used lora weights before like this. Thank you for the clarification!
> > 
> > 
> > 


---



* --- discussion numver 101, the number of votes :2 ---

# Replacing response A and response B for Data Augmentation

**Takamichi Toda** *Wed Jun 05 2024 09:29:20 GMT+0900 (日本標準時)* (2 votes)

The current approach in the public code often creates features from responses A and B and uses these to train classifiers. I thought that a simple data augmentation could be achieved by swapping responses A and B and the winner labels.

However, it not works.

|  | Local | Public |
| --- | --- | --- |
| baseline | 0.997 | 1.012 |
| Augument by replace A/B | 1.011 | 1.025 |

My CV strategy is a simple one-holdout, and so far it correlates well with the Public LB ([reference](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/500031#2824772)).

It may be that whether the response is A or B is also an important feature. I had seen a thread discussing bias in evaluation depending on whether the response is A or B, but it seems to have disappeared (probably [here](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/507091)).



---

 # Comments from other users

> ## Lisa DunlapCompetition Host
> 
> Not sure how helpful this is, but position bias is a known phenomenon in both humans and LLMs: both tend to favor the first answer they are presented with. We look at this in the [original LLM as a judge paper ](https://arxiv.org/abs/2306.05685) if you want some concrete numbers of how prevalent this is 
> 
> 
> 


---

> ## Valentin Werner
> 
> My assumption is that by simply swapping, you are not creating new value for the model to learn. You are instead basically training those rows twice.
> 
> Questions:
> 
> 1) with what percentage of samples are you augmenting? If you only do 10-20% you are just making the model overfit / learn more about those samples. There might be an argument to do 100% of samples to make the model learn that resp A or B literally does not matter! (even though this might not reflect reality)
> 
> 2) are you also doing the swap with ties (keeping the tie label)? If not, you introduce class imbalance and ties are less likely to be predicted.
> 
> 
> 
> > ## Takamichi TodaTopic Author
> > 
> > Thank you for the comment.
> > 
> > 1)
> > 
> > It's 100%. By the way, I am using DeBERTa, and I conducted experiments to enable the model to know which sentence is A and which is B by adding special tokens, but it was not very effective (only a slight improvement).
> > 
> > 2)
> > 
> > The label for "tie" remains "tie" even after swapping.
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > So If you do 100%, you basically just train two epochs at the price of one. This will effect lr scheduling etc.
> > > 
> > > Did you also tune parameters in your experiment (e.g., warm up ratio or epochs)
> > > 
> > > 
> > > 
> > > ## Takamichi TodaTopic Author
> > > 
> > > You may be right.
> > > 
> > > We tried three different patterns for the learning rate (smaller is better).
> > > 
> > > 
> > > 


---



* --- discussion numver 102, the number of votes :2 ---

# predict the model of the response to to a classification?

**Lee** *Sun May 26 2024 18:24:03 GMT+0900 (日本標準時)* (2 votes)

Hello, I'm new to Kaggle and I've got an idea: What if we shift from simply evaluating responses to a 3-class classification, to a  64-class classification? Here's the plan:

First, use our training data to train a classification model. This model will help us predict which among the 64 models a given response belongs to.

Then, during the inference phase, armed with our trained classifier, we'll categorize each response into one of the 64 model types.

With this information in hand, we can ascertain which two models are in competition. Leveraging the training dataset as our prior knowledge, we'll then proceed to predict the likely winner between these two models.

[Translated from chatGPT] Sorry for your uncomfortable reading, I am not a naive English speaker🙏



---

 # Comments from other users

> ## Valentin Werner
> 
> I think this can be a valuable proxy or feature for prediction. But you should keep in mind that the best model had ~65% winrate, so even if you know the model, it is difficult to predict whether it will win.
> 
> As such, I can imagine that this is one feature among text embeddings or the length feture. But predicting the model that wrote a response is similar difficult to predicting the win directly. You will have less training data per class etc.
> 
> I think a similar strategy was also proposed in the Detect AI Generated Text Competion.
> 
> 
> 
> > ## Ivan Vybornov
> > 
> > Model of a response is an immensely valueable feature. Tried adding it to the lgbm locally: a few features like length of prompt and responses alongside with model name gives a score of around 0.99 with CV. 
> > 
> > Though I am concerned that new models might appear in the private set (not sure if it is a reasonable concern).
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > I dont think it is a reasonable concern. If you are able to reliably predict the model, than a new model will likely fall into the "next best" category. It would probably reduce score compared to if you know all models but you would likely still gain. 
> > > 
> > > also from my knowledge the model distribution seems not immensely imbalanced to the point where only a few responses exist for a model. Therefore, I imagine this would not be the case
> > > 
> > > 
> > > 


---



* --- discussion numver 103, the number of votes :2 ---

# Easily Visualize and Compare Prompt, Response and Winner

**Nazim Cherpanov** *Mon May 27 2024 18:42:02 GMT+0900 (日本標準時)* (2 votes)

## Introduction:

When dealing with conversational AI datasets, it's crucial to grasp the quality of the responses produced by various models. In this conversation, I will introduce a useful function that enables you to easily visualize and compare the responses for a specific prompt, as well as the top-performing model.

## Function Overview:

The function get_info_by_id(index) takes an index as input and retrieves the corresponding prompt, responses from two models (Model A and Model B), and the winner from the Kaggle dataset. It then displays the information in an easy-to-read format.

## Code Snippet:

```
train_path = '/kaggle/input/lmsys-chatbot-arena/train.csv'
train = pd.read_csv(train_path, index_col='id').reset_index(drop=True)

ef get_info_by_id(index):
     if index not in list(train.index):
         display("index not in train")
     else:
        print(f"\n{'*'*10} Prompt {'*'*10}\n")
        display(train.iloc[index]['prompt'])

        print(f"\n\n{'*'*10} response A {'*'*10}\n")
        display(train.iloc[index]['response_a'])

        print(f"\n\n{'*'*10} response B {'*'*10}\n")
        display(train.iloc[index]['response_b'])

        print(f"\n\n{'*'*10} Winner {'*'*10}\n")
        if train.iloc[index]['winner_model_a'] == 1:
            display('Model A')
        elif train.iloc[index]['winner_model_b'] == 1:
            display('Model B')
        else:
            display('Tie')`

get_info_by_id(3)

```

## Usage:

To use the function, simply call get_info_by_id() with the desired index from the train dataset. For example, get_info_by_id(3) will display the prompt, responses, and the winner for the row with index 3.

## Happy Kaggling!





* --- discussion numver 104, the number of votes :2 ---

# how can I load a pretrained model with internet off

**Dirk N** *Tue May 14 2024 23:56:23 GMT+0900 (日本標準時)* (2 votes)

It seems I cannot use pip install, what is the best way to load a pretrained model with internet off?



---

 # Comments from other users

> ## RobsonDSP
> 
> I tried download a model from huggingface but until now is not working. I cloned the model to my local machine and uploaded it to my private space here on Kaggle as dataset. I uploaded all files, config.json, tf_model.h5, vocab.json and others. I tried to load them using the code bellow:
> 
> from transformers import AutoModelForSequenceClassification
> 
> from transformers import TFAutoModelForSequenceClassification
> 
> from transformers import AutoTokenizer, AutoConfig
> 
> import numpy as np
> 
> from scipy.special import softmax
> 
> MODEL = f"/kaggle/input/pretrained-model-from-huggingface/"
> 
> tokenizer = AutoTokenizer.from_pretrained(MODEL)
> 
> config = AutoConfig.from_pretrained(MODEL)
> 
> model = AutoModelForSequenceClassification.from_pretrained(MODEL)
> 
> Now I'm getting the following error message:
> 
> OSError: You seem to have cloned a repository without having git-lfs installed. Please install git-lfs and run git lfs install followed by git lfs pull in the folder you cloned.
> 
> When I run the commands in my machine it starts to download a huge file. I stopped at 1GB and the progress bar at 0%. I intended to upload this file to my account on Kaggle too but I stopped because I'm probably doing something wrong. 
> 
> I really don't know what to do now because I cannot enabled the internet access.
> 
> 
> 


---

> ## Muhammad Tariq Pervez
> 
> [@dirknbr](https://www.kaggle.com/dirknbr), Kaggle competition rules don't impose restrictions to download a model and use it. In Kaggle competitions, "disabling internet" means that the code you submit to Kaggle for scoring is executed in an environment that does not have access to the internet. Ensure your submission does not include any code that requires internet access, such as downloading data from external URLs or accessing online APIs.
> 
> 
> 


---

> ## Kishan Vavdara
> 
> Keep train and inference separate notebooks, download/load/train model in train notebook and import it in inference notebook. 
> 
> 
> 


---

> ## djchen
> 
> You can download the pertrained model on huggingface and upload it to Kaggle as a model, then you can load such pertrained model in your notebook.
> 
> 
> 


---

> ## Simon Veitner
> 
> You can clone the huggingface repository and upload it as a dataset. There are many examples how to load it from there.
> 
> Also you should check, if somebody else did it already :)
> 
> 
> 


---



* --- discussion numver 105, the number of votes :2 ---

# I have started hallucinating because of data :D

**Kuldeep Rathore** *Tue May 14 2024 19:58:09 GMT+0900 (日本標準時)* (2 votes)

Only hallucinating comments are welcome on this thread ☺️



---

 # Comments from other users

> ## G John Rao
> 
> Yeah, it's funny but this goes under the pre-processing part
> 
> 
> 


---

> ## kheder yazgi
> 
> same models?
> 
> 
> 


---



* --- discussion numver 106, the number of votes :2 ---

# [New Starter] 3 texts + Huggingface

**Heroseo** *Sun May 05 2024 05:16:42 GMT+0900 (日本標準時)* (2 votes)

I shared a new notebook for Huggingface users.

This notebook uses huggingface and uses all three texts in the tokenizer.

- prompt, response_a, response_b

V3 - add truncate_text - but score got a little worse

- link: [[Train] LMSYS / Deberta-v3 meets Huggingface](https://www.kaggle.com/code/piantic/train-lmsys-deberta-v3-meets-huggingface/notebook)



---

 # Comments from other users

> ## Nicholas Broad
> 
> your model only predicts label 1?
> 
> 
> 
> > ## Valentin Werner
> > 
> > I guess you can save some inference time on those predictions 😉
> > 
> > 
> > 
> > ## HeroseoTopic Author
> > 
> > thank you for telling me. I will check again later and update.
> > 
> > p.s. But now I've run out of Kaggle GPU time. 🥲
> > 
> > 
> > 


---



* --- discussion numver 107, the number of votes :1 ---

# How crazy！Top 1: LB 707 ——> 663!

**Sun And Ray** *Sun Aug 04 2024 09:55:22 GMT+0900 (日本標準時)* (1 votes)

I'm not sure how this guy managed to quickly move from LB: 880 to LB: 707, and then to LB: 663. I suspect his training plan is similar to those of other teams in the gold tier, but the training data might be very different!

Additionally, in a discussion thread titled “Suspicious Surge of Novice Accounts on the Leaderboard,” I initially thought these "newcomers" wouldn’t affect the Top 100, but this morning when I checked the leaderboard, I found myself around 80th place. I admit my guess was wrong.

Lastly, my teammates and I are discussing whether to make our training and inference solutions public today or tomorrow in order to counter these "potentially cheating newcomers."



---

 # Comments from other users

> ## CPMP
> 
> Don't publish your solution before competition end! 
> 
> 
> 


---

> ## heartkilla
> 
> Please do not publish your solution before the deadline. This will do nothing but create unnecessary turbulence on the leaderboard by giving advantage to those who have enough time to incorporate your ideas. This imbalance will be even more amplified giving the time zone difference across the participants.
> 
> 
> 
> > ## Sun And RayTopic Author
> > 
> > Our team has spent a lot of money renting GPU resources, but it seems that our investment has yielded unequal returns.
> > 
> > 
> > 
> > > ## XXX
> > > 
> > > sorry to heard that🥺
> > > 
> > > 
> > > 
> > > ## heartkilla
> > > 
> > > That is unfortunate but does not justify publishing high scoring submissions 2 days before the deadline.
> > > 
> > > 
> > > 


---

> ## Kamau
> 
> So sad! This leaves me thinking of all the hours, sweat, and tears some of us have put into this. It may not look like it, but this is truly disheartening. It almost explains how I moved from the top 100 to lower ranks on the leaderboard in barely a week. The situation reminds of the quote:
> 
> "What's the point of fighting my way up the mountain when someone else is just going to come up the easy way?"
> 
> ~ from The Key of the Titans
> 
> 
> 


---

> ## Ya Xu
> 
> Have faith, I believe Kaggle will deal with cheaters just like they did recently.
> 
> 
> 
> > ## Sun And RayTopic Author
> > 
> > I hope so!
> > 
> > 
> > 


---

> ## SeshuRaju 🧘‍♂️
> 
> 
> Lastly, my teammates and I are discussing whether to make our training and inference solutions public today or tomorrow in order to counter these "potentially cheating newcomers."
> 
> -- As per Kaggle policy, top notebooks are not allow to release in last 7 days. I surprise, won't see that message now.
> 
> 
> 


---

> ## Victor Lu
> 
> This competition is really becoming increasingly unpredictable. I’m very curious to see what changes will occur on the leaderboard after the competition ends. 
> 
> 
> 


---

> ## Dlond Mike
> 
> sadT.T,i thought it woule be my first time i could get a medal….
> 
> 
> 


---

> ## XXX
> 
> Hi [@sunandray](https://www.kaggle.com/sunandray), may i ask how many "newcomers" do you think in top 100?🤔
> 
> 
> 
> > ## Sun And RayTopic Author
> > 
> > I'm not sure how many teams there are in the medal zone, as my focus has primarily been on the silver zone. In the silver zone, I feel there are at least 10 teams that might be cheating. This is because I've noticed some teams were around 938 on the LB a few days ago, and suddenly they are around 900 today.
> > 
> > 
> > 
> > > ## XXX
> > > 
> > > So, by cheating, do you mean that these teams use the same leaked data as the first one?
> > > 
> > > 
> > > 
> > > ## Enter your display name
> > > 
> > > No, I think he means that they share their solutions privately.
> > > 
> > > 
> > > 
> > > ## XXX
> > > 
> > > thank you 
> > > 
> > > 
> > > 


---



* --- discussion numver 108, the number of votes :1 ---

# 1h -> .707! Is the dataset leaked?

**Roschild.Rui** *Sun Aug 04 2024 04:36:14 GMT+0900 (日本標準時)* (1 votes)

Unbelievable! I have great desire to know what’s really help and how could the master achieve this after the competition ending



---

 # Comments from other users

> ## sayoulala
> 
> I believe it's very likely. My training set loss couldn't even reach that score. As of now, his score has risen to 0.6 again… I hope Kaggle officials can handle this matter fairly.
> 
> 
> 
> > ## Valentin Werner
> > 
> > Training loss doesn't even get close to it. Even ignoring all remarks on speed of submission, I dont think a model that could run inference in an hour (likely the size of deberta Base or smaller), is even  able to overfit this hard on a problem this complex. 
> > 
> > Not going to lie, I would love him to have come up with some insane solution.
> > 
> > 
> > 
> > > ## Cody_Null
> > > 
> > > I feel the same way but I would be completely shocked haha
> > > 
> > > 
> > > 
> > > ## sayoulala
> > > 
> > > If he can come up with a better solution, the whole world will thank him. But if he's exploiting some loopholes, that would be truly disappointing.
> > > 
> > > 
> > > 


---

> ## Cody_Null
> 
> I hope he doesn’t share before competition end. Because if he does the comp is ruined lol 
> 
> 
> 


---



* --- discussion numver 109, the number of votes :1 ---

# postprocess data that have [null] responses

**ano** *Fri Aug 02 2024 22:59:02 GMT+0900 (日本標準時)* (1 votes)

Training dataset have some data whose responses for both A and B are [null].

[https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/502303](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/502303)

Therefore, I implemented the code to postprocess null data, assuming the same percentage of winner_model_a, winner_model_b and winner_tie for the train and test dataset. However, the score got worse a little bit. Has anyone had the same experience?



---

 # Comments from other users

> ## Valentin Werner
> 
> I think the problem we are facing is how random the results for these samples are. 
> 
> Guessing average distributions for these samples might be a good approach (if actually both are null), but I think you are focusing on a very niche problem for your post-processing. On the 57k training samples, 19 samples fit into this pattern according to the post you link. Assuming same distribution in the dataset you are doing postprocessing for 10 samples. And 2-3 of which would be in the public lb.
> 
> As the 19 samples in the training set are not a representative sample size to start with, it is quite likely that you should just "trust your model". 
> 
> 
> 
> > ## anoTopic Author
> > 
> > I appreciate your detailed explanation. It seems like the randomness of the results for these samples is indeed a significant factor. The null data in the test dataset, which you estimated to be only 2-3 affecting the public leaderboard, is just too small.
> > 
> > In this case, it might be ineffective to assume the same distribution based on these few samples.
> > 
> > 
> > 


---



* --- discussion numver 110, the number of votes :1 ---

# How many epochs do people usually choose when fine-tuning?

**KeShuang Liu** *Sat Jul 27 2024 22:40:05 GMT+0900 (日本標準時)* (1 votes)

As a beginner, I am eager for a score increase, but reality keeps hitting me. If we train for 1 epoch and 2 epochs with the same parameters and configuration respectively, will training for 2 epochs produce the same results as training for 1 epoch at the end of the first epoch, or will it be slower to become proficient?



---

 # Comments from other users

> ## Valentin Werner
> 
> There are a bunch of different questions in here. First, lets losely define what an epoch is: An epoch is a Forward and Backward Propogation through your whole Training dataset; this means, that your model saw all your training data once. Two epochs mean it saw all the training data twice.
> 
> This means, that the results of one epoch training and two epochs training will be different. However, the results of epoch 1 in a single epoch training should be around the same as the results of epoch 1 in a two epoch training (assume no learning rate scheduling).
> 
> What is a go-to number of epochs? The go-to number I see most often when finetuning pretrained models is three. However, for larger models (with peft) this value tends to be lower (for example two) and for larger datasets this value tends to be lower too. This is because the model learns more information within a single epoch.
> 
> Now, the last important note on epochs is learning rate scheduling. Often learning rates are scheduled to reduce learning rate in later epochs. Lets assume the learning rate decreased linear from start of the first epoch until the end of the third epoch. This means that the model will overfit less in the second and even less in the third epoch, while still being able to learn nuances about the training data, that can improve your score. This also means that a single epoch training with lr scheduling will have different results than a two epoch training with scheduling, as the learning rate will hit 0 much earlier in the first case. 
> 
> In general, transformer trainings are non-deterministic and you need to set a seed if you want to replicate exact results.
> 
> 
> 
> > ## KeShuang LiuTopic Author
> > 
> > Thank you for your reply.I have learned a lot from it, I will keep trying more.
> > 
> > 
> > 


---

> ## Mr.T
> 
> When I train with two epochs, I experience severe overfitting.
> 
> 
> 


---

> ## xiaotingting
> 
> The more data there is, the smaller the epochs need to be fine-tuned. Otherwise, the larger the epochs need to be fine-tuned.
> 
> 
> 


---

> ## KeShuang LiuTopic Author
> 
> Can someone help me clarify my doubts
> 
> 
> 


---



* --- discussion numver 111, the number of votes :1 ---

# question about the quota of GPU

**Dlond Mike** *Mon Jul 29 2024 20:57:34 GMT+0900 (日本標準時)* (1 votes)

Does submission take the quota of GPU?if so,how much quota it will take?



---

 # Comments from other users

> ## CPMP
> 
> saving your notebook runs it again using your quota. Once this is done, submitting does not use your quota anymore.
> 
> 
> 


---

> ## Yi-Fu Chen
> 
> ```
> import os
> if os.getenv('KAGGLE_IS_COMPETITION_RERUN'):
>     pass
> else:
>     raise SystemExit
> 
> ```
> 
> Adding the above code at the front of the submitted notebook will quickly close the trial run notebook and retain the scored run.
> 
> 
> 


---

> ## Ravi Ramakrishnan
> 
> I usually submit to code competitions in a script. I use the below to ensure I don't use up my GPU quotas during my dummy LB submission- 
> 
> ```
> import pandas as pd
> sub_fl = pd.read_csv(.......submission.csv)
> 
> if len(sub_fl) <=10:
>     print(f"Submitting the dummy file")
>     sub_fl.to_csv("submission.csv", index = None)
> 
> else:
>     ....... (your script)
> 
> ```
> 
> [@dlondmike](https://www.kaggle.com/dlondmike) best of luck!
> 
> 
> 


---

> ## SeshuRaju 🧘‍♂️
> 
> [@dlondmike](https://www.kaggle.com/dlondmike) for scorning won't take GPU quota, but for generating the submitted notebook version ( even after submit, you can cancel the notebook, so GPU quota can be saved )
> 
> 
> 
> > ## Valentin Werner
> > 
> > From what I know (and experienes last week), the "save" notebook (not submit) also doesnt crash if it goes above quota. I think I ended last week on 32/30 hrs by accident 😃
> > 
> > 
> > 


---

> ## bao
> 
> There are two notebooks running when submitted. The scoring notebook does not use GPU quota, while the other one does.
> 
> 
> 


---



* --- discussion numver 112, the number of votes :1 ---

# Finetuned --> Quantized vs Quantized--> Finetuned

**Varun Jagannath** *Fri Jul 26 2024 23:22:44 GMT+0900 (日本標準時)* (1 votes)

Which approach is performing better in this competition: fine-tuning a model like Llama 3 and then quantizing it, or taking a low-bit quantized model and fine-tuning it on the dataset ?



---

 # Comments from other users

> ## Valentin Werner
> 
> I hope somebody who tested it actually answers and knows better than me. My intuition is that Finetune -> Quantize should be better, as the finetuning is more precise. Obviously there is also the argument that this precision is quantized later anyways and maybe training in a quantized way makes sure your val / lb is more consistent
> 
> 
> 
> > ## Pranshu Bahadur
> > 
> > Ok so I kind of tested this scenario a bit and I agree with your hypothesis, when I trained gemma 2 9b on bfloat16 training loss went down to 0.44 (definitely a sign of overfitting). I think quantization should be done post-training.
> > 
> > 
> > 
> > ## Maksim Metelskii
> > 
> > LoRa adapters (which are 16 or 32 bit) trained on quantized model may help to fix inaccuracy stemmed from quantization. Like they address both quantization and new specific task inaccuracy. ChatGPT says Quantized--> Finetuned may be more beneficial for accuracy. But really need to be tested though
> > 
> > 
> > 
> > ## Varun JagannathTopic Author
> > 
> > My observation is that earlier TPU train notebook which was published got nearly around 0.98 LB and the latest 0.94LB of Training and Inference with unsloth gemma 2. So really wanted to understand if the quantized followed fine tuning is performing well in this competition. 
> > 
> > 
> > 


---

> ## xiaotingting
> 
> I think fine-tuning after quantization is better because it can make up for the loss caused by quantization. Maybe fine-tuning the quantized model and quantizing after training require different learning rates.
> 
> 
> 


---



* --- discussion numver 113, the number of votes :1 ---

# Am I overfitting?

**KeShuang Liu** *Sat Jul 27 2024 12:07:19 GMT+0900 (日本標準時)* (1 votes)





---

 # Comments from other users

> ## Valentin Werner
> 
> Overfitting is best analyzed in combination with validation loss. If you validation loss has a similar drop to your training loss (which I guess would win the competition at these scores), you are not overfitting. In general, if training loss goes down while validation loss is either plateauing or going back up, you are likely overfitting.
> 
> Another way of estimating overfitting is to look at what performance you expect and what you see on the train loss. We would not expect the model to go to .800 or even below it - therefore, it is likely to overfit. However, this does not mean that the model was best before this downward shift at steps 550 - you should use a validation score to evaluate how well the model predicts on unseen data
> 
> 
> 
> > ## KeShuang LiuTopic Author
> > 
> > Yes, but my validation set can only be calculated after this epoch is completed, and it takes a long time, so I am considering whether to stop it directly
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > You can set how often you want to evaluate. It does indeed take a lot of time, so I think evaluating 2-4 times is feasible.
> > > 
> > > 
> > > 
> > > ## KeShuang LiuTopic Author
> > > 
> > > Yes, my model should be overfitting. Its loss on the validation set is 0.99
> > > 
> > > 
> > > 


---

> ## xiaotingting
> 
> It has to be combined with the indicators of the validation set. If the loss on the validation set is large, but very low on the training set, it is overfitting, and you can consider adding regularization such as weight decay. If the loss on both the validation set and the training set is low, it means the model is effective.
> 
> 
> 
> > ## KeShuang LiuTopic Author
> > 
> > The next validation metric will be calculated in a few hours, and I am considering whether to abandon this training directly
> > 
> > 
> > 


---

> ## Rise_Hand
> 
> Wow so Crazy! 600 epochs !!! Which kind of model you are using 
> 
> 
> 
> > ## KeShuang LiuTopic Author
> > 
> > steps,haha
> > 
> > 
> > 


---

> ## AYUSH KHAIRE
> 
> [@liukeshuang](https://www.kaggle.com/liukeshuang) yes about 580 to 600 you are overfitting. 
> 
> 
> 
> > ## KeShuang LiuTopic Author
> > 
> > Then I probably don't need to continue training now
> > 
> > 
> > 


---



* --- discussion numver 114, the number of votes :1 ---

# Is it possible to use gemma-2-27B with vLLM?

**yechenzhi1** *Tue Jul 23 2024 00:34:19 GMT+0900 (日本標準時)* (1 votes)

Inspired by [@cdeotte](https://www.kaggle.com/cdeotte)'s great [work](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/521294), I'm trying to use gemma-2-27B with vLLM. First I use GPTQmodel to quantinize it to 4-bit, then use vLLM-0.5.2 to do the infer. But we have to use flashinfer as the backend because of gemma-2's logits capping, then the problem comes, it's said flashinfer only supports GPU with compute [capability >= 8.0](https://github.com/vllm-project/vllm/issues/6173#issuecomment-2214759644), and T4 is 7.5. So is gemma-2-27b impossible for this competition?



---

 # Comments from other users

> ## Yixiao Yuan
> 
> I think we can't run gemma-2 with vLLM, but we can run it by huggingface. vLLM is much better for generation task due to PagedAttention. However, if we only generate one token or use classification head (we don't need KV cache in such cases), the performance should be similar.
> 
> 
> 
> > ## yechenzhi1Topic Author
> > 
> > bad news here, it seems only vllm/sglang can infer [quantized gemma-2-27b](https://github.com/ModelCloud/GPTQModel/issues/140#issuecomment-2242221690) correctly right now. 
> > 
> > 
> > 
> > ## yechenzhi1Topic Author
> > 
> > But thanks! I'll try it anyway!
> > 
> > 
> > 
> > > ## beanpotato
> > > 
> > > Could you share if you can run gema-2-27b with vLLM?🥰
> > > 
> > > 
> > > 
> > > ## yechenzhi1Topic Author
> > > 
> > > No, T4 GPU doesn't support FlashInfer. I stopped trying gemma-2-27B after a few days.
> > > 
> > > 
> > > 


---

> ## ShelterW
> 
> Is it possible to use gemma-2-27B with vLLM now?
> 
> 
> 
> > ## Somesh88
> > 
> > I've been trying to use gemma 2 with vllm the weights over kaggle doesn't contain config file. If I try to load it form transformers then I have to keep internet access enabled which is not allowed in submission. have you found any workround for this? 
> > 
> > 
> > 
> > > ## Kishan Vavdara
> > > 
> > > you can create kaggle dataset of configs, packages, weights, etc. and add to your inference notebook, then you can use it without enabling internet. 
> > > 
> > > 
> > > 


---



* --- discussion numver 115, the number of votes :1 ---

# elo modelling?

**kawaii** *Fri Jul 26 2024 23:17:19 GMT+0900 (日本標準時)* (1 votes)

i believe we dont have info on which model reponses we are looking at during test times, did anyone try modelling a mapping between the responses and the model it came from using the training data we have. Basically guessing which model the response came from. Do you think such a model will be very noisy? 





* --- discussion numver 116, the number of votes :1 ---

# Why are cv and lb badly mismatched

**Rabbit** *Fri Jul 26 2024 13:51:44 GMT+0900 (日本標準時)* (1 votes)

I got acv of0.927 and lb of 0.960 in local training

Training notebook:[https://www.kaggle.com/code/shelterw/training-llama3-8b-4-bit-qlora-sft](https://www.kaggle.com/code/shelterw/training-llama3-8b-4-bit-qlora-sft)

Inference notebook:[https://www.kaggle.com/code/shelterw/sft-llama-3-8b-inference](https://www.kaggle.com/code/shelterw/sft-llama-3-8b-inference)





* --- discussion numver 117, the number of votes :1 ---

# Has anyone used Google cloud TPUs ?

**JamshaidSohail** *Thu Jul 18 2024 19:54:51 GMT+0900 (日本標準時)* (1 votes)

Hi. Guys has anyone used Google Cloud TPUs ? If yes, can someone share some link for using them without any difficulty. 



---

 # Comments from other users

> ## The-Hai Nguyen
> 
> I could use the two links below to apply to my code without any serious issues:
> 
> - [https://www.kaggle.com/code/defdet/llama-2-13b-on-tpu-training/](https://www.kaggle.com/code/defdet/llama-2-13b-on-tpu-training/)
> 
> - [https://www.kaggle.com/code/kishanvavdara/lmsys-llama-3-tpu-train/](https://www.kaggle.com/code/kishanvavdara/lmsys-llama-3-tpu-train/)
> 
> Hope it helps 🤗.
> 
> 
> 


---

> ## Sparsh Tewatia
> 
> Nothing happens without difficulty bro 😭
> 
> 
> 


---



* --- discussion numver 118, the number of votes :1 ---

# Has anyone tried using an SVR (Support Vector Regression) to replace the original classification header?

**lllleeeo** *Sat Jul 20 2024 00:48:44 GMT+0900 (日本標準時)* (1 votes)

Has anyone tried using an SVR (Support Vector Regression) to replace the original classification head? I've noticed that the classification heads currently used in the public notebooks are simple linear fully connected layers, or two layers of linear heads with an activation function and dropout in the middle as someone mentioned in the comments section, and I'm wondering if using an SVR to generate predictions would perform better with the amount of data in the competition. 

I'm about to make an attempt at this but still have some concerns because then the parameters of the model are trained independently of the classification header that is ultimately used, and may blend even worse, so I'm wondering if anyone has experimented with this? We can discuss this together!😀





* --- discussion numver 119, the number of votes :1 ---

# Allowing the notebook keep on running at the back on Vast.ai

**JamshaidSohail** *Wed Jul 17 2024 00:34:15 GMT+0900 (日本標準時)* (1 votes)

Hi. I have successfully setup my instance on vast.ai for training Gemma 2. My notebook is running. I just want to make sure that it keeps on running even if close the browser. How would that be possible [@kishanvavdara](https://www.kaggle.com/kishanvavdara) [@valentinwerner](https://www.kaggle.com/valentinwerner).



---

 # Comments from other users

> ## Valentin Werner
> 
> How did I get to the point where I am directly tagged in open discussion questions? 😉
> 
> I have never used vast.ai, but what I did back when I had a university server with 4xV100 at my disposal:
> 
> - you should probably put your notebooks into a python script (train.py for example)
> 
> - you should start the scrip and move it to the background. I always used the linux command "screen" for this. Make sure to detach your screen before you close the browser and make sure the server keeps running (again, I never used vast.ai)..
> 
> ChatGPT should be able to give you more details, there are also plenty of documentations online
> 
> 
> 
> > ## JamshaidSohailTopic Author
> > 
> > Thank you so much. It works :D [@valentinwerner](https://www.kaggle.com/valentinwerner) 
> > 
> > 
> > 


---



* --- discussion numver 120, the number of votes :1 ---

# P100 and T4*2 GPUs inference results are different

**Femca7** *Tue Jul 16 2024 09:47:35 GMT+0900 (日本標準時)* (1 votes)

Recently, I found that the inference results differ when using a single GPU compared to using two GPUs. Another issue is that the inference results on my local machine and on Kaggle also have slight differences.

Does anyone know the reason for this?

Using one GPU:  

id     winner_model_a  winner_model_b  winner_tie 

1233961     0.245430    0.517676    0.236894

Using two GPUs:  

id     winner_model_a  winner_model_b  winner_tie 

1233961     0.238452    0.535787    0.225761



---

 # Comments from other users

> ## Valentin Werner
> 
> I also noticed that the scores are different across transformer versions.
> 
> 
> 


---



* --- discussion numver 121, the number of votes :1 ---

# Accessing Llama 3 MODEL_NAME in inference notebook

**JamshaidSohail** *Mon Jul 15 2024 00:07:29 GMT+0900 (日本標準時)* (1 votes)

Hi. I have successfully run the amazing [TPU Llama 3 training notebook](https://www.kaggle.com/code/kishanvavdara/lmsys-llama-3-tpu-train) by [@kishanvavdara](https://www.kaggle.com/kishanvavdara) and now I am trying to run the inference notebook. I have already been given access to the Llama 3 usage both on hugging face and meta official page and I have the corresponding hugging face token as well and weights file as well. When I try to run the [inference notebook](https://www.kaggle.com/code/kishanvavdara/inference-llama-3-8b), i get the below error 

OSError: Incorrect path_or_model_id: '/kaggle/input/llama-3/transformers/8b-chat-hf/1'. Please provide either the path to a local folder or the repo_id of a model on the Hub.

Internet access is off in the inference notebook. So I cannot use MODEL_NAME="meta-llama/Meta-Llama-3-8B-Instruct" like I did in training notebook which downloads the model from scratch from hugging face hub. Any sort of help would be highly appreciated. [@valentinwerner](https://www.kaggle.com/valentinwerner) 



---

 # Comments from other users

> ## Valentin Werner
> 
> First, you also need to request Llama Access on Kaggle, you can do so by following the model link. Then, make sure you have the llama model added as model in the notebook, then the path will be exactly right.
> 
> 
> 
> > ## JamshaidSohailTopic Author
> > 
> > So I already got access to the Llama model via using the official Meta page and now I submitted the form via the Kaggle. I hope it gets approved quickly and I can move fast :D. Thank you so much once again.
> > 
> > 
> > 
> > > ## JamshaidSohailTopic Author
> > > 
> > > Thank you [@valentinwerner](https://www.kaggle.com/valentinwerner). I have been granted access and I am able to do the inference :D
> > > 
> > > 
> > > 
> > > ## Valentin Werner
> > > 
> > > Amazing, that you got it within the hour on a saturday! Some people reported waiting times of 24+ hours. Best of luck with your training - toi toi toi 😉
> > > 
> > > 
> > > 


---



* --- discussion numver 122, the number of votes :1 ---

# Does the order of the submission file matter?

**Lorry Zou** *Sat Jul 13 2024 04:05:31 GMT+0900 (日本標準時)* (1 votes)

Title. Is it OK if I change the order of the original submission file?

For example, the original id's are: 01, 02, 03.

Is it OK if I submit in this order: 02|prediction, 01|prediction, 03|prediction ?



---

 # Comments from other users

> ## Valentin Werner
> 
> No it won't matter. I submitted submission.csv files with reversed IDs before.
> 
> 
> 


---



* --- discussion numver 123, the number of votes :1 ---

# There is more than 1 prompt in ~10% of the ['prompt'] rows

**Matthew Hendricks** *Fri Jul 12 2024 02:04:16 GMT+0900 (日本標準時)* (1 votes)



```
import matplotlib.pyplot as plt
from datasets import load_dataset
import ast

# Load the dataset
dataset = load_dataset("lmsys/lmsys-arena-human-preference-55k", split='train')

# Function to safely evaluate the string as a list
def safe_eval(s):
    try:
        return ast.literal_eval(s)
    except:
        return []

# Count the number of items in each prompt
item_counts = [len(safe_eval(prompt)) for prompt in dataset['prompt']]

# Count the frequency of each number of items
count_freq = {}
for count in item_counts:
    count_freq[count] = count_freq.get(count, 0) + 1

# Prepare data for plotting
counts = list(count_freq.keys())
frequencies = list(count_freq.values())

# Create the bar plot
plt.figure(figsize=(10, 6))
plt.bar(counts, frequencies)
plt.xlabel('Number of Items in Prompt')
plt.ylabel('Frequency')
plt.title('Distribution of Number of Items in Prompts')
plt.xticks(range(min(counts), max(counts)+1))

# Add value labels on top of each bar
for i, v in enumerate(frequencies):
    plt.text(counts[i], v, str(v), ha='center', va='bottom')

plt.tight_layout()
plt.show()

# Print some statistics
total_prompts = len(item_counts)
avg_items = sum(item_counts) / total_prompts
print(f"Total number of prompts: {total_prompts}")
print(f"Average number of items per prompt: {avg_items:.2f}")
print(f"Most common number of items: {max(count_freq, key=count_freq.get)}")
print(f"Maximum number of items in a prompt: {max(counts)}")

```





* --- discussion numver 124, the number of votes :1 ---

# Explanation on the prediction that the model must perform

**GregReds** *Thu Jul 11 2024 05:15:59 GMT+0900 (日本標準時)* (1 votes)

Hello everyone!

I am a master's degree student and I am using this competition for an exam; for educational purposes, I must primarily rely on the use of word embedding. My question and my doubt is: to make predictions and to determine whether to award the win to model a or model b, should the model only check the structure of the responses, or also their correctness?

Let me give an example to be more explicit:

If the prompt were: What is the capital of France?

response_a: The capital of France is Paris.

response_b: The capital of France is Rome.

Typically, a model like word2vec, if not too well-trained, might base its evaluation on the structure rather than the correctness, focusing on the fact that the sentences are structured similarly and this predicting a tie. However, model A should win because the actual capital is indeed Paris, not Rome.

Therefore, it might be useful to utilize word embedding models like Bert that theoretically also check the correctness of the response.

I hope I have made myself clear! Thanks everyone.

[Screenshot 2024-07-10 alle 22.14.58.png](https://storage.googleapis.com/kaggle-forum-message-attachments/2916192/20917/Screenshot 2024-07-10 alle 22.14.58.png)



* --- discussion numver 125, the number of votes :1 ---

# this requirement <= 9 hours run-time is for public dataset or private ?

**Dlond Mike** *Mon Jul 08 2024 22:13:47 GMT+0900 (日本標準時)* (1 votes)

this requirement

<= 9 hours run-time

is for public dataset or private ?



---

 # Comments from other users

> ## Valentin Werner
> 
> On submission you are running the whole test set, private and public. Therefore, if your submission finishes in 9 hours, and you see a score on LB, you have nothin to worry about.
> 
> 
> 


---

> ## gmin5y
> 
> See this previous post for details: [https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/517142](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/517142)
> 
> 
> 


---

> ## Lorry Zou
> 
> It's for the whole(private) test set.
> 
> 
> 


---



* --- discussion numver 126, the number of votes :1 ---

# Too long waiting time for TPU

**Saiyan Warrior** *Thu Jul 04 2024 19:11:11 GMT+0900 (日本標準時)* (1 votes)

Hi Kaggler, 

Are you also facing too long waiting time/queue( sometimes more than 1 hour) for TPU usage? 
To whom should we raise this issue? 
What other options are you trying for TPU besides colab?


---

 # Comments from other users

> ## Valentin Werner
> 
> Not sure about many other options. With the rise of LLMs, these resources have been used a lot more. You can raise feature requests and complain about stuff like this in Product Feedback: [https://www.kaggle.com/discussions/product-feedback?sort=published](https://www.kaggle.com/discussions/product-feedback?sort=published)
> 
> However, Kaggle provides these resources for free so you dont have to provide them yourself and to even out the playing field for these competitions a bit. I think its important to either be grateful for what Kaggle provides (of course you can still raise it in product feedback), or adapt & overcome and find a solution that works for you. There are many alternatives for the goold old GPU - which still works well 😉
> 
> 
> 
> > ## Saiyan WarriorTopic Author
> > 
> > [@valentinwerner](https://www.kaggle.com/valentinwerner) 
> > 
> > I am not only grateful for computing but also for the kaggle platform itself I have learned a lot from this platform.
> > I just wanted to check whether this happening to me only or in general and what option others are using.
> > 
> > 
> > > ## Sparsh Tewatia
> > > 
> > > Try applying for TRC google program , they give I think 1 month of free access to TPUs
> > > 
> > > 
> > > 


---

> ## madarshbb
> 
> 1) Yes, it is an issue for quite some time now.
> 
> 2) You can raise this in kaggle's product feedback
> 
> 3) I tried GCS and azure sagemaker. But they have quite a cumbersome setup process. Would much rather wait for kaggle's TPU for a few hours, but less TPU waiting time would be a blessing.
> 
> 
> 
> > ## Saiyan WarriorTopic Author
> > 
> > Thanks [@madarshbb](https://www.kaggle.com/madarshbb) 
> > 
> > 
> > 


---



* --- discussion numver 127, the number of votes :1 ---

# Model licenses

**gromml** *Fri Jul 05 2024 06:27:37 GMT+0900 (日本標準時)* (1 votes)

Hi all,

I am new to HF. I can see that different models come with different licenses: [https://huggingface.co/docs/hub/repositories-licenses](https://huggingface.co/docs/hub/repositories-licenses). How can I find out which licenses conform to the competition rules?

Thanks.



---

 # Comments from other users

> ## Valentin Werner
> 
> You need to have available commercial use.
> 
> The common licenses that work are including (but others probably too): MIT, Apache 2.0, CC-BY4.0, Llama License, Gemma License.
> 
> Always make sure that you further read the licenses if you plan to distribute information (e.g., for Llama and Gemma).
> 
> 
> 
> > ## grommlTopic Author
> > 
> > For example, if I want to use this model:
> > 
> > [https://huggingface.co/vennify/t5-base-grammar-correction](https://huggingface.co/vennify/t5-base-grammar-correction)
> > 
> > I can see that it has Creative Commons Attribution Non Commercial Share Alike 4.0. Does using this model conform to this competition?
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > This sounds weird but you can try it out locally or in kaggle. From my understanding (not a lawyer) you should not submit this to the competition (because then it becomes an attempt to win money). However, as long as you dont go for a gold medal, it probably hardly matters.
> > > 
> > > 
> > > 


---



* --- discussion numver 128, the number of votes :1 ---

# Can I use model which is not in kaggle ? 

**AlphaTT30** *Sat Jun 29 2024 08:42:50 GMT+0900 (日本標準時)* (1 votes)

In this competition, internet access is not allowed. So I can't use hugging face pre-trained transformer models like this one. The submission gets an error, I think for this one. This needs to be downloaded 

```
# Load model directly
from transformers import AutoTokenizer, AutoModelForMaskedLM

tokenizer = AutoTokenizer.from_pretrained("google-bert/bert-base-uncased")
model = AutoModelForMaskedLM.from_pretrained("google-bert/bert-base-uncased")

```

So what to do? 

Are all the hugging face models in kaggle? 

should I use a model that exists on Kaggle? 

or is there another way to use this one? 



---

 # Comments from other users

> ## tanaka
> 
> You can download these kind of Bert related things and llms before internet ristriction.
> 
> Major topic of these competition is
> 
> Training llm or nlp related model using some techniques and gpus (it is updated to you)
> 
> And then use these models as inference models without internet.
> 
> 
> 


---

> ## Yichuan Gao
> 
> If the model license permits, you can just download the model from huggingface and upload it to kaggle as a model, then add it to your notebook
> 
> 
> 
> > ## AlphaTT30Topic Author
> > 
> > Can I train a model outside kaggle and then upload here and use that model for this competition?  
> > 
> > 
> > 
> > > ## Ravi Ramakrishnan
> > > 
> > > Yes of course, this is a preferred way to handle these competitions [@alphatt30](https://www.kaggle.com/alphatt30) 
> > > 
> > > 
> > > 
> > ## Ivel afred
> > 
> > Does this mean that your model needs to be made public on Kaggle? Or is it okay to just make it public on Hugging Face.
> > 
> > 
> > 
> > > ## Yichuan Gao
> > > 
> > > You don't need to upload your model to huggingface, just upload it here on kaggle is ok. Also you can make it private (by default) and use it in your notebooks
> > > 
> > > 
> > > 
> > > ## Ivel afred
> > > 
> > > Code Requirements in LMSYS states: 'Freely&publicly available external data is allowed, including pre trained models.' Does this not require your models to be public? I'm a little confused
> > > 
> > > 
> > > 


---



* --- discussion numver 129, the number of votes :1 ---

# Traing steps cannot match the sample size!

**godmysalary** *Fri Jul 05 2024 12:49:34 GMT+0900 (日本標準時)* (1 votes)

Hello everyone! We were using the vscode to run the amazing fine-tune work by [https://www.kaggle.com/code/hotchpotch/train-llm-detect-ai-comp-mistral-7b/notebook](url)

The only difference is that we change the model to Llama3. 

And when I run the code on Kaagle GPU, everything is fine. The sample size is 500, gradient_accumulate_steps is 16, batch_size=1, so we will undergo 31 steps, which is shown by the first picture below. 

However when I just COPY the same code to my vscode which is connected to a remote server, the total steps became 10! The sample size, gradient_accumulate_steps, batch_size stay unchanged but the total steps became 10, which is shown in the second picture and means only about 160 (16*10) samples are processed? Only one GPU is used on the vscode. 

Could anybody give me a hint about what is going on? The packages are updated. 



---

 # Comments from other users

> ## godmysalaryTopic Author
> 
> Hello everybody! We checked this probelm again and finally found the "killer"! Our remote server has 3 GPUs and so as you may suspect, the program is parallelled. The most annoying part is that when we loaded the model, we set device_map={'': 0} but somehow it still ran parallelly. So we explicitly set CUDA_VISIBLE_DEVICES = 0 at the beginning of our code and the problem faded! Hope this help you for your fine-tuning.
> 
> 
> 


---

> ## Valentin Werner
> 
> Did you check the length of your data? Did you accidentally swap train and validation dataset?
> 
> 
> 
> > ## godmysalaryTopic Author
> > 
> > yes! the length of train_dataset is 500 and the length of evaluation_dataset is 100.
> > 
> > 
> > 


---



* --- discussion numver 130, the number of votes :1 ---

# Getting error in sumbission.

**AlphaTT30** *Sun Jun 30 2024 21:56:50 GMT+0900 (日本標準時)* (1 votes)

Notebook successfully rans but then getting error like this 

[no idea what's going no or why happening this ] 

What to do now ? 

You're using a BertTokenizerFast tokenizer. Please note that with a fast tokenizer, using the __call__ method is faster than using a method to encode the text followed by a call to the pad method to get a padded encoding.

89.2s    2   /opt/conda/lib/python3.10/site-packages/traitlets/traitlets.py:2930: FutureWarning: --Exporter.preprocessors=["remove_papermill_header.RemovePapermillHeader"] for containers is deprecated in traitlets 5.0. You can pass --Exporter.preprocessors item … multiple times to add items to a list.

89.2s    3     warn(

89.2s    4   [NbConvertApp] WARNING | Config option kernel_spec_manager_class not recognized by NbConvertApp.

89.3s    5   [NbConvertApp] Converting notebook notebook.ipynb to notebook

89.7s    6   [NbConvertApp] Writing 32587 bytes to notebook.ipynb

91.3s    7   /opt/conda/lib/python3.10/site-packages/traitlets/traitlets.py:2930: FutureWarning: --Exporter.preprocessors=["nbconvert.preprocessors.ExtractOutputPreprocessor"] for containers is deprecated in traitlets 5.0. You can pass --Exporter.preprocessors item … multiple times to add items to a list.

91.3s    8     warn(

91.3s    9   [NbConvertApp] WARNING | Config option kernel_spec_manager_class not recognized by NbConvertApp.

91.3s    10  [NbConvertApp] Converting notebook notebook.ipynb to html

92.2s    11  [NbConvertApp] Writing 319012 bytes to results.html



---

 # Comments from other users

> ## Anya
> 
> Same situation. Waiting for resolution🤷‍♂️
> 
> 
> 
> > ## Anya
> > 
> > [https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/511861](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/511861)
> > 
> > There is a similar tag, you can check if it helps.
> > 
> > 
> > 
> > > ## AlphaTT30Topic Author
> > > 
> > > I solved my problem. Do you need a solution? 
> > > 
> > > 
> > > 


---



* --- discussion numver 131, the number of votes :1 ---

# Why is the scoring process so time-consuming

**David.Ricardo.H.X** *Thu May 30 2024 12:13:45 GMT+0900 (日本標準時)* (1 votes)


I submit successfully the code, the scoring is still running.
The submitted notebook throws error, the scoring is still running. 

Does anybody have the same issue? 



---

 # Comments from other users

> ## Valentin Werner
> 
> Note that time difference between Submission and save come from the data difference. During saving (the success / error you mentioned) the test data only has 3 rows, during submission its 25,000 rows. A subset of these rows are used for Public Leaderboard (what we see on Leaderboard right now), while most IS used for private Leaderboard / the score we see once the competition finished, and which is used for actual evaluation in the competition placement.
> 
> So you are running A LOT more data during submission, increasing runtime for row based operations
> 
> 
> 
> > ## Nguyễn Anh Tú
> > 
> > Does the data in file train.csv in submission environment different from the data in that file when we training model with our private notebook sir? 
> > 
> > 
> > 


---

> ## [Deleted User]
> 
> The scoring process can be time-consuming due to several factors:
> 
> Complexity of Notebook: Long-running computations or large datasets extend execution time.
> Resource Constraints: Limited computational resources and high submission volumes cause delays.
> Error Handling: Systems may attempt to run all cells despite errors to gather complete data.
> Automated Evaluation: Comprehensive testing and validation can take a significant amount of time.
> System Overhead: Infrastructure tasks such as container setup and data transfer add to the delay
> 
> 


---



* --- discussion numver 132, the number of votes :1 ---

# offline use of fine-tuned Llama3

**nahyat** *Thu Jun 20 2024 16:00:07 GMT+0900 (日本標準時)* (1 votes)

Inspired by Kishan Vavdara's wonderful notebook, I fine-tuned the Llama3-8b model in colab. I got the basemodel from huggingface's Llama3-8b model instead of the kaggle dataset.（MODEL_NAME = 'meta-llama/Meta-Llama-3-8B'）

When I tried to use the fine-tuned model in kaggle, I was faced with a situation where I could not load the weights of the model I created because huggingface could not be authenticated in the offline environment.

After loading the basemodel from the kaggle dataset, I also failed to load the weights of my model.

Is it because the models in huggingface and kaggle dataset are not compatible, which is why the loading fails?

Note: Llama3 license applications for the kaggle dataset are also allowed.

Thank you for watching



---

 # Comments from other users

> ## Kishan Vavdara
> 
> I'm glad you found my notebook helpful. Can you share the error you're facing ? and did you use LoRA for fine-tuning?
> 
> 
> 
> > ## nahyatTopic Author
> > 
> > Thank you for watching!
> > 
> > I wasn't getting any errors, but I was worried that the processing was too fast (compared to your model) when loading the weights of the fine-tuned model into the basemodel. ↓
> > 
> > model_0.load_state_dict(torch.load(WEIGHTS_PATH), strict=False)
> > 
> > I noticed that the results of inference were surprisingly low, so I guessed that there was some kind of problem when loading the model parameters.
> > 
> > However, when I reviewed the code in a local environment, I confirmed that there was a discrepancy in the variable names in the training flow, which caused the correct labels required for backward to fail to be obtained. (I don't know why trainer.train() worked without an error.)
> > 
> > I'm sorry for taking the time to watch it…
> > 
> > 
> > 
> > > ## Kishan Vavdara
> > > 
> > > No worries, It's great to hear that you found the discrepancy and resolved the issue. Happy finetuning) 
> > > 
> > > 
> > > 


---

> ## Lorry Zou
> 
> How long did it take to fine-tune on Colab? I'm also trying to fine-tune on Colab but it'll take over 20 hours using A100, which is much longer than the max session length of Colab (12 hours). How did you make it shorter than 12 hours? Thank you so much.
> 
> 
> 


---



* --- discussion numver 133, the number of votes :1 ---

# Why do I get "Notebook Threw Exception", and with the same notebook, sometimes, I get a successful submission?

**Kilaru Vasudeva** *Sat Jun 15 2024 21:32:39 GMT+0900 (日本標準時)* (1 votes)

I find it wierd. Is it any wrong code specification on myside or it is something on the kaggle backend?



---

 # Comments from other users

> ## OminousDude
> 
> Can I get some more info about this problem? It could be if you don't set a random seed something like a division by zero could occur.
> 
> 
> 


---



* --- discussion numver 134, the number of votes :1 ---

# More information on test dataset

**Matous Famera** *Thu Jun 13 2024 02:12:49 GMT+0900 (日本標準時)* (1 votes)

Hello, I have a few questions regarding the nature of test dataset.

I already know that 26% of the entire test dataset is used for public leaderboard and 74% is used for private leaderboard.

What is the difference between the train dataset and test dataset? Are the same LLMs used? Was the same dataset used for train dataset and test dataset?
How long is the test dataset? Or atleast how long compared to the train dataset is the test dataset?

Thanks if any of these questions can be answered



---

 # Comments from other users

> ## James Day
> 
> 
> What is the difference between the train dataset and test dataset? Are the same LLMs used? Was the same dataset used for train dataset and test dataset?
> 
> I've noticed there aren't any recently released models (e.g. Llama 3) in the training dataset, so I have a suspicion they split their data based on the date on which each comparison occurred and I would expect to receive messages from different LLMs during testing.
> 
> How long is the test dataset? Or atleast how long compared to the train dataset is the test dataset?
> 
> The data tab says "you can expect roughly 25,000 rows in the test set"
> 
> 
> 
> > ## Matous FameraTopic Author
> > 
> > 
> > There are 55K rows in the training data, and you can expect roughly 25,000 rows in the test set.
> > 
> > Does it mean that the entire test dataset has 25k rows or just the public leaderboard part?
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > The entire data has 25k rows, ~26% of them is public leaderboard (so about 6.5k rows).
> > > 
> > > As you probably guess, this makes trusting the public leaderboard score similar to trusting a single validation fold in a 4-fold cv setup. Thats why it is often recommended to build a good CV strategy and try to create a correlation between the CV score (which should be reliable) and the public LB score.
> > > 
> > > Also note, that the final score is ONLY the private LB, so the other 74% of the data. Meaning the fold, you may overfit on (the public LB) is NOT part of your winning score. This can lead to what we call "Leaderboard shakeup". These concepts apply to basically all kaggle competitions.
> > > 
> > > 
> > > 
> > > ## Matous FameraTopic Author
> > > 
> > > Thanks for clarification. I was asking that questions, because the length of the test dataset is related to variance and reliability of the score.
> > > 
> > > I'm aware of the concept of overfitting for public leaderboard.
> > > 
> > > 
> > > 


---



* --- discussion numver 135, the number of votes :1 ---

# training loss doesnt converge

**ivan_c2004** *Sat Jun 08 2024 22:15:28 GMT+0900 (日本標準時)* (1 votes)

Hello guys, i am using deberta xsmall with peft for training. the batch size is 8 and the learning rate is 1e-4, data for training is the range 40k to 56k , everytime i train the model the loss keeps at about 1.01, doesnt decrease after 6-7 epoches. my gpu is rtx 3060 only and training for ten or more epoches would take me more than a day and that i read from online websites lora finertuning llm should take only a few epoches so i didnt try for more epoches. Does anyone know how to solve this issue, or just try training for more epoches until the loss reaches a certain number like 0.2 0.3? thank you so much

My codes for training can be found below. Thank you 

```
from peft import get_peft_config, PeftModel, PeftConfig, get_peft_model, LoraConfig, TaskType
import torch
import sklearn
import numpy as np
import pandas as pd
import time
from tqdm import tqdm
from torch.nn import CrossEntropyLoss
from torch.utils.data import DataLoader, Dataset
from sklearn.model_selection import train_test_split
import matplotlib.pyplot as plt

from transformers import AutoTokenizer, LlamaModel, LlamaForSequenceClassification, BitsAndBytesConfig,get_linear_schedule_with_warmup,AutoModelForSequenceClassification,DebertaTokenizerFast
from torch.cuda.amp import autocast

torch.backends.cuda.enable_mem_efficient_sdp(False)
torch.backends.cuda.enable_flash_sdp(False)

if (not torch.cuda.is_available()): print("Sorry - GPU required!")
print(torch.__version__)
if torch.cuda.is_available(): print('gpu available')
from huggingface_hub import login
login(token="")

class CustomDataset(Dataset):
    def __init__(self, df, tokenizer):
        self.df = df
        self.tokenizer = tokenizer

    def __len__(self):
        return len(self.df)

    def __getitem__(self, idx):
        text = self.df.loc[idx, 'text']
        labels_a = self.df.loc[idx, 'winner_model_a']
        labels_b = self.df.loc[idx, 'winner_model_b']
        labels_tie = self.df.loc[idx, 'winner_tie']

        max_length = 1024

        inputs = self.tokenizer(
            text,
            max_length=max_length,
            truncation=True,
            padding="max_length",
            return_tensors="pt"
        )
        input_ids = inputs['input_ids'].squeeze()
        attention_mask = inputs['attention_mask'].squeeze()

        labels = torch.tensor([labels_a, labels_b, labels_tie]) 

        return {
            'input_ids': input_ids,
            'attention_mask': attention_mask,
            'labels': labels  
        }

bnb_config = BitsAndBytesConfig(
    load_in_4bit=True,
    bnb_4bit_use_double_quant=True,
    bnb_4bit_quant_type="nf4",
    bnb_4bit_compute_dtype=torch.float16
)
print(torch.cuda.get_device_name(0))

model_id = "microsoft/deberta-v3-xsmall"
tokenizer_id = "microsoft/deberta-v3-xsmall"

tokenizer = AutoTokenizer.from_pretrained(tokenizer_id)
model = AutoModelForSequenceClassification.from_pretrained(
    model_id,
    num_labels=3,
    torch_dtype=torch.float16,
    quantization_config=bnb_config,
    device_map='cuda:0')
model.config.pad_token_id = tokenizer.pad_token_id
tokenizer.pad_token = tokenizer.eos_token

peft_config = LoraConfig(
    r=16,
    lora_alpha=32,
    lora_dropout=0.10,
    bias='none',
    task_type=TaskType.SEQ_CLS,
    )
device = torch.device('cuda:0')
baseline_model = get_peft_model(model, peft_config).to(device)
baseline_model.print_trainable_parameters()
baseline_model.eval()

lr = 1e-4
num_epochs = 16
batch_size = 8
kaggle = False

train_df = pd.read_csv('./lmsys-chatbot-arena/train.csv')
print('number of training data: ',len(train_df))
train_df = train_df.iloc[:]
def process(input_str):
    stripped_str = input_str.strip('[]')
    sentences = [s.strip('"') for s in stripped_str.split('","')]
    return ' '.join(sentences)

train_df.loc[:, 'prompt'] = train_df['prompt'].apply(process)
train_df.loc[:, 'response_a'] = train_df['response_a'].apply(process)
train_df.loc[:, 'response_b'] = train_df['response_b'].apply(process)
train_df['text'] = 'User prompt: ' + train_df['prompt'] + '\n\nModel A :\n' + train_df['response_a'] + '\n\n--------\n\nModel B:\n' + train_df['response_b']
train_df = train_df.reset_index(drop=True)

if kaggle:
    print(f'number of training data {len(train_df)}')
else:
    train_df, val_df = train_test_split(train_df, test_size=0.2, random_state=42)
    train_df = train_df.reset_index(drop=True)
    val_df = val_df.reset_index(drop=True)
    print(f'number of training data after spliting: {len(train_df)} number of testing data: {len(val_df)}')
    val_dataset = CustomDataset(val_df, tokenizer)
    val_dataloader = DataLoader(val_dataset, batch_size=batch_size, shuffle=False)

train_dataset = CustomDataset(train_df, tokenizer)
train_dataloader = DataLoader(train_dataset, batch_size=batch_size, shuffle=False)

import gc

gc.collect()

torch.cuda.empty_cache()

criterion = CrossEntropyLoss()

optimizer = torch.optim.AdamW(baseline_model.parameters(), lr=lr)

lr_scheduler = torch.optim.lr_scheduler.StepLR(optimizer, step_size=5, gamma=0.1)

training_losses = []  
validation_losses = []  

for epoch in range(num_epochs):
    baseline_model.train()
    epoch_training_loss = 0  

    for step, batch in enumerate(tqdm(train_dataloader)):
        batch = {k: v.to(device) for k, v in batch.items()} 

        inputs = {
            'input_ids': batch['input_ids'],
            'attention_mask': batch['attention_mask'],
        }
        outputs = baseline_model(**inputs)
        labels = batch['labels'].float()
        loss = criterion(outputs.logits, labels)
        loss.backward()
        optimizer.zero_grad()

        epoch_training_loss += loss.item() 

    epoch_training_loss /= len(train_dataloader)  
    training_losses.append(epoch_training_loss) 
    baseline_model.eval()
    if not kaggle:
        total_validation_loss = 0
        total_samples = 0
        correct_predictions = 0

        with torch.no_grad():
            for step, batch in enumerate(tqdm(val_dataloader)):
                batch = {k: v.to(device) for k, v in batch.items()}  

                inputs = {
                    'input_ids': batch['input_ids'],
                    'attention_mask': batch['attention_mask'],
                }
                outputs = baseline_model(**inputs)
                predictions = outputs.logits.argmax(dim=-1)
                labels = batch['labels'].float().argmax(dim=1)

                loss = criterion(outputs.logits, labels)
                total_validation_loss += loss.item()
                total_samples += len(labels)
                correct_predictions += (predictions == labels).sum().item()

        epoch_validation_loss = total_validation_loss / len(val_dataloader)
        validation_losses.append(epoch_validation_loss)  

        accuracy = correct_predictions / total_samples
        print(f"Validation Loss: {epoch_validation_loss:.4f}, Accuracy: {accuracy:.4f}")
    print(f"Epoch {epoch+1}: Training Loss: {epoch_training_loss:.4f}")

plt.plot(training_losses, label='Training Loss')
plt.plot(validation_losses, label='Validation Loss')
plt.xlabel('Epoch')
plt.ylabel('Loss')
plt.legend()
plt.show()

torch.save(baseline_model.state_dict(), 'model.pt')

```



---

 # Comments from other users

> ## yechenzhi1
> 
> larger batch size helped for me( I just increased gradient_accumulation_steps to 100)
> 
> 
> 
> > ## ivan_c2004Topic Author
> > 
> > yah gradient accumulation can help! thx. 
> > 
> > how long does the training take? what is the suggested epoch and batch size?
> > 
> > 
> > 
> > > ## yechenzhi1
> > > 
> > > Training time is up to your GPUs and model size. And I simply tried 1 epoch and 400 batch size( I didn't do much experiments, this is just my personal choice)
> > > 
> > > 
> > > 
> > > ## ivan_c2004Topic Author
> > > 
> > > I see. Thank you so much!
> > > 
> > > 
> > > 


---

> ## Valentin Werner
> 
> model might be too small. took me Base model, Higher effective batch size and lower lr with all data for some epochs to her ANY convergence
> 
> Using PEFT with XSmall model might not be preferrable either, training on kaggle GPU can easily handle full finetune of the small models.
> 
> Also you leaked your huggingface token, I recommend to remove that.
> 
> 
> 
> > ## ivan_c2004Topic Author
> > 
> > i see. 
> > 
> > thank you so much for reminding me the leak 
> > 
> > 
> > 


---



* --- discussion numver 136, the number of votes :1 ---

# How far can a boosting get you?

**Ivan Vybornov** *Sat Jun 08 2024 05:37:05 GMT+0900 (日本標準時)* (1 votes)

I am curious what is a score upper bound on using solely a boosting?

The best performing public notebook that only utilizes a GBDTs so far is [https://www.kaggle.com/code/andreasbis/lmsys-chatbot-arena-tf-idf#Model-Training-%F0%9F%A7%A0](https://www.kaggle.com/code/andreasbis/lmsys-chatbot-arena-tf-idf#Model-Training-%F0%9F%A7%A0)

But the difference with llama3 inference is more than significant (1.011 vs 0.989) which makes me wonder if one should even bother trying to get below 0.98 with it.



---

 # Comments from other users

> ## Valentin Werner
> 
> I was wondering the same. Different than the notebook you mentioned above I went a pure Text characteristic based Feature approach (Length, Paragraph Count, …) and got to around 1.036
> 
> This is so far away from Raja's current score that I think it is not worth to be the main model for the prediction
> 
> If you are not going for the win and instead want to learn about boosting and feature engineering, I would suggest you try to get below 1.0 yourself
> 
> 
> 


---



* --- discussion numver 137, the number of votes :1 ---

# How can i use llama3?

**zyw** *Tue May 28 2024 03:11:29 GMT+0900 (日本標準時)* (1 votes)

I submitted the llama3 form without applying from the meta official website, and the model author refused me to use llama3. 

After I clicked "here" and filled out the form on the meta official website, I can now use llama2 normally, but cannot use llama3. I want to resubmit the form but I don't find the submit button. Can anyone help me solve this problem?



---

 # Comments from other users

> ## Valentin Werner
> 
> Not directly answering your problem, but giving you a workaround:
> 
> You can also go to huggingface, create an Account, apply for llama3 on the model Page, wait 12 hours, put an access token into your Notebook (dont share it!!) and then use it that way by specifying "token=…" in all the from_pretrained calls (model, tokenizer).
> 
> this is rather recommended for local Training. You will not be able to turn off Internet access for that notebook.
> 
> 
> 
> > ## zywTopic Author
> > 
> > This is indeed a great idea, thank you for sharing!
> > 
> > 
> > 


---



* --- discussion numver 138, the number of votes :1 ---

# Opening move for this competition

**MountainGoriillas** *Fri May 24 2024 22:03:31 GMT+0900 (日本標準時)* (1 votes)

This competition doesn't provide a starter notebook created by the host. How did you all prepare for it?



---

 # Comments from other users

> ## G John Rao
> 
> There is one pinned notebook in the code section. Here's the link to the starter notebook [https://www.kaggle.com/code/awsaf49/lmsys-kerasnlp-starter](https://www.kaggle.com/code/awsaf49/lmsys-kerasnlp-starter)
> 
> 
> 


---



* --- discussion numver 139, the number of votes :1 ---

# Internet access condition

**Kamil Machalica** *Fri May 17 2024 21:07:02 GMT+0900 (日本標準時)* (1 votes)

Hi Kagglers!

If there is internet access restrictions can we even use pre-trained models to download them?

Thanks

Kamil



---

 # Comments from other users

> ## Valentin Werner
> 
> There are several things you can do, and what is often done:
> 
> 1) You can download the models, save them as kaggle dataset, load them from kaggle dataset instead (same goes for pip installs you might want to do)
> 
> 2) You can train models in one notebook with internet access, save the model checkpoint at the end and then create a separate notebook without internet access. Then you can simply add the training notebook as input for the inference notebook!
> 
> Hope this helps, welcome to kaggle and good luck!
> 
> 
> 
> > ## Kamil MachalicaTopic Author
> > 
> > Thank you, it explains a lot!
> > 
> > 
> > 


---

> ## Muhammad Tariq Pervez
> 
> [@machalx](https://www.kaggle.com/machalx), In Kaggle competitions, "disabling internet" means that the code you submit to Kaggle for scoring is executed in an environment that does not have access to the internet. Ensure your submission does not include any code that requires internet access, such as downloading data from external URLs or accessing online APIs.
> 
> Otherwise no issue. 
> 
> 
> 


---



* --- discussion numver 140, the number of votes :1 ---

# Is TPU allowed to be used in this competition 

**kheder yazgi** *Fri May 17 2024 09:27:55 GMT+0900 (日本標準時)* (1 votes)

Considering the huge data; we have, is allowed to train models on TPU?



---

 # Comments from other users

> ## Muhammad Tariq Pervez
> 
> Generally yes. But please read rules carefully
> 
> 
> 


---

> ## Valentin Werner
> 
> yes, you have TPU quota available, so you could use it to train.
> 
> 
> 
> > ## kheder yazgiTopic Author
> > 
> > Thanks really 
> > 
> > 
> > 


---



* --- discussion numver 141, the number of votes :1 ---

# why are there only 3 test cases in the test.csv?

**Kaizhao Liang** *Mon May 13 2024 23:44:03 GMT+0900 (日本標準時)* (1 votes)

Is this expected?



---

 # Comments from other users

> ## Ravi Ramakrishnan
> 
> This is expected- your test data in the data page is a sample to be used for code check- the actual one is hidden [@lkz919](https://www.kaggle.com/lkz919) 
> 
> 
> 
> > ## Kaizhao LiangTopic Author
> > 
> > Ah thank you, so basically when they are running the notebook they would replace it with the hidden csv file. One additional question about no internet access, does it mean we can't access the trained models we upload ourselves when they run it? A bit confused by this constraint, and where should we download the pretrained weights if we use anything from huggingface.
> > 
> > 
> > 
> > > ## Ravi Ramakrishnan
> > > 
> > > Pre trained models need to be imported into a Kaggle model/ dataset and then used in the submission kernel [@lkz919](https://www.kaggle.com/lkz919) 
> > > 
> > > You can refer my baseline work to know more 
> > > 
> > > 
> > > 


---



* --- discussion numver 142, the number of votes :1 ---

# Data Understanding: Some response is NULL

**Squirrel** *Fri May 10 2024 13:10:21 GMT+0900 (日本標準時)* (1 votes)

I find some response is Null. Seems that they are deleted for some reason.



---

 # Comments from other users

> ## Austin Paxton
> 
> Based on the following discussion, it appears that it can be caused by platform error and possibly erratic user behavior.
> 
> [https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/502303](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/502303)
> 
> 
> 


---



* --- discussion numver 143, the number of votes :1 ---

# TF-IDF -> Boosted Trees [LB 1.038]

**Rich Olson** *Tue May 07 2024 10:44:19 GMT+0900 (日本標準時)* (1 votes)

Hey all -

Sharing my first (working) effort at this:

[https://www.kaggle.com/code/richolson/lmsys-tf-idf-boosted-trees](https://www.kaggle.com/code/richolson/lmsys-tf-idf-boosted-trees)

Simple idea is to use TF-IDF for vectorizing the texts - then see if a gradient boosted tree framework (LightGBM) can figure it out.

The TF-IDF vectorizer is fitted on prompt, response_a and response_b.

Vectorization is done on response_a and response_b separately and then combined in an hstack - and then LightGBM is trained on the whole mess.

(Using prompt for training didn't seem to obviously improve performance).

Vectorization + training takes about 30 minutes on CPU.  I don't have a time estimate on inference - but it's fast on just CPU.

I had minimal luck when vectorizing with ngram_range=(3, 5).  Performance improved a bunch when I changed that to ngram_range=(1, 5).  This approach working may be a lot about simple word frequency.

Another version of the notebook uses XGBoost - which trains much slower (about 2.5 hours).  That one is still scoring as I type this (I suspect it will have an LB score about the same).  I tried speeding up XGBoost using GPU - but for some reason it wouldn't converge.

Since I'm able to train-on-submission - one interesting option might be to try fitting the vectorizer on the test data (and then using that to vectorize the training data)…

Hope this is helpful to someone!

-Rich

Side note: I just noticed validation on LightGBM reported a log-loss score of 1.036.. - shockingly close to my LB of 1.038! I can't recall another time I've had that happen…



---

 # Comments from other users

> ## Rich OlsonTopic Author
> 
> The XGBoost version finished scoring - 1.039 on the LB.
> 
> Considering XGBoost took much, much longer to train - I'll stick with LightGBM for this notebook.
> 
> If you're curious to see the XGBoost code - just look a version 8 of this notebook.
> 
> 
> 


---



* --- discussion numver 144, the number of votes :0 ---

# 0.707 -> 0.663 in 3 hours

**justin1357** *Sun Aug 04 2024 08:04:40 GMT+0900 (日本標準時)* (0 votes)

don't want to repeat anything, do our best.



---

 # Comments from other users

> ## Enter your display name
> 
> He directly used the leaked data for a match, and then used his own model to predict the rest. It's unbelievable that something like this happened so close to the end of the competition; it almost ruined the whole competition.
> 
> 
> 
> > ## Valentin Werner
> > 
> > This is actually a reasonable explanation in terms of speed and loss. Let's see how it is being handled.
> > 
> > However, I would love it to be real - because breakthoughs do happen.
> > 
> > 
> > 


---

> ## JM
> 
> Hey [@artvolgin](https://www.kaggle.com/artvolgin) are you finding a data leak or something more clever? 
> 
> 
> 
> > ## SeshuRaju 🧘‍♂️
> > 
> > we will know in 30 hours !! [@julianmukaj](https://www.kaggle.com/julianmukaj) 
> > 
> > 
> > 
> > > ## Cody_Null
> > > 
> > > No clever technique is creating this gap on the worlds best in less than a 5th the time.
> > > 
> > > 
> > > 


---

> ## SeshuRaju 🧘‍♂️
> 
> 0.663 <- 0.707 ~ its margin itself 0.044
> 
> 
> 


---



* --- discussion numver 145, the number of votes :0 ---

# About Data Augmentation

**KeShuang Liu** *Sun Aug 04 2024 03:34:53 GMT+0900 (日本標準時)* (0 votes)

The competition is coming to an end. As a novice, this is my first time playing Kaggle. I encountered many problems and learned a lot. I was constantly fine-tuning the model before, but I had never enhanced the data. Today, I have realized all my ideas about fine-tuning the model. I have started a new exploration on how to get a higher score. I have learned some knowledge about data enhancement, including back-translation method and EDA method, and I am ready to use EDA for the next attempt. At the same time, I wonder if you have other methods you are willing to share.

[https://www.cnblogs.com/IllidanStormrage/p/16347433.html](https://www.cnblogs.com/IllidanStormrage/p/16347433.html)



---

 # Comments from other users

> ## Garvin Bhati
> 
> At this point in the competition, I don't think adding any additional data is going to improve the score, training set is already enough, and training hours are quite long. Using external data didn't improve the score for anyone as far as I can remember from the discussions, but I'll be curious to see if it works. 
> 
> 
> 
> > ## Garvin Bhati
> > 
> > I was trying to find ways to sample the data properly so that we could do more trials with different parameters.
> > 
> > 
> > 
> > ## Xinyuan Qiao
> > 
> > extra data works, but not in a simple way, we will find out in 48 hours
> > 
> > 
> > 


---

> ## KeShuang LiuTopic Author
> 
> For synonym replacement, what are some good ways to find its synonyms?
> 
> 
> 


---



* --- discussion numver 146, the number of votes :0 ---

# submission scoreing error

**Xin** *Fri Aug 02 2024 04:32:13 GMT+0900 (日本標準時)* (0 votes)

Has anyone meet this problem when using gemma?  I just changed the inputs.

Thanks!!!



---

 # Comments from other users

> ## Enter your display name
> 
> This could be caused by many reasons, but the most common one is likely that the number of rows in your output submission.csv file does not match test.csv after rerunning on all hidden test data.
> 
> 
> 
> > ## XinTopic Author
> > 
> > Thanks!
> > 
> > By using:
> > 
> > ```
> > !python /kaggle/usr/lib/lmsys_script/lmsys_script.py
> > import pandas as pd
> > lmsys_with_metadata = pd.read_csv("/kaggle/working/lmsys_with_metadata.csv")
> > !rm /kaggle/working/lmsys_with_metadata.csv
> > test_df = pd.read_csv("/kaggle/input/lmsys-chatbot-arena/test.csv")
> > if len(test_df) != len(lmsys_with_metadata):
> >     1/0
> > 
> > ```
> > 
> > I got Notebook Throw Exception which proves you must right.
> > 
> > Why lmsys_script.py (as a utility script) will output different length after submitting submission.csv.
> > 
> > Inside the lmsys_script.py:
> > 
> > df = pd.read_csv("/kaggle/input/lmsys-chatbot-arena/test.csv")
> > 
> > 
> > 
> > > ## XinTopic Author
> > > 
> > > lmsys_script.py (as a utility script) will output same length using train.csv and test.csv before submitting submission.csv.
> > > 
> > > 
> > > 
> > > ## XinTopic Author
> > > 
> > > Finally I abandoned using utility script way to release GPU then the problem solved.
> > > 
> > > 
> > > 


---



* --- discussion numver 147, the number of votes :0 ---

# Did you try to explode the conversation responses?

**Mattia Vanzetto** *Thu Aug 01 2024 04:42:15 GMT+0900 (日本標準時)* (0 votes)

Hello guys,

I saw that the ~86% of the training conversations is composed by just a single prompt + response, but 14% is not. I saw also that, at least in the public notebooks, the fine-tuned models usually have a maximum sequence lenght of 2000/2400 characters, and often the prompt assembled for the models are just prompt_list + response_a_list + response_b_list, which surely lead to cases where the response_b is completely truncated, or anyway to a loss of information.

Did you try to explode the responses, fine-tune a model and then aggregate the predictions on the single piece of the conversation?

The mean/median length of the single piece of conversation "prompt_i + response_a_i + response_b_i" is between 2000 and 2400 characters, which seems perfect for this expirement.

I would like to try myself, but I have no fine-tuning experience, no computing power, and no time 😂

For what it's worth, I tried with a simple xgboost, same features preparation, same optimization procedure, the exploding+aggregating approach got 1.03 on the leaderboard vs 1.04 of the standard approach.

Another expirement I would have liked to do is to build a binary classifier considering just prompt + response_X, with target the relative winner_model_X, basically duplicating the number of rows, without considering the "opponent's response", and then aggregate all back.

I am really looking forward to see the solutions after the competitions ends. 

Good luck for the last days of the competition 🍀



---

 # Comments from other users

> ## JM
> 
> I tried, it increase the inference time and did not see any improvement to public LB myself
> 
> 
> 


---

> ## Yi-Fu Chen
> 
> 
> Another expirement I would have liked to do is to build a binary classifier considering just prompt + response_X, with target the relative winner_model_X, basically duplicating the number of rows, without considering the "opponent's response", and then aggregate all back.
> 
> I have thought about a similar concept, but the intuition seems unreasonable because winning and losing are compared.
> 
> 
> 
> > ## Mattia VanzettoTopic Author
> > 
> > Do you mean loosing and tie? These two would be "compared" doing so.
> > 
> > 
> > 


---



* --- discussion numver 148, the number of votes :0 ---

# [Solved] trainer.train("checkpoint-1000") ignores the first samples?: Resuming training in Transformers library. 

**ano** *Thu Aug 01 2024 15:27:59 GMT+0900 (日本標準時)* (0 votes)

My question is if trainer.train("checkpoint-x") ignores the first samples?

For example, I first trained using 4000 samples as train_dataset and got checkpoint-200, 400, 600, 800 and the last checkpoint as checkpoint-1000. And then I resumed training using 4800 samples by trainer.train("checkpoint-1000") and I got only checkpoint-1000 and checkpoint-1200 (no directory corresponding to 200-800). Does that mean the first 4000 samples were skipped?

In order to resume training using new training datasets, do we need to add the first samples as "dummy"? 



---

 # Comments from other users

> ## yechenzhi1
> 
> Yes, resuming training involves bypassing the previously processed data. If you wish to modify your dataset, you can specify 'model_name' as 'checkpoint-1000' and subsequently fine-tune it using your 4800 samples.
> 
> However, if you do so, your model will see the 4000 samples twice, is this what you want?
> 
> 
> 
> > ## anoTopic Author
> > 
> > Thank you for clarifying!
> > 
> > In my case, I trained with dataset_a and retrained with dataset_b from the checkpoint, but it seemed like the first samples in dataset_b was ignored. That's why I experimented a bit and asked this question here. Your answer is very helpful. Thank you so much!
> > 
> > 
> > 


---



* --- discussion numver 149, the number of votes :0 ---

# Synthetic Closed source API

**Just A game on your lips** *Thu Aug 01 2024 09:34:24 GMT+0900 (日本標準時)* (0 votes)

Can I using another API such as: Chatgpt, gemini4o… to generate datasets for training model. 



---

 # Comments from other users

> ## Valentin Werner
> 
> That profile picture irritated me (Expected Nischay) 😀
> 
> On your question: The rules are quite vague, as there is a section about sharing non-open source data with the whole competition. However, in past competitions there were winning solutions that used self-generated data based on closed source models where data was not shared to my knowledge. Those guys still got a very deserved first place. Therefore, I would assume it to be okay. 
> 
> However, for rule questions it is always best to ask kaggle staff directly. 
> 
> 
> 
> > ## Just A game on your lipsTopic Author
> > 
> > thanks [@valentinwerner](https://www.kaggle.com/valentinwerner).  
> > 
> > 
> > 


---



* --- discussion numver 150, the number of votes :0 ---

# Help! TPU install error(From today)

**Robert0921** *Wed Jul 31 2024 14:58:46 GMT+0900 (日本標準時)* (0 votes)

Hello! When I installed TPU by the following steps,

!pip install -qq torch_xla[tpu]~=2.1.0 -f https://storage.googleapis.com/libtpu-releases/index.html -q

the following error occurred from today, What happened?

ERROR: Could not find a version that satisfies the requirement libtpu-nightly==0.1.dev20230825; extra == "tpu" (from torch-xla[tpu]) (from versions: 0.1.dev20210615+nightly, 0.1.dev20210709+nightly, 0.1.dev20210809+nightly, 0.1.dev20210916+nightly, 0.1.dev20210917+nightly, 0.1.dev20210920+nightly, 0.1.dev20210921+nightly, 0.1.dev20210922+nightly, 0.1.dev20210923+nightly, 0.1.dev20210924+nightly, 0.1.dev20210925+nightly, 0.1.dev20210926+nightly, 0.1.dev20210927+nightly, 0.1.dev20210928+nightly, 0.1.dev20210929+nightly, 0.1.dev20210930+nightly, 0.1.dev20211001+nightly, 0.1.dev20211002+nightly, 0.1.dev20211003+nightly, 0.1.dev20211004+nightly, 0.1.dev20211005+nightly, 0.1.dev20211006+nightly, 0.1.dev20211007+nightly, 0.1.dev20211008+nightly, 0.1.dev20211009+nightly, 0.1.dev20211010+nightly, 0.1.dev20211011+nightly, 0.1.dev20211012+nightly, 0.1.dev20211013+nightly, 0.1.dev20211014+nightly, 0.1.dev20211015+nightly, 0.1.dev20211016+nightly, 0.1.dev20211017+nightly, 0.1.dev20211018+nightly, 0.1.dev20211019+nightly, 0.1.dev20211020+nightly, 0.1.dev20211022+nightly, 0.1.dev20211023+nightly, 0.1.dev20211024+nightly, 0.1.dev20211025+nightly, 0.1.dev20211026+nightly, 0.1.dev20211027+nightly, 0.1.dev20211028+nightly, 0.1.dev20211029+nightly, 0.1.dev20211030+nightly, 0.1.dev20211031+nightly, 0.1.dev20211101+nightly, 0.1.dev20211102+nightly, 0.1.dev20211103+nightly, 0.1.dev20211104+nightly, 0.1.dev20211105+nightly, 0.1.dev20211106+nightly, 0.1.dev20211107+nightly, 0.1.dev20211108+nightly, 0.1.dev20211109+nightly, 0.1.dev20211110+nightly, 0.1.dev20211111+nightly, 0.1.dev20211112+nightly, 0.1.dev20211113+nightly, 0.1.dev20211114+nightly, 0.1.dev20211115+nightly, 0.1.dev20211117+nightly, 0.1.dev20211118+nightly, 0.1.dev20211119+nightly, 0.1.dev20211120+nightly, 0.1.dev20211121+nightly, 0.1.dev20211122+nightly, 0.1.dev20211123+nightly, 0.1.dev20211124+nightly, 0.1.dev20211125+nightly, 0.1.dev20211126+nightly, 0.1.dev20211127+nightly, 0.1.dev20211128+nightly, 0.1.dev20211129+nightly, 0.1.dev20211130+nightly, 0.1.dev20211201+nightly, 0.1.dev20211202+nightly, 0.1.dev20211203+nightly, 0.1.dev20211204+nightly, 0.1.dev20211205+nightly, 0.1.dev20211206+nightly, 0.1.dev20211207+nightly, 0.1.dev20211208+nightly, 0.1.dev20211209+nightly, 0.1.dev20211217+nightly, 0.1.dev20211229+nightly, 0.1.dev20211230+nightly, 0.1.dev20211231+nightly, 0.1.dev20220101+nightly, 0.1.dev20220102+nightly, 0.1.dev20220103+nightly, 0.1.dev20220104+nightly, 0.1.dev20220105+nightly, 0.1.dev20220106+nightly, 0.1.dev20220107+nightly, 0.1.dev20220108+nightly, 0.1.dev20220109+nightly, 0.1.dev20220110+nightly, 0.1.dev20220111+nightly, 0.1.dev20220114+nightly, 0.1.dev20220115+nightly, 0.1.dev20220116+nightly, 0.1.dev20220117+nightly, 0.1.dev20220118+nightly, 0.1.dev20220119+nightly, 0.1.dev20220126+nightly, 0.1.dev20220127+nightly, 0.1.dev20220128+nightly, 0.1.dev20220202+nightly, 0.1.dev20220203+nightly, 0.1.dev20220204+nightly, 0.1.dev20220205+nightly, 0.1.dev20220206+nightly, 0.1.dev20220207+nightly, 0.1.dev20220208+nightly, 0.1.dev20220209+nightly, 0.1.dev20220210+nightly, 0.1.dev20220211+nightly, 0.1.dev20220212+nightly, 0.1.dev20220213+nightly, 0.1.dev20220214+nightly, 0.1.dev20220215+nightly, 0.1.dev20220216+nightly, 0.1.dev20220217+nightly, 0.1.dev20220218+nightly, 0.1.dev20220219+nightly, 0.1.dev20220220+nightly, 0.1.dev20220221+nightly, 0.1.dev20220222+nightly, 0.1.dev20220223+nightly, 0.1.dev20220224+nightly, 0.1.dev20220225+nightly, 0.1.dev20220226+nightly, 0.1.dev20220227+nightly, 0.1.dev20220228+nightly, 0.1.dev20220301+nightly, 0.1.dev20220303+nightly, 0.1.dev20220304+nightly, 0.1.dev20220305+nightly, 0.1.dev20220306+nightly, 0.1.dev20220307+nightly, 0.1.dev20220308+nightly, 0.1.dev20220309+nightly, 0.1.dev20220310+nightly, 0.1.dev20220311+nightly, 0.1.dev20220312+nightly, 0.1.dev20220313+nightly, 0.1.dev20220314+nightly, 0.1.dev20220315+nightly, 0.1.dev20220316+nightly, 0.1.dev20220317+nightly, 0.1.dev20220318+nightly, 0.1.dev20220319+nightly, 0.1.dev20220320+nightly, 0.1.dev20220321+nightly, 0.1.dev20220322+nightly, 0.1.dev20220323+nightly, 0.1.dev20220324+nightly, 0.1.dev20220325+nightly, 0.1.dev20220326+nightly, 0.1.dev20220327+nightly, 0.1.dev20220328+nightly, 0.1.dev20220329+nightly, 0.1.dev20220407+nightly, 0.1.dev20220408+nightly, 0.1.dev20220409+nightly, 0.1.dev20220410+nightly, 0.1.dev20220411+nightly, 0.1.dev20220412+nightly, 0.1.dev20220413+nightly, 0.1.dev20220414+nightly, 0.1.dev20220415+nightly, 0.1.dev20220416+nightly, 0.1.dev20220417+nightly, 0.1.dev20220418+nightly, 0.1.dev20220419+nightly, 0.1.dev20220420+nightly, 0.1.dev20220503+nightly, 0.1.dev20220504+nightly, 0.1.dev20220505+nightly, 0.1.dev20220506+nightly, 0.1.dev20220507+nightly, 0.1.dev20220509+nightly, 0.1.dev20220510+nightly, 0.1.dev20220511+nightly, 0.1.dev20220515+nightly, 0.1.dev20220516+nightly, 0.1.dev20220517+nightly, 0.1.dev20220518+nightly, 0.1.dev20220520+nightly, 0.1.dev20220521+nightly, 0.1.dev20220522+nightly, 0.1.dev20220524+nightly, 0.1.dev20220526+nightly, 0.1.dev20220527+nightly, 0.1.dev20220528+nightly, 0.1.dev20220529+nightly, 0.1.dev20220530+nightly, 0.1.dev20220531+nightly, 0.1.dev20220601+nightly, 0.1.dev20220602+nightly, 0.1.dev20220603+nightly, 0.1.dev20220604+nightly, 0.1.dev20220605+nightly, 0.1.dev20220606+nightly, 0.1.dev20220607+nightly, 0.1.dev20220608+nightly, 0.1.dev20220609+nightly, 0.1.dev20220610+nightly, 0.1.dev20220611+nightly, 0.1.dev20220612+nightly, 0.1.dev20220613+nightly, 0.1.dev20220614+nightly, 0.1.dev20220615+nightly, 0.1.dev20220616+nightly, 0.1.dev20220617+nightly, 0.1.dev20220618+nightly, 0.1.dev20220619+nightly, 0.1.dev20220620+nightly, 0.1.dev20220621+nightly, 0.1.dev20220622+nightly, 0.1.dev20220623+nightly, 0.1.dev20220624+nightly, 0.1.dev20220625+nightly, 0.1.dev20220626+nightly, 0.1.dev20220627+nightly, 0.1.dev20220628+nightly, 0.1.dev20220629+nightly, 0.1.dev20220630+nightly, 0.1.dev20220701+nightly, 0.1.dev20220702+nightly, 0.1.dev20220703+nightly, 0.1.dev20220704+nightly, 0.1.dev20220705+nightly, 0.1.dev20220706+nightly, 0.1.dev20220707+nightly, 0.1.dev20220708+nightly, 0.1.dev20220709+nightly, 0.1.dev20220710+nightly, 0.1.dev20220711+nightly, 0.1.dev20220713+nightly, 0.1.dev20220714+nightly, 0.1.dev20220715+nightly, 0.1.dev20220716+nightly, 0.1.dev20220717+nightly, 0.1.dev20220718+nightly, 0.1.dev20220719+nightly, 0.1.dev20220720+nightly, 0.1.dev20220721+nightly, 0.1.dev20220722+nightly, 0.1.dev20220723+nightly, 0.1.dev20220724+nightly, 0.1.dev20220725+nightly, 0.1.dev20220726+nightly, 0.1.dev20220727+nightly, 0.1.dev20220728+nightly, 0.1.dev20220729+nightly, 0.1.dev20220730+nightly, 0.1.dev20220731+nightly, 0.1.dev20220801+nightly, 0.1.dev20220802+nightly, 0.1.dev20220803+nightly, 0.1.dev20220804+nightly, 0.1.dev20220806+nightly, 0.1.dev20220807+nightly, 0.1.dev20220808+nightly, 0.1.dev20220809+nightly, 0.1.dev20220810+nightly, 0.1.dev20220812+nightly, 0.1.dev20220813+nightly, 0.1.dev20220814+nightly, 0.1.dev20220815+nightly, 0.1.dev20220816+nightly, 0.1.dev20220824+nightly, 0.1.dev20220908+nightly, 0.1.dev20220909+nightly, 0.1.dev20220910+nightly, 0.1.dev20220912+nightly, 0.1.dev20220913+nightly, 0.1.dev20220914+nightly, 0.1.dev20220915+nightly, 0.1.dev20220916+nightly, 0.1.dev20220917+nightly, 0.1.dev20220918+nightly, 0.1.dev20220919+nightly, 0.1.dev20220920+nightly, 0.1.dev20220921+nightly, 0.1.dev20220922+nightly, 0.1.dev20220923+nightly, 0.1.dev20220924+nightly, 0.1.dev20220925+nightly, 0.1.dev20220926+nightly, 0.1.dev20220927+nightly, 0.1.dev20220928+nightly, 0.1.dev20220929+nightly, 0.1.dev20220930+nightly, 0.1.dev20221001+nightly, 0.1.dev20221002+nightly, 0.1.dev20221003+nightly, 0.1.dev20221004+nightly, 0.1.dev20221005+nightly, 0.1.dev20221006+nightly, 0.1.dev20221007+nightly, 0.1.dev20221008+nightly, 0.1.dev20221009+nightly, 0.1.dev20221010+nightly, 0.1.dev20221011+nightly, 0.1.dev20221012+nightly, 0.1.dev20221013+nightly, 0.1.dev20221014+nightly, 0.1.dev20221015+nightly, 0.1.dev20221016+nightly, 0.1.dev20221017+nightly, 0.1.dev20221018+nightly, 0.1.dev20221019+nightly, 0.1.dev20221020+nightly, 0.1.dev20221021+nightly, 0.1.dev20221022+nightly, 0.1.dev20221023+nightly, 0.1.dev20221024+nightly, 0.1.dev20221025+nightly, 0.1.dev20221026+nightly, 0.1.dev20221027+nightly, 0.1.dev20221028+nightly, 0.1.dev20221029+nightly, 0.1.dev20221030+nightly, 0.1.dev20221031+nightly, 0.1.dev20221101+nightly, 0.1.dev20221102+nightly, 0.1.dev20221103+nightly, 0.1.dev20221104+nightly, 0.1.dev20221105+nightly, 0.1.dev20221106+nightly, 0.1.dev20221107+nightly, 0.1.dev20221108+nightly, 0.1.dev20221109+nightly, 0.1.dev20221115+nightly, 0.1.dev20221117+nightly, 0.1.dev20221118+nightly, 0.1.dev20221119+nightly, 0.1.dev20221120+nightly, 0.1.dev20221121+nightly, 0.1.dev20221122+nightly, 0.1.dev20221123+nightly, 0.1.dev20221124+nightly, 0.1.dev20221125+nightly, 0.1.dev20221126+nightly, 0.1.dev20221127+nightly, 0.1.dev20221128+nightly, 0.1.dev20221129+nightly, 0.1.dev20221130+nightly, 0.1.dev20221201+nightly, 0.1.dev20221202+nightly, 0.1.dev20221203+nightly, 0.1.dev20221204+nightly, 0.1.dev20221205+nightly, 0.1.dev20221206+nightly, 0.1.dev20221207+nightly, 0.1.dev20221208+nightly, 0.1.dev20221209+nightly, 0.1.dev20221210+nightly, 0.1.dev20221211+nightly, 0.1.dev20221212+nightly, 0.1.dev20221213+nightly, 0.1.dev20221214+nightly, 0.1.dev20221216+nightly, 0.1.dev20221217+nightly, 0.1.dev20221218+nightly, 0.1.dev20221219+nightly, 0.1.dev20221220+nightly, 0.1.dev20221221+nightly, 0.1.dev20221222+nightly, 0.1.dev20221223+nightly, 0.1.dev20221224+nightly, 0.1.dev20221225+nightly, 0.1.dev20221226+nightly, 0.1.dev20221227+nightly, 0.1.dev20221228+nightly, 0.1.dev20221229+nightly, 0.1.dev20221230+nightly, 0.1.dev20221231+nightly, 0.1.dev20230101+nightly, 0.1.dev20230102+nightly, 0.1.dev20230103+nightly, 0.1.dev20230104+nightly, 0.1.dev20230105+nightly, 0.1.dev20230106+nightly, 0.1.dev20230107+nightly, 0.1.dev20230108+nightly, 0.1.dev20230109+nightly, 0.1.dev20230110+nightly, 0.1.dev20230111+nightly, 0.1.dev20230112+nightly, 0.1.dev20230113+nightly, 0.1.dev20230114+nightly, 0.1.dev20230115+nightly, 0.1.dev20230116+nightly, 0.1.dev20230117+nightly, 0.1.dev20230118+nightly, 0.1.dev20230119+nightly, 0.1.dev20230120+nightly, 0.1.dev20230121+nightly, 0.1.dev20230122+nightly, 0.1.dev20230123+nightly, 0.1.dev20230124+nightly, 0.1.dev20230125+nightly, 0.1.dev20230126+nightly, 0.1.dev20230127+nightly, 0.1.dev20230128+nightly, 0.1.dev20230129+nightly, 0.1.dev20230130+nightly, 0.1.dev20230131+nightly, 0.1.dev20230201+nightly, 0.1.dev20230202+nightly, 0.1.dev20230203+nightly, 0.1.dev20230204+nightly, 0.1.dev20230205+nightly, 0.1.dev20230206+nightly, 0.1.dev20230207+nightly, 0.1.dev20230208+nightly, 0.1.dev20230209+nightly, 0.1.dev20230210+nightly, 0.1.dev20230211+nightly, 0.1.dev20230212+nightly, 0.1.dev20230213+nightly, 0.1.dev20230214+nightly, 0.1.dev20230215+nightly, 0.1.dev20230216+nightly, 0.1.dev20230217+nightly, 0.1.dev20230218+nightly, 0.1.dev20230219+nightly, 0.1.dev20230220+nightly, 0.1.dev20230221+nightly, 0.1.dev20230222+nightly, 0.1.dev20230223+nightly, 0.1.dev20230224+nightly, 0.1.dev20230225+nightly, 0.1.dev20230226+nightly, 0.1.dev20230228+nightly, 0.1.dev20230301+nightly, 0.1.dev20230302+nightly, 0.1.dev20230303+nightly, 0.1.dev20230304+nightly, 0.1.dev20230305+nightly, 0.1.dev20230306+nightly, 0.1.dev20230307+nightly, 0.1.dev20230308+nightly, 0.1.dev20230309+nightly, 0.1.dev20230310+nightly, 0.1.dev20230311+nightly, 0.1.dev20230312+nightly, 0.1.dev20230313+nightly, 0.1.dev20230314+nightly, 0.1.dev20230315+nightly, 0.1.dev20230316+nightly, 0.1.dev20230317+nightly, 0.1.dev20230318+nightly, 0.1.dev20230319+nightly, 0.1.dev20230320+nightly, 0.1.dev20230321+nightly, 0.1.dev20230322+nightly, 0.1.dev20230323+nightly, 0.1.dev20230324+nightly, 0.1.dev20230325+nightly, 0.1.dev20230326+nightly, 0.1.dev20230327+nightly, 0.1.dev20230328+nightly, 0.1.dev20230329+nightly, 0.1.dev20230330+nightly, 0.1.dev20230331+nightly, 0.1.dev20230401+nightly, 0.1.dev20230402+nightly, 0.1.dev20230403+nightly, 0.1.dev20230404+nightly, 0.1.dev20230405+nightly, 0.1.dev20230406+nightly, 0.1.dev20230407+nightly, 0.1.dev20230408+nightly, 0.1.dev20230409+nightly, 0.1.dev20230410+nightly, 0.1.dev20230411+nightly, 0.1.dev20230412+nightly, 0.1.dev20230413+nightly, 0.1.dev20230414+nightly, 0.1.dev20230415+nightly, 0.1.dev20230416+nightly, 0.1.dev20230417+nightly, 0.1.dev20230418+nightly, 0.1.dev20230419+nightly, 0.1.dev20230420+nightly, 0.1.dev20230421+nightly, 0.1.dev20230422+nightly, 0.1.dev20230423+nightly, 0.1.dev20230424+nightly, 0.1.dev20230425+nightly, 0.1.dev20230426+nightly, 0.1.dev20230427+nightly, 0.1.dev20230428+nightly, 0.1.dev20230429+nightly, 0.1.dev20230430+nightly, 0.1.dev20230501+nightly, 0.1.dev20230502+nightly, 0.1.dev20230503+nightly, 0.1.dev20230504+nightly, 0.1.dev20230505+nightly, 0.1.dev20230506+nightly, 0.1.dev20230507+nightly, 0.1.dev20230508+nightly, 0.1.dev20230509+nightly, 0.1.dev20230510+nightly, 0.1.dev20230511+nightly, 0.1.dev20230512+nightly, 0.1.dev20230513+nightly, 0.1.dev20230514+nightly, 0.1.dev20230515+nightly, 0.1.dev20230516+nightly, 0.1.dev20230517+nightly, 0.1.dev20230518+nightly, 0.1.dev20230519+nightly, 0.1.dev20230520+nightly, 0.1.dev20230521+nightly, 0.1.dev20230522+nightly, 0.1.dev20230523+nightly, 0.1.dev20230524+nightly, 0.1.dev20230525+nightly, 0.1.dev20230526+nightly, 0.1.dev20230527+nightly, 0.1.dev20230528+nightly, 0.1.dev20230529+nightly, 0.1.dev20230530+nightly, 0.1.dev20230531+nightly, 0.1.dev20230601+nightly, 0.1.dev20230602+nightly, 0.1.dev20230603+nightly, 0.1.dev20230604+nightly, 0.1.dev20230605+nightly, 0.1.dev20230606+nightly, 0.1.dev20230607+nightly, 0.1.dev20230608+nightly, 0.1.dev20230609+nightly, 0.1.dev20230610+nightly, 0.1.dev20230611+nightly, 0.1.dev20230612+nightly, 0.1.dev20230613+nightly, 0.1.dev20230614+nightly, 0.1.dev20230615+nightly, 0.1.dev20230616+nightly, 0.1.dev20230617+nightly, 0.1.dev20230618+nightly, 0.1.dev20230619+nightly, 0.1.dev20230620+nightly, 0.1.dev20230621+nightly, 0.1.dev20230622+nightly, 0.1.dev20230623+nightly, 0.1.dev20230624+nightly, 0.1.dev20230625+nightly, 0.1.dev20230626+nightly, 0.1.dev20230627+nightly, 0.1.dev20230628+nightly, 0.1.dev20230629+nightly, 0.1.dev20230630+nightly, 0.1.dev20230701+nightly, 0.1.dev20230702+nightly, 0.1.dev20230703+nightly, 0.1.dev20230704+nightly, 0.1.dev20230705+nightly, 0.1.dev20230706+nightly, 0.1.dev20230707+nightly, 0.1.dev20230708+nightly, 0.1.dev20230709+nightly, 0.1.dev20230710+nightly, 0.1.dev20230711+nightly, 0.1.dev20230712+nightly, 0.1.dev20230715+nightly, 0.1.dev20230716+nightly, 0.1.dev20230717+nightly, 0.1.dev20230718+nightly, 0.1.dev20230719+nightly, 0.1.dev20230720+nightly, 0.1.dev20230721+nightly, 0.1.dev20230722+nightly, 0.1.dev20230723+nightly, 0.1.dev20230724+nightly, 0.1.dev20230725+nightly, 0.1.dev20230726+nightly, 0.1.dev20230727+nightly, 0.1.dev20230802+nightly, 0.1.dev20230803+nightly, 0.1.dev20230804+nightly, 0.1.dev20230805+nightly, 0.1.dev20230806+nightly, 0.1.dev20230807+nightly, 0.1.dev20230808+nightly, 0.1.dev20230809+nightly, 0.1.dev20230810+nightly, 0.1.dev20230815+nightly, 0.1.dev20230816+nightly, 0.1.dev20230817+nightly, 0.1.dev20230818+nightly, 0.1.dev20230819+nightly, 0.1.dev20230820+nightly, 0.1.dev20230821+nightly, 0.1.dev20230823+nightly, 0.1.dev20230824+nightly, 0.1.dev20230825+nightly, 0.1.dev20230826+nightly, 0.1.dev20230827+nightly, 0.1.dev20230828+nightly, 0.1.dev20230829+nightly, 0.1.dev20230830+nightly, 0.1.dev20230831+nightly, 0.1.dev20230911+nightly, 0.1.dev20230912+nightly, 0.1.dev20230913+nightly, 0.1.dev20230914+nightly, 0.1.dev20230915+nightly, 0.1.dev20230916+nightly, 0.1.dev20230917+nightly, 0.1.dev20230918+nightly, 0.1.dev20230919+nightly, 0.1.dev20230920+nightly, 0.1.dev20230921+nightly, 0.1.dev20230922+nightly, 0.1.dev20230923+nightly, 0.1.dev20230924+nightly, 0.1.dev20230925+nightly, 0.1.dev20230926+nightly, 0.1.dev20230927+nightly, 0.1.dev20230928+nightly, 0.1.dev20230929+nightly, 0.1.dev20230930+nightly, 0.1.dev20231001+nightly, 0.1.dev20231002+nightly, 0.1.dev20231003+nightly, 0.1.dev20231004+nightly, 0.1.dev20231005+nightly, 0.1.dev20231006+nightly, 0.1.dev20231007+nightly, 0.1.dev20231008+nightly, 0.1.dev20231009+nightly, 0.1.dev20231010+nightly, 0.1.dev20231011+nightly, 0.1.dev20231012+nightly, 0.1.dev20231013+nightly, 0.1.dev20231014+nightly, 0.1.dev20231015+nightly, 0.1.dev20231016+nightly, 0.1.dev20231017+nightly, 0.1.dev20231018+nightly, 0.1.dev20231019+nightly, 0.1.dev20231020+nightly, 0.1.dev20231021+nightly, 0.1.dev20231022+nightly, 0.1.dev20231023+nightly, 0.1.dev20231024+nightly, 0.1.dev20231025+nightly, 0.1.dev20231026+nightly, 0.1.dev20231027+nightly, 0.1.dev20231028+nightly, 0.1.dev20231029+nightly, 0.1.dev20231030+nightly, 0.1.dev20231031+nightly, 0.1.dev20231101+nightly, 0.1.dev20231102+nightly, 0.1.dev20231103+nightly, 0.1.dev20231104+nightly, 0.1.dev20231105+nightly, 0.1.dev20231106+nightly, 0.1.dev20231107+nightly, 0.1.dev20231114+nightly, 0.1.dev20231115+nightly, 0.1.dev20231116+nightly, 0.1.dev20231117+nightly, 0.1.dev20231118+nightly, 0.1.dev20231119+nightly, 0.1.dev20231120+nightly, 0.1.dev20231121+nightly, 0.1.dev20231122+nightly, 0.1.dev20231123+nightly, 0.1.dev20231124+nightly, 0.1.dev20231125+nightly, 0.1.dev20231126+nightly, 0.1.dev20231127+nightly, 0.1.dev20231128+nightly, 0.1.dev20231129+nightly, 0.1.dev20231130+nightly, 0.1.dev20231201+nightly, 0.1.dev20231202+nightly, 0.1.dev20231203+nightly, 0.1.dev20231204+nightly, 0.1.dev20231205+nightly, 0.1.dev20231206+nightly, 0.1.dev20231207+nightly, 0.1.dev20231208+nightly, 0.1.dev20231209+nightly, 0.1.dev20231210+nightly, 0.1.dev20231211+nightly, 0.1.dev20231212+nightly, 0.1.dev20231213+nightly, 0.1.dev20231214+nightly, 0.1.dev20231215+nightly, 0.1.dev20231216+nightly, 0.1.dev20231217+nightly, 0.1.dev20231218+nightly, 0.1.dev20231219+nightly, 0.1.dev20231220+nightly, 0.1.dev20231221+nightly, 0.1.dev20231222+nightly, 0.1.dev20231223+nightly, 0.1.dev20231224+nightly, 0.1.dev20231225+nightly, 0.1.dev20231226+nightly, 0.1.dev20231227+nightly, 0.1.dev20231228+nightly, 0.1.dev20231229+nightly, 0.1.dev20231230+nightly, 0.1.dev20231231+nightly, 0.1.dev20240101+nightly, 0.1.dev20240102+nightly, 0.1.dev20240103+nightly, 0.1.dev20240104+nightly, 0.1.dev20240105+nightly, 0.1.dev20240106+nightly, 0.1.dev20240107+nightly, 0.1.dev20240108+nightly, 0.1.dev20240109+nightly, 0.1.dev20240110+nightly, 0.1.dev20240111+nightly, 0.1.dev20240113+nightly, 0.1.dev20240114+nightly, 0.1.dev20240115+nightly, 0.1.dev20240116+nightly, 0.1.dev20240117+nightly, 0.1.dev20240118+nightly, 0.1.dev20240119+nightly, 0.1.dev20240120+nightly, 0.1.dev20240121+nightly, 0.1.dev20240122+nightly, 0.1.dev20240123+nightly, 0.1.dev20240124+nightly, 0.1.dev20240127+nightly, 0.1.dev20240128+nightly, 0.1.dev20240129+nightly, 0.1.dev20240130+nightly, 0.1.dev20240131+nightly, 0.1.dev20240201+nightly, 0.1.dev20240202+nightly, 0.1.dev20240203+nightly, 0.1.dev20240204+nightly, 0.1.dev20240205+nightly, 0.1.dev20240206+nightly, 0.1.dev20240207+nightly, 0.1.dev20240208+nightly, 0.1.dev20240209+nightly, 0.1.dev20240210+nightly, 0.1.dev20240213+nightly, 0.1.dev20240214+nightly, 0.1.dev20240215+nightly, 0.1.dev20240216+nightly, 0.1.dev20240217+nightly, 0.1.dev20240218+nightly, 0.1.dev20240219+nightly, 0.1.dev20240220+nightly, 0.1.dev20240221+nightly, 0.1.dev20240222+nightly, 0.1.dev20240223+nightly, 0.1.dev20240224+nightly, 0.1.dev20240225+nightly, 0.1.dev20240226+nightly, 0.1.dev20240227+nightly, 0.1.dev20240228+nightly, 0.1.dev20240229+nightly, 0.1.dev20240301+nightly, 0.1.dev20240302+nightly, 0.1.dev20240303+nightly, 0.1.dev20240304+nightly, 0.1.dev20240305+nightly, 0.1.dev20240306+nightly, 0.1.dev20240307+nightly, 0.1.dev20240308+nightly, 0.1.dev20240309+nightly, 0.1.dev20240310+nightly, 0.1.dev20240311+nightly, 0.1.dev20240312+nightly, 0.1.dev20240313+nightly, 0.1.dev20240314+nightly, 0.1.dev20240315+nightly, 0.1.dev20240316+nightly, 0.1.dev20240317+nightly, 0.1.dev20240318+nightly, 0.1.dev20240319+nightly, 0.1.dev20240320+nightly, 0.1.dev20240321+nightly, 0.1.dev20240322+nightly, 0.1.dev20240323+nightly, 0.1.dev20240324+nightly, 0.1.dev20240325+nightly, 0.1.dev20240326+nightly, 0.1.dev20240327+nightly, 0.1.dev20240328+nightly, 0.1.dev20240329+nightly, 0.1.dev20240330+nightly, 0.1.dev20240331+nightly, 0.1.dev20240401+nightly, 0.1.dev20240402+nightly, 0.1.dev20240403+nightly, 0.1.dev20240404+nightly, 0.1.dev20240405+nightly, 0.1.dev20240406+nightly, 0.1.dev20240407+nightly, 0.1.dev20240408+nightly, 0.1.dev20240409+nightly, 0.1.dev20240410+nightly, 0.1.dev20240411+nightly, 0.1.dev20240412+nightly, 0.1.dev20240413+nightly, 0.1.dev20240414+nightly, 0.1.dev20240415+nightly, 0.1.dev20240416+nightly, 0.1.dev20240417+nightly, 0.1.dev20240418+nightly, 0.1.dev20240419+nightly, 0.1.dev20240420+nightly, 0.1.dev20240421+nightly, 0.1.dev20240422+nightly, 0.1.dev20240423+nightly, 0.1.dev20240424+nightly, 0.1.dev20240425+nightly, 0.1.dev20240426+nightly, 0.1.dev20240427+nightly, 0.1.dev20240428+nightly, 0.1.dev20240429+nightly, 0.1.dev20240430+nightly, 0.1.dev20240501+nightly, 0.1.dev20240502+nightly, 0.1.dev20240503+nightly, 0.1.dev20240504+nightly, 0.1.dev20240505+nightly, 0.1.dev20240506+nightly, 0.1.dev20240507+nightly, 0.1.dev20240508+nightly, 0.1.dev20240509+nightly, 0.1.dev20240510+nightly, 0.1.dev20240511+nightly, 0.1.dev20240512+nightly, 0.1.dev20240513+nightly, 0.1.dev20240515+nightly, 0.1.dev20240516+nightly, 0.1.dev20240517+nightly, 0.1.dev20240518+nightly, 0.1.dev20240519+nightly, 0.1.dev20240520+nightly, 0.1.dev20240521+nightly, 0.1.dev20240522+nightly, 0.1.dev20240523+nightly, 0.1.dev20240524+nightly, 0.1.dev20240525+nightly, 0.1.dev20240526+nightly, 0.1.dev20240527+nightly, 0.1.dev20240528+nightly, 0.1.dev20240529+nightly, 0.1.dev20240531+nightly, 0.1.dev20240601+nightly, 0.1.dev20240602+nightly, 0.1.dev20240603+nightly, 0.1.dev20240604+nightly, 0.1.dev20240605+nightly, 0.1.dev20240606+nightly, 0.1.dev20240607+nightly, 0.1.dev20240608+nightly, 0.1.dev20240609+nightly, 0.1.dev20240610+nightly, 0.1.dev20240611+nightly, 0.1.dev20240612+nightly, 0.1.dev20240613+nightly, 0.1.dev20240614+nightly, 0.1.dev20240615+nightly, 0.1.dev20240616+nightly, 0.1.dev20240617+nightly, 0.1.dev20240618+nightly, 0.1.dev20240619+nightly, 0.1.dev20240620+nightly, 0.1.dev20240621+nightly, 0.1.dev20240622+nightly, 0.1.dev20240623+nightly, 0.1.dev20240624+nightly, 0.1.dev20240625+nightly, 0.1.dev20240626+nightly, 0.1.dev20240627+nightly, 0.1.dev20240628+nightly, 0.1.dev20240629+nightly, 0.1.dev20240630+nightly, 0.1.dev20240701+nightly, 0.1.dev20240702+nightly, 0.1.dev20240703+nightly, 0.1.dev20240704+nightly, 0.1.dev20240705+nightly, 0.1.dev20240706+nightly, 0.1.dev20240707+nightly, 0.1.dev20240708+nightly, 0.1.dev20240709+nightly, 0.1.dev20240710+nightly, 0.1.dev20240711+nightly, 0.1.dev20240712+nightly, 0.1.dev20240713+nightly, 0.1.dev20240714+nightly, 0.1.dev20240715+nightly, 0.1.dev20240716+nightly, 0.1.dev20240717+nightly, 0.1.dev20240718+nightly, 0.1.dev20240719+nightly, 0.1.dev20240720+nightly, 0.1.dev20240721+nightly, 0.1.dev20240722+nightly, 0.1.dev20240723+nightly, 0.1.dev20240724+nightly, 0.1.dev20240725+nightly, 0.1.dev20240726+nightly, 0.1.dev20240727+nightly, 0.1.dev20240728+nightly, 0.1.dev20240729+nightly, 0.1.dev20240730+nightly, 0.1.dev20240731+nightly)

ERROR: No matching distribution found for libtpu-nightly==0.1.dev20230825; extra == "tpu"



---

 # Comments from other users

> ## Sergey Bryansky
> 
> It seems there is problem with python env in new docker image, dirty fix is
> 
> !pip install torch~=2.1.0 torch_xla[tpu]~=2.1.0 -f https://storage.googleapis.com/libtpu-releases/index.html -q --use-deprecated=legacy-resolver
> 
> 
> 


---

> ## dddmd
> 
> I ran into the same problem today, but was able to install it just now.
> 
> 
> 


---

> ## Lorry Zou
> 
> I ran into exactly the same issue today.
> 
> 
> 


---



* --- discussion numver 151, the number of votes :0 ---

# Does increase the batch size of gemma2 9b in training do some help?

**Dlond Mike** *Sun Jul 28 2024 09:06:07 GMT+0900 (日本標準時)* (0 votes)

i new here and i'm quite confused about this



---

 # Comments from other users

> ## xiaotingting
> 
> It seems that we need to use grid search to find a suitable learning rate when the batch size is fixed. If the graphics card has some spare capacity, we can actually scale the batch size and learning rate proportionally. Generally speaking, we can think that scaling the batch size and learning rate proportionally is equivalent.
> 
> 
> 
> > ## Z Hello
> > 
> > Should the learning rate and batch size be increased or decreased simultaneously?
> > 
> > 
> > 


---

> ## ano
> 
> I also want to know how everyone chooses batch size, learning rate and architecture (like gate_proj, q_proj… when using lora)
> 
> 
> 
> > ## Dlond MikeTopic Author
> > 
> > 🥹some tips?
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > All the insights coming in 9 days 😉
> > > 
> > > 
> > > 


---



* --- discussion numver 152, the number of votes :0 ---

# Is there verbosity bias?

**OHIRA** *Tue Jul 30 2024 17:37:18 GMT+0900 (日本標準時)* (0 votes)

I'm using Llama 3 , Is there serious verbosity bias ?

If there is the bias, I want to know how to prevent it using prompt technique.





* --- discussion numver 153, the number of votes :0 ---

# Help! Loss function not behaving as expected!

**Shreyansh Murathia** *Sat Jul 27 2024 22:43:41 GMT+0900 (日本標準時)* (0 votes)

pred = torch.tensor([[1.0, 0.0, 0.0]])

target = torch.tensor([0])

loss_fct = nn.CrossEntropyLoss()

​

loss = loss_fct(pred, target)

loss

​

tensor(0.5514)

Should'nt the loss be 0 or a very small value? Why is it returning 0.5514? 

I am really sorry if this question is very easy. I am fairly new to this loss. 



---

 # Comments from other users

> ## sayoulala
> 
> Answer from gpt4:
> 
> No need to apologize! Your question is absolutely valid, and I'm here to help clarify it for you.
> 
> In your scenario, you are using nn.CrossEntropyLoss from PyTorch, which combines nn.LogSoftmax and nn.NLLLoss (negative log likelihood loss). Let me break down your example and explain why you are getting a loss value of 0.5514.
> 
> CrossEntropyLoss in PyTorch
> 
> nn.CrossEntropyLoss expects:
> 
> pred (predictions): a 2D tensor of raw, unnormalized scores for each class (often called "logits"). Shape: (batch_size, num_classes).
> 
> target: a 1D tensor of the true class indices. Shape: (batch_size,).
> 
> The CrossEntropyLoss applies a LogSoftmax function to the raw scores first, converting them into log-probabilities. It then uses the NLLLoss to compute the negative log likelihood of the correct class.
> 
> In your example:
> 
> python
> 
> import torch
> 
> import torch.nn as nn
> 
> pred = torch.tensor([[1.0, 0.0, 0.0]])
> 
> target = torch.tensor([0])
> 
> loss_fct = nn.CrossEntropyLoss()
> 
> loss = loss_fct(pred, target)
> 
> print(loss)  # Output: tensor(0.5514)
> 
> Step-by-Step Explanation
> 
> Raw logits (pred):
> 
> python
> 
> [[1.0, 0.0, 0.0]]
> 
> Applying LogSoftmax to logits: The LogSoftmax transformation converts logits to log-probabilities. For pred, the resulting log-probabilities are calculated as:
> 
> python
> 
> log_probabilities = torch.log_softmax(pred, dim=1)
> 
> The softmax transformation for your pred would be:
> 
> python
> 
> softmax(pred) = [exp(1.0)/sum(exp(1.0) + exp(0.0) + exp(0.0)),
> 
>                  exp(0.0)/sum(exp(1.0) + exp(0.0) + exp(0.0)),
> 
>                  exp(0.0)/sum(exp(1.0) + exp(0.0) + exp(0.0))]
> 
>              ≈ [0.5761, 0.2119, 0.2119]
> 
> Applying log to the softmax probabilities gives us:
> 
> python
> 
> log_probabilities = [log(0.5761), log(0.2119), log(0.2119)]
> 
>                   ≈ [-0.5514, -1.5514, -1.5514]
> 
> Negative Log Likelihood of the target class: Since the target class is 0 (target = [0]), we take the log-probability of the first element:
> 
> python
> 
> loss = -log_probabilities[0]
> 
>      = -(-0.5514)
> 
>      = 0.5514
> 
> Summary
> 
> The loss value of 0.5514 is not incorrect. It is derived from the log-probability of the correct class (class 0) for your prediction. The fact that the prediction is not perfect (with a raw logit of 1.0 vs. 0.0 for other classes) leads to a non-zero loss.
> 
> Had the logit for class 0 been significantly higher (e.g., [10.0, 0.0, 0.0]), the softmax probability for class 0 would be closer to 1, resulting in a loss closer to 0. Here, the logit of 1 is not high enough to give a near-zero softmax probability and thus results in a non-zero loss.
> 
> Feel free to ask if you have other questions or need further clarification!
> 
> 
> 
> > ## sayoulala
> > 
> > The input should not be probabilities; it should be the values before applying softmax.
> > 
> > 
> > 
> > ## Shreyansh MurathiaTopic Author
> > 
> > Thanks a lot 😊
> > 
> > 
> > 


---



* --- discussion numver 154, the number of votes :0 ---

# An idea to use Reward Model

**bao** *Fri Jul 26 2024 20:02:28 GMT+0900 (日本標準時)* (0 votes)

Hello, kagglers：

I have tried an idea with Reward Model，someone who is instrested in can disccuss in 

[notebook](https://www.kaggle.com/code/huangshibao/internlm2-reward/notebook)





* --- discussion numver 155, the number of votes :0 ---

# Llama loading error! HELP!

**박민욱peterminpark** *Sat Jul 27 2024 14:33:00 GMT+0900 (日本標準時)* (0 votes)



When i try to load 

[https://www.kaggle.com/models/metaresearch/llama-3/Transformers/8b-chat-hf/1](https://www.kaggle.com/models/metaresearch/llama-3/Transformers/8b-chat-hf/1)

with llamaforsequenceclassification i get the above error.



---

 # Comments from other users

> ## Valentin Werner
> 
> Make sure you apply for access to the model first. Access is usually granted within 10minutes to 24hours.
> 
> 
> 


---



* --- discussion numver 156, the number of votes :0 ---

# how to fine-tune again?

**Mukatai** *Tue Jul 16 2024 01:09:47 GMT+0900 (日本標準時)* (0 votes)

In the public notebook, there is information about fine-tuning the Gemma2 model. Do you know how to fine-tune a model that has already been fine-tuned again?

`@dataclass

class Config:

    gemma_dir = '/kaggle/input/gemma-2/transformers/gemma-2-9b-it-4bit/1/gemma-2-9b-it-4bit'

    lora_dir = '/kaggle/input/73zap2gx/checkpoint-5600'

    max_length = 2048

    batch_size = 4

    device = torch.device("cuda")    

    tta = False  # test time augmentation. --

    spread_max_length = False  # whether to apply max_length//3 on each input or max_length on the concatenated input

cfg = Config()`

I am trying to load a pre-trained model with lora_dir = '/kaggle/input/73zap2gx/checkpoint-5600', but the final results suggest that it has only trained on the additional data.



---

 # Comments from other users

> ## Darshan Patel
> 
> [@mukatai](https://www.kaggle.com/mukatai) You load the pre-trained model Gemma-2-9b-it-4bit and apply the LoRA adapter from /kaggle/input/73zap2gx/checkpoint-5600. This combined model becomes your new base model, which you then fine-tune using your own dataset and hyperparameters.
> 
> 
> 


---



* --- discussion numver 157, the number of votes :0 ---

# Any ways to see submission runtime?

**gmin5y** *Thu Jul 25 2024 03:34:25 GMT+0900 (日本標準時)* (0 votes)

Hi, I am new to Kaggle and I am wondering if we can have access to the outputs of the notebooks we submitted for scoring (probably not?) If we couldn't access the submission logs, then how can we know how long our notebooks run? I have seen people discussing about the runtime of the notebook and I would really appreciate someone can explain how you measure the runtime of your solution on test set.

Thank you all! Best of luck for everyone in the coming 2 weeks!



---

 # Comments from other users

> ## Valentin Werner
> 
> You can hover over the "3h ago" to get an exact timestamp of submission. You cannot see exactly how long it runs, so you have to check in regularly, which is quite annoying.
> 
> Submission logs do not exist, as you could just print all the testdata etc.
> 
> 
> 
> > ## gmin5yTopic Author
> > 
> > 
> > You can hover over the "3h ago" to get an exact timestamp of submission. You cannot see exactly how long it runs, so you have to check in regularly, which is quite annoying.
> > 
> > Submission logs do not exist, as you could just print all the testdata etc.
> > 
> > Thank you so much!
> > 
> > 
> > 
> > ## RB
> > 
> > I have used  [this](https://www.kaggle.com/c/riiid-test-answer-prediction/discussion/201047) , its easy and works , you don't have to keep checking forever to measure runtime.
> > 
> > [This](https://www.kaggle.com/code/cpmpml/submission-timing) is another option.
> > 
> > 
> > 


---



* --- discussion numver 158, the number of votes :0 ---

# Do I still need to continue training?

**KeShuang Liu** *Fri Jul 26 2024 14:05:04 GMT+0900 (日本標準時)* (0 votes)

I have fine tuned many models, but the losses have remained almost unchanged. Is it necessary for me to continue training because I haven't trained enough? I find it difficult to make a decision at this point.This is my current validation set loss curve, which I verify every 2000 steps



---

 # Comments from other users

> ## S J Moudry
> 
> Are you testing on a validation set? I'd be more worried about performance there.  I'd also check my warmup steps and set them around 5-20%, having too few can cause a big drop right away but then you never really improve.
> 
> 
> 


---



* --- discussion numver 159, the number of votes :0 ---

# How to choose a suitable model

**KeShuang Liu** *Wed Jul 24 2024 13:48:06 GMT+0900 (日本標準時)* (0 votes)

When I was fine-tuning, log_dass started oscillating around 1. Do I need to choose a point with the lowest loss to submit, or do I submit the final result



---

 # Comments from other users

> ## Valentin Werner
> 
> This looks like a training loss, right? Your validation loss should be more stable. 
> 
> Selecting a model should never be done based on training loss, as training loss does not represent the way the model can predict on unseen data. From my experience, it is either best to train with CV to find best parameters and then do a full train for a fixed length, that worked best for all the CV models OR you train a single model, use a validation set and submit that single model.
> 
> You would then select the model / parameter which minimizes the validation loss. Note, that you can still overfit on validation loss, as you might take a specific point of the epoch which has the lowest validation loss. Small differences in validation loss do not necessarily reflect capability of the model on new data. So, it is fine to you the leaderboard submissions as "test set", which basically validates your validation loss. If your model has a lower validation loss and leaderboard score (which is loss in this case), this is a promising model.
> 
> Hope this helps you out!
> 
> 
> 
> > ## KeShuang LiuTopic Author
> > 
> > Thank you very much. I just checked and confirmed that this is indeed a training loss rather than a validation set loss. I will use the validation set loss to select the model and also try to use the training method you mentioned. Thank you for your reply
> > 
> > 
> > 


---

> ## Casmir Sunny
> 
> I will suggest that you submit the model corresponding to the checkpoint with the lowest validation loss rather than the final model. This approach ensures you are submitting the most generalizable and best-performing version of your model.
> 
> 
> 
> > ## Valentin Werner
> > 
> > This does not have to be the case. You can definetly overfit on validation data by blindly following this approach, particularly when only using a smaller subset of data as validation data. It also makes sense to compare validation loss with training loss, and decide from there. 
> > 
> > 
> > 


---

> ## Yi-Fu Chen
> 
> About Trainer
> 
> My understanding is that "Training Loss" is the last loss calculated during training, and there is no average, while "Validation Loss" is the average loss of the entire Validation dataset.
> 
> So "Validation Loss" may be smoother and "Training Loss" may be jumpier.
> 
> 
> 


---



* --- discussion numver 160, the number of votes :0 ---

# Does post-processing apply to this competition?

**Nicole** *Wed Jul 24 2024 08:12:23 GMT+0900 (日本標準時)* (0 votes)

I tried to use some post-processing to deal with my prediction, but the effect was not good. Did you have any improvement in post-processing?



---

 # Comments from other users

> ## Valentin Werner
> 
> I tried some post processing early in the competition, which did also not work well for me. I think the intuition is that the model is basically already caibrating itself, meaning if it says "0.4" as highest probability, it will be right around 40% of the time. And 80% will be right around 80% of the time. 
> 
> If you now say 0.4 is not really confident, and that should be 0.33 , you will increase the loss in ~6 out of 10 cases (because the loss is lower if your predict 40% and it actually the right prediction).
> 
> I prepared this little code snippet to demonstrate this: 
> 
> ```
> from sklearn.metrics import log_loss
> 
> y_true = [[1,0,0]] * 4 + [[0,1,0]] * 3 + [[0,0,1]] * 3
> y_pred = [[0.4, 0.3, 0.3]] * 10
> print("raw log_loss:", log_loss(y_true, y_pred))
> # raw log_loss: 1.0888999753452235
> 
> y_true = [[1,0,0]] * 4 + [[0,1,0]] * 3 + [[0,0,1]] * 3
> y_pred = [[0.334, 0.333, 0.333]] * 10
> print("post processed (overconfident) log_loss):", log_loss(y_true, y_pred))
> # post processed (overconfident) log_loss): 1.0984133878031905
> 
> ```
> 
> Further, overconvidence is a killer. If you set a 0.8 (probably right in 80% of cases), to a 0.9, you will have a much higher loss in those 20% of cases, where you are now overconfident. You are penalized way higher for high-confidence wrong classifications.
> 
> I prepared this little code snippet to demonstrate this: 
> 
> ```
> from sklearn.metrics import log_loss
> 
> y_true = [[1,0,0]] * 2 + [[0,1,0]] * 8
> y_pred = [[0.1, 0.8, 0.05]] * 10
> print("raw log_loss:", log_loss(y_true, y_pred))
> # raw log_loss: 0.5877385652626266
> 
> y_true = [[1,0,0]] * 2 + [[0,1,0]] * 8
> y_pred = [[0.075, 0.90, 0.025]] * 10
> print("post processed (overconfident) log_loss):", log_loss(y_true, y_pred))
> # post processed (overconfident) log_loss): 0.6023418456154264
> 
> ```
> 
> I might be missing something in my intuition, but assuming your model is well calibrated, doing correction will more likely harm than fix anything.
> 
> 
> 
> > ## NicoleTopic Author
> > 
> > Totally agree with you
> > 
> > 
> > 


---

> ## Lorry Zou
> 
> I tried log-loss clipping, got same results.
> 
> 
> 


---



* --- discussion numver 161, the number of votes :0 ---

# [need help]How to use DDP to speedup sft ?

**bao** *Wed Jul 24 2024 18:42:20 GMT+0900 (日本標準時)* (0 votes)

hello，kagglers,

I use [codes ](https://www.kaggle.com/code/shelterw/training-llama3-8b-4-bit-qlora-sft/notebook) and change args like below:

```
 args = TrainingArguments(
        output_dir='/gemini/output',
        overwrite_output_dir = True,
        evaluation_strategy = "epoch",
        save_strategy = "steps",
        save_steps=200,
        save_total_limit=2,
        logging_strategy="steps",
        logging_steps=20,
        warmup_steps=20,
        optim="adamw_8bit",
        learning_rate=2e-4,
        per_device_train_batch_size=8,
        per_device_eval_batch_size=8,
        gradient_accumulation_steps=16,
        num_train_epochs=1,
        fp16=True,
        metric_for_best_model="log_loss",
        greater_is_better = False,
        report_to="none",
        accelerator="ddp"  
    )

    trainer = Trainer(
        args=args,
        model=model,
        train_dataset=ds.select(train_idx),
        eval_dataset=ds.select(eval_idx),
        data_collator=DataCollatorForSeq2Seq(tokenizer=tokenizer),
        compute_metrics=compute_metrics,
    )
    trainer.train()

```

but GPU0 utility can reach 97%+， GPU1 only got 20%- even 0%。  the total training is slower than one GPU，how to fix it ?



---

 # Comments from other users

> ## CPMP
> 
> In order to use ddp you have to spawn two processes. Here are some example from HF documentation: [https://huggingface.co/docs/transformers/v4.43.0/en/perf_train_gpu_many#scalability-strategy](https://huggingface.co/docs/transformers/v4.43.0/en/perf_train_gpu_many#scalability-strategy)
> 
> 
> 
> > ## baoTopic Author
> > 
> > Thanks, I will try it.
> > 
> > 
> > 
> > > ## CPMP
> > > 
> > > You can try the accelerate library as well. I never used it myself, but it looks simpler to use than writing your own DDP code.
> > > 
> > > 
> > > 


---

> ## Pranshu Bahadur
> 
> Hf trainer already uses ddp try not setting any accelerator
> 
> And device_map = 'auto' when loading the model
> 
> Is your model unsloth?
> 
> Because they mention that 1xT4 is 5x faster at the end
> 
> [https://huggingface.co/unsloth/llama-3-8b-bnb-4bit](https://huggingface.co/unsloth/llama-3-8b-bnb-4bit)
> 
> [Screenshot_2024-07-24-17-08-15-27_40deb401b9ffe8e1df2f1cc5ba480b12.jpg](https://storage.googleapis.com/kaggle-forum-message-attachments/2934339/20965/Screenshot_2024-07-24-17-08-15-27_40deb401b9ffe8e1df2f1cc5ba480b12.jpg)
> 
> > ## baoTopic Author
> > 
> > I remove the accelerator setting, and set device_map = 'auto' when loading the model. But got the same 
> > 
> > 
> > 
> > > ## Pranshu Bahadur
> > > 
> > > Yeah its because of unsloth quantized models training faster on 1xt4
> > > 
> > > Have you tried just using a P100?
> > > 
> > > Also can you share screenshot of memory usage while training?
> > > 
> > > 
> > > 
> > > ## baoTopic Author
> > > 
> > > I use 2x3090. the screenshot was in my last reply message.
> > > 
> > > 
> > > 
> > > ## Pranshu Bahadur
> > > 
> > > Oh then you can use way higher batch size that's why only 1 is being used right now
> > > 
> > > 
> > > 


---



* --- discussion numver 162, the number of votes :0 ---

# A question about submission

**Owen** *Fri Jul 19 2024 09:52:13 GMT+0900 (日本標準時)* (0 votes)

Will sample_submission.csv be replaced during submission like test.csv files



---

 # Comments from other users

> ## CPMP
> 
> Yes. sample submission when you submit has the same number of rows as test.
> 
> 
> 


---

> ## Enter your display name
> 
> The answer should be no.
> 
> 
> 


---

> ## Yichuan Gao
> 
> It will be replaced with the same row count and ids with input data. Almost all notebooks are using it as a template for output predictions 
> 
> 
> 


---



* --- discussion numver 163, the number of votes :0 ---

# The language

**Dlond Mike** *Sun Jul 21 2024 22:03:48 GMT+0900 (日本標準時)* (0 votes)

train.csv are all english but how about the Public Datasets and private?



---

 # Comments from other users

> ## Valentin Werner
> 
> train.csv is not all english. The data definetly involves a few multi-lingual samples. It is save to assume there could be some samples in the test data too
> 
> 
> 


---



* --- discussion numver 164, the number of votes :0 ---

# [Question] Confused with random classification layer weight(score.weight) for LlamaForSequenceClassification

**Xuhang_CN** *Sat Jul 20 2024 19:07:52 GMT+0900 (日本標準時)* (0 votes)

Hi , I am a freshman for llm. I want to SFT llama3 in my GPU.

When I check for the same train environment, I find classification layer weight is initialized randomly(maybe?):

When I run below code first time and second time, I get different score.weight.

model_raw = LlamaForSequenceClassification.from_pretrained(
    model_name,
    quantization_config=quantization_config,
    num_labels=3,
    device_map='auto'
model = prepare_model_for_kbit_training(model)
config = PeftConfig.from_pretrained(finetune_model_name)
model = PeftModel.from_pretrained(model, finetune_model_name,is_trainable=False)
)

Even if I load saved adapter weight, weight is still not the same.

So I want to know how to make sure I train llama3 in my GPU and upload adapter in kaggle to make sure I get the same model.

Thanks!



---

 # Comments from other users

> ## Valentin Werner
> 
> You could set the seed for the run. That way you always get the same initial values. Make sure versions are similar / identical between kaggle notebook and local. There are plenty of "seed all" functions on kaggle and google that you can use
> 
> 
> 


---

> ## hn
> 
> You may need to do a custom save LoRA as some combinations may render the LoRA saving the wrong weights.
> 
> 
> 


---



* --- discussion numver 165, the number of votes :0 ---

# Will we no longer be able to use GPUs and TPUs in competitions?

**Hıdır Demir** *Sat Jul 20 2024 05:11:45 GMT+0900 (日本標準時)* (0 votes)

Will we no longer be able to use GPUs and TPUs in competitions?ns?  



---

 # Comments from other users

> ## Lorry Zou
> 
> L UI change 
> 
> 
> 


---

> ## Nicholas Broad
> 
> Check the Settings > Accelerator from the top menu bar
> 
> 
> 


---

> ## Akeryu Ryuu
> 
> I don't know if they are experimenting with new UI but you can find the accelerator option in session options on the right side where you turn off internet for the notebook. 
> 
> 
> 


---



* --- discussion numver 166, the number of votes :0 ---

# special token Efficiency

**박민욱peterminpark** *Fri Jul 19 2024 07:18:04 GMT+0900 (日本標準時)* (0 votes)

many organized their dataset into  +  +  input text form. I tried adding , ,  as special tokens and trained a model but the result was not good does anyone know why this is the case.



---

 # Comments from other users

> ## cm391
> 
> have you resized the embedding to take into account that you have added new tokens?
> 
> Gemma contains some spare special tokens in its tokenizer - you could just repurpose those!
> 
> 
> 
> > ## 박민욱peterminparkTopic Author
> > 
> > thx
> > 
> > I did resize my model.
> > 
> > recycling unused special token is a good idea. I'll try that out
> > 
> > 
> > 


---



* --- discussion numver 167, the number of votes :0 ---

# Question about submission

**Stanislav9801** *Thu Jul 18 2024 05:44:16 GMT+0900 (日本標準時)* (0 votes)

When creating submission, do my notebook should take as input test.csv file and produce output.csv file?

I mean, when I submit notebook, does test data will be loaded there dynamically, and through notebook inference submission.csv file should be produced? And this test.csv will not be the same as test.csv in the data provided?

So in this case my notebook should behave as a function, which takes test.csv as input, and submission.csv as output? Am I right?

This is my first time submission, so I don't understand this process a bit.

Thanks.



---

 # Comments from other users

> ## Cristóbal Mackenzie
> 
> Yes, you are right. On submission, the test.csv file will contain all test data, not just the three samples you see when editing a notebook.
> 
> 
> 
> > ## Stanislav9801Topic Author
> > 
> > Thank you!
> > 
> > 
> > 


---



* --- discussion numver 168, the number of votes :0 ---

# Usage of unsloth

**Varun Jagannath** *Mon Jul 08 2024 01:16:33 GMT+0900 (日本標準時)* (0 votes)

Has anyone used unsloth in the competition as it says that training and inferencing is much with it. Looking forward for suggestions.



---

 # Comments from other users

> ## Ivan Vybornov
> 
> They do not have kernels for classifier yet.
> 
> 
> 
> > ## Cristóbal Mackenzie
> > 
> > Exactly, and I think the "axolotl" library which is also being very widely used doesn't support classification models yet.
> > 
> > 
> > 
> > ## Varun JagannathTopic Author
> > 
> > ok, thanks for the input. But do you think it would be too much of a task if we give prompts and then ask model to predict the classes.
> > 
> > 
> > 
> > ## Takamichi Toda
> > 
> > In the CausalLM header can use the probabilities of generation of tokens A, B and tie as predictions.
> > 
> > ```
> > inputs = tokenizer(text)
> > out = model(inputs)
> > pred_token_id = tokenizer.encode("A") + tokenizer.encode("B") + tokenizer.encode("tie")
> > pred = out.logits[0, -1, pred_token_id].softmax(0)
> > 
> > ```
> > 
> > 
> > 
> > > ## Varun JagannathTopic Author
> > > 
> > > Tried this method as well, but it always predicts or weighs towards one class. Even I have checked your notebook. Model A is always having higher weight. I guess the classification head is working well in this competition.
> > > 
> > > 
> > > 
> > > ## Takamichi Toda
> > > 
> > > In my experiment as well, the classification head has been producing better results so far. I am currently in the process of trial and error to see if improvements can be made with fine-tuning (in [this discussion](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/520470#2925128), it seems they were able to achieve 0.902 with the generation head).
> > > 
> > > 
> > > 


---



* --- discussion numver 169, the number of votes :0 ---

# Error when submit

**Nguyễn Anh Tú** *Mon Jul 15 2024 16:23:48 GMT+0900 (日本標準時)* (0 votes)

I got the error "Submission Scoring Error" when I submitted  my notebook, I thought that I set the wrong format for my submission.csv. Then, I read the sample_submission.csv and change the the value of ['winner_model_a', 'winner_model_b', 'winner_tie'] columns with my y_predict. The worst thing is my notebook ran successful but when I submitted again I got the error "Notebook Threw Exception", please help me!



---

 # Comments from other users

> ## Valentin Werner
> 
> ### Submission scoring error -> make sure that you include id
> 
> An example way to get a working submission:
> 
> ```
> # Submit
> sub = pd.DataFrame(sm, index = test.id, columns = ["winner_model_a","winner_model_b","winner_tie"]).reset_index()
> sub.to_csv('submission.csv', index=False)
> sub.head()
> 
> ```
> 
> where sm is an array like np.array([0.123,0.567,0.234],…,[0.999,0.000,0.001])
> 
> ### Notebook threw exception
> 
> You managed to make a working notebook not work anymore 😀 This could have some reasons: GPU goes OOM (this does not trigger an OOM Error); There are some "null" responses in the responses which need to be handled (e.g., replace null with 'null' before loading the string representation of the list as real list); There is actually an error raised during runtime.
> 
> What you can do to evaluate the errors is try to run your inference code on the half the train set (which is basically the size of test) and see what happens.
> 
> 
> 
> > ## Nguyễn Anh TúTopic Author
> > 
> > It's very helpful for me. Thanks a lot.
> > 
> > 
> > 


---



* --- discussion numver 170, the number of votes :0 ---

# Training not proceeding for Llama 3

**JamshaidSohail** *Sun Jul 14 2024 20:29:44 GMT+0900 (日本標準時)* (0 votes)

Hi. I am trying to train the Llama 2 model from the [notebook](https://www.kaggle.com/code/kishanvavdara/lmsys-llama-3-tpu-train/notebook) shared by [@kishanvavdara](https://www.kaggle.com/kishanvavdara). But my training is not proceeding as shown in the figure. Any help would be appreciated.  



---

 # Comments from other users

> ## Valentin Werner
> 
> If you have the tqdm per epoch, I recommend changing it to the inner loop (steps within the epoch) to see if it actually does something:
> 
> ```
> for epoch in range(CFG.NUM_EPOCHS):
>     ste = time()
>     for step in tqdm(range(STEPS_PER_EPOCH)):
>         # Zero Out Gradients
>         OPTIMIZER.zero_grad()
> 
> ```
> 
> Also, the first samples sometimes take multiple minutes (I once had 300 seconds for the first batch) but then it will speed up afterwards. The notebook shared works well technically, so if you havent changed anything, I would just recommend factory reset and try again.
> 
> 
> 
> > ## JamshaidSohailTopic Author
> > 
> > The only changes I need to do is the addition of HF_TOKEN for my own account in the tokenizer as well as in the model loading area as below. 
> > 
> > ```
> > model_id = "meta-llama/Meta-Llama-3-8B-Instruct"
> > tokenizer = AutoTokenizer.from_pretrained(model_id,use_auth_token=HF_TOKEN)
> > 
> > base_model = LlamaForSequenceClassification.from_pretrained(model_id,
> >                                                             use_auth_token=HF_TOKEN,
> >                                                             torch_dtype=torch.bfloat16,
> >                                                             num_labels=3)    
> > 
> > ```
> > 
> > Now i followed your advice and added the tqdm to the STEPS_PER_EPOCH line as well and watching the training goes inside. 
> > 
> > 
> > 
> > > ## JamshaidSohailTopic Author
> > > 
> > > It is working now. Thank you for your comment and help 😀
> > > 
> > > 
> > > 


---



* --- discussion numver 171, the number of votes :0 ---

# How to solve no kernel

**KeShuang Liu** *Thu Jun 20 2024 12:36:40 GMT+0900 (日本標準時)* (0 votes)

RuntimeError: cutlassF: no kernel found to launch!



---

 # Comments from other users

> ## YingxiZhang
> 
> what kernel？Any more errors?
> 
> 
> 


---



* --- discussion numver 172, the number of votes :0 ---

# Should we train our model just for English or for multiple languages ? 

**AlphaTT30** *Sun Jul 14 2024 21:51:33 GMT+0900 (日本標準時)* (0 votes)

Can the test data contain multiple languages or just English? 



---

 # Comments from other users

> ## Valentin Werner
> 
> The training data does include non-english samples. Even languages with non-latin alphabet (e.g., asian languages and russian). However, the amount of samples seem to be quite low. Keep in mind that many models are able to "speak" multile languages inherently, so if you are using LLMs like Llama or Gemma, you are probably wasting time on this filter.
> 
> 
> 


---



* --- discussion numver 173, the number of votes :0 ---

# Can we use external data that contain other model's responses excluding  those in  the competition data? 

**AlphaTT30** *Sun Jul 14 2024 18:39:39 GMT+0900 (日本標準時)* (0 votes)

Is there any restriction to use the other model's responses that are not in the competition data? Or can we use any model's responses?



---

 # Comments from other users

> ## Valentin Werner
> 
> Just need to make sure data is available open source. Good luck!
> 
> 
> 
> > ## AlphaTT30Topic Author
> > 
> > I have another question, can the test data set contain multiple languages or just English? 
> > 
> > 
> > 


---



* --- discussion numver 174, the number of votes :0 ---

# how to save qlora_trained model weight with pytorch

**YEI0907** *Sat Jul 13 2024 14:23:51 GMT+0900 (日本標準時)* (0 votes)

because of some problems,I can`t use qlora to train my model  with transformers.Trainer,so,I trained my qlora model with my own pytorch training script and save my weights with torch.save directly,but when i use my weights to inference,i found that when i run my notebook ,my predictions is different in each turns .so,i think my model saving method might be wrong,so, how can i save my trained weights after qlora training with pytorch training script? can i use torch.save directly? or is there any other problems during my inference?Thanks very much for answering my question



---

 # Comments from other users

> ## Valentin Werner
> 
> If you load the model with the peft library, you simply also use model.save_pretrained. This will only save the adapter and not the full model. So we are talking < 100 MB instead of multiple GB.
> 
> Code snippet as example:
> 
> ```
> if test_loss < best_val and epoch != 0:
>     model.save_pretrained(
>         f"my_newest_model_{epoch+1}_{step}"
>     )
> 
> ```
> 
> You will later load it by first loading the model itself (e.g., LlamaForSequenceClassification), getting the PEFT model and then loading the QLoRA weights
> 
> ```
> # Get peft
> model_0 = get_peft_model(base_model_0, peft_config).to(device_0) 
> # Load weights
> model_0.load_state_dict(torch.load(CFG.LORA_PATH), strict=False)
> model_0.eval()
> 
> ```
> 
> 
> 
> > ## YEI0907Topic Author
> > 
> > thanks!,I use torch.save directly to save my model,code just like this
> > 
> > ```
> > if score < best_score:
> >             best_score = score
> >             if int(os.environ["RANK"]) == 0:
> >                 torch.save({
> >                     'epoch': epoch,
> >                     'model_state_dict': dict([(k, v) for k, v in model.module.named_parameters() if v.requires_grad]),
> >                     'optimizer_state_dict': optimizer.state_dict(),
> >                     'scheduler_state_dict': scheduler.state_dict()
> >                 }, model_path)
> > 
> > ```
> > 
> > and my model loading method is same as yours,
> > 
> > so you mean I should use peft_model.save_pretrained() insteat of torch.save?
> > 
> > addtionaly,i test my weights in kaggle by using train_data and my loss is 1.8xxxx,but in my traing, the eval_sets loss is 0.9XX and train_sets loss is also 0.9xx
> > 
> > by the way,i learned a lot from your notebooks, thank you for sharing your notebook!
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > Happy to be of help :)
> > > 
> > > I highly recommend saving adapters separately and loading them separately. I do not see any value in saving full models as long as you are not adding any layers to the model. If you create a custom model with additional layers, you will need to save these weights to, in that case it might make sense to save full models.
> > > 
> > > However, if you load Llama3 like this:
> > > 
> > > ```
> > > base_model = LlamaForSequenceClassification.from_pretrained(model_id, token=HF_TOKEN, num_labels=CFG.NUM_LABELS, torch_dtype=CFG.TORCH_DTYPE, trust_remote_code=True)   
> > > 
> > > ```
> > > 
> > > The sequence classification head is always initialized in the same way, just random values. Things that can help achieve the same result is setting the seed, so the weights are randomly initialized exactly as they were initialized during training.
> > > 
> > > ```
> > > def set_seeds(seed):
> > >     """Set seeds for reproducibility """
> > >     os.environ['PYTHONHASHSEED'] = str(seed)
> > >     random.seed(seed)
> > >     np.random.seed(seed)
> > >     torch.manual_seed(seed)
> > >     if torch.cuda.is_available():
> > >         torch.cuda.manual_seed(seed)
> > >         torch.cuda.manual_seed_all(seed)
> > >     # Set seed for all TPU cores
> > >     xm.set_rng_state(seed, device=xm.xla_device())  
> > > 
> > > ```
> > > 
> > > Doing this helped me to achieve a better LB <-> CV relationship.
> > > 
> > > Further, you may want to save the tokenizer or replicate and deterministic changes you did to it during training (e.g., if you changed pad_token_id or such). Make sure you are exactly tokenizing the same way (also input formats etc.) as you did during training. This can easily switch a lot for your score too.
> > > 
> > > 
> > > 
> > > ## YEI0907Topic Author
> > > 
> > > thanks,this provide a new idea for me to ensure consistency between train and test ;for my model , i had added some my custom modules,and i will re-train the model and save the weight with two part,one for llama3 with peft.save_pretrained(),one for my custom module with torch.save directly.T_T，the previous weight resulted in my LB score reaching 3.x
> > > 
> > > 
> > > 
> > > ## Ilya Turaev
> > > 
> > > All my life I've been thinking that classification heads for decoders were pretrained on some benchmarks or other data. Glad that I've busted this myth and misunderstanding now…
> > > 
> > > 
> > > 


---



* --- discussion numver 175, the number of votes :0 ---

# Which hardware configuration is used in scoring?

**Michael Benton** *Sat Jul 13 2024 10:56:59 GMT+0900 (日本標準時)* (0 votes)

I'm at a point where I'm making optimizations to get within 9hours. I just launched one that should work in time if on a p100, but won't if on one of the TPM or 2x T4. Does it automatically give you the same hardware configuration as you have set in the notebook? 



---

 # Comments from other users

> ## Valentin Werner
> 
> Yep, you get what you choose during runtime.
> 
> 
> 


---



* --- discussion numver 176, the number of votes :0 ---

# Notebook throwing Exception

**Varun Jagannath** *Wed Jul 10 2024 23:45:51 GMT+0900 (日本標準時)* (0 votes)

After submitting the notebook. And, after some grueling hours it throws exception and there is no way to find out about it. Is there any other way to check.



---

 # Comments from other users

> ## Valentin Werner
> 
> This is just one potential issue, but how are you handling the "null" that sometimes occur? Doing this helped for me in the early submissions: response.replace("null","'null'") <-- note the extra ' to make it a string before loading the string representation of the list an actual list (e.g., with ast.literal_eval(response))
> 
> I really hope this is doing it for you - because these exceptions can be nasty. If not, maybe try debugging by predicting on training data again.
> 
> If the GPU goes OOM its not an OOM error on kaggle but an Exception, so maybe reduce batch size or max length too. Best of luck!
> 
> 
> 
> > ## Varun JagannathTopic Author
> > 
> > Looks like its an issue with batch size
> > 
> > 
> > 


---

> ## Robert Turro
> 
> Try clicking on the notebook then going to the Logs section.
> 
> 
> 


---



* --- discussion numver 177, the number of votes :0 ---

# Using template for instruct model?

**Weiren** *Thu Jul 11 2024 15:42:49 GMT+0900 (日本標準時)* (0 votes)

I heard that using instruct model would perform slightly better. But when I was using Llama-8b and Llama-8b-instruct without template,  they got the same LB score.

Does the template matters? I had tried using template but the score was even worse. Also, I found that using a template causes the logloss stuck…

Some details:

1 epoch

4 batch size * 2 accumulation_steps

and just trying different lora params 🤡

Any thoughts or insights on this?



---

 # Comments from other users

> ## hn
> 
> Actually anecdotally I use the Llama3 template as well for instruct and I think it’s worse off than no template for some reason. 
> 
> 
> 


---



* --- discussion numver 178, the number of votes :0 ---

# What is 8b-chat-hf in kaggle's llama3 models? 

**Dylan Liu** *Thu Jul 11 2024 18:38:03 GMT+0900 (日本標準時)* (0 votes)

If I'm right, Llama 3 has a normal version and an instruct version. 

In [https://www.kaggle.com/models/metaresearch/llama-3/Transformers/8b-chat-hf/1](https://www.kaggle.com/models/metaresearch/llama-3/Transformers/8b-chat-hf/1), I see 8b-chat-hf, what's that? And where is the instruct version?



---

 # Comments from other users

> ## Weiren
> 
> I think the 8b-chat-hf one is fine-tuned for dialogue use cases and in huggingface format. 
> 
> The instruct model I think you can download from hugging face then upload to kaggle.
> 
> 
> 
> > ## Cristóbal Mackenzie
> > 
> > I actually think the 8b-chat-hf is the same as the instruct model in huggingface.
> > 
> > 
> > 
> > > ## Weiren
> > > 
> > > Yea, should be the same. thanks~
> > > 
> > > 
> > > 


---



* --- discussion numver 179, the number of votes :0 ---

# How to avoid wights and bias logging, when I try train the model, it was asking wights and bias token id

**suri@7** *Wed Jul 10 2024 18:24:36 GMT+0900 (日本標準時)* (0 votes)

when I try train the model, it was asking wights and bias token id. I don't want to wights and bias to my model.

```
training_args = TrainingArguments(
  output_dir="./kaggle/input/lmsys-chatbot-arena/bert_model",
  learning_rate=2e-5,
  per_device_train_batch_size=3,
  per_device_eval_batch_size=3,
  num_train_epochs=2,
  weight_decay=0.01,
  evaluation_strategy="epoch",
  save_strategy="epoch",
  load_best_model_at_end=True,
)
trainer = Trainer(
  model=model,
  args=training_args,
  train_dataset=train_dataset,
  eval_dataset=test_dataset,
  tokenizer=tokenizer,
  data_collator=data_collator,
  #compute_metrics=compute_metrics,
)
trainer.train()

```



---

 # Comments from other users

> ## waechter
> 
> Set report_to='none' in TrainingArguments if you don't want to use remote logging
> 
> report_to (str or List[str], optional, defaults to "all") — The list of integrations to report the results and logs to. Supported platforms are "azure_ml", "clearml", "codecarbon", "comet_ml", "dagshub", "dvclive", "flyte", "mlflow", "neptune", "tensorboard", and "wandb". Use "all" to report to all integrations installed, "none" for no integrations. 
> 
>   From [https://huggingface.co/docs/transformers/en/main_classes/trainer](https://huggingface.co/docs/transformers/en/main_classes/trainer)
> 
> 
> 
> > ## suri@7Topic Author
> > 
> > Thanks for your help [@waechter](https://www.kaggle.com/waechter) ,, I would like to know after training my model how, can I can submit the prediction offline, When saving the model Kaggle input path, It does not load when submitted to p predictions.
> > 
> > 
> > 
> > > ## waechter
> > > 
> > > output_dir="./kaggle/input/lmsys-chatbot-arena/bert_model",
> > > 
> > > I think this is wrong because you trying to write to the kaggle/input directory (which is read only)
> > > 
> > > You should save the pretrained model to kaggle/working dir : output_dir="kaggle/working/bert_model"
> > > 
> > > 
> > > 
> > > ## suri@7Topic Author
> > > 
> > > ok, Thanks
> > > 
> > > 
> > > 


---



* --- discussion numver 180, the number of votes :0 ---

# Using XGBoost and Graident Boosting Techniques

**Royy** *Mon Jul 08 2024 17:59:56 GMT+0900 (日本標準時)* (0 votes)

Here, the provided code defines several functions to compute various text analysis metrics to understand the quality of the prompt and responses. The functions are defined to calculate word count, character count, sentence count, average word length, average sentence length, type-token ratio, word frequency, bigram frequency, and readability scores using the nltk and textstat libraries. 

The readability scores function calculates several readability indices, including the Flesch-Kincaid score, Gunning Fog index, SMOG index, and Automated Readability Index (ARI).

After defining these functions, the code applies them to the "prompt", "response_a", and "response_b" columns of the DataFrame. For each of these columns, it calculates the word count, character count, sentence count, average word length, and average sentence length by applying the respective functions and creates new columns in the DataFrame to store these metrics. 

Here, in the notebook  I have just tried a few of these metrics to achieve a log loss of 1.05.

Ways you can enhance this code to decrease it's log loss:

Add more hyperparameters.
Try out the other metrics (which are commented on in the code).
Also, add more variables like the Jaccard index and cosine similarity between response a, b, and prompt.
Increase the number of iterations for each model per fold.

These can easily improve the model output and decrease the log loss on the test dataset.

Also, upload the textstat library as the internet is turned off for this competition.

Notebook URL: [https://www.kaggle.com/code/nehalroy/using-xgboost-and-gb-using-nltk](https://www.kaggle.com/code/nehalroy/using-xgboost-and-gb-using-nltk)



---

 # Comments from other users

> ## Valentin Werner
> 
> Hey [@nehalroy](https://www.kaggle.com/nehalroy) - please beware that Pyphen is not released as open source / commercially available package and is therefore one of the few packages that is not allowed in this competition. 
> 
> 
> 
> > ## RoyyTopic Author
> > 
> > Thank you [@valentinwerner](https://www.kaggle.com/valentinwerner) for the heads up. Highly appreciated.
> > 
> > Although, I just shared this as a technique that can be used to design a Gradient Boosting model for this certain problem.
> > 
> > 
> > 


---



* --- discussion numver 181, the number of votes :0 ---

# How to finetune LLM? 

**bao** *Tue Jun 25 2024 18:26:28 GMT+0900 (日本標準時)* (0 votes)

I am a beginner in LLM and would like to get started. Could you please explain how to fine-tune the model for this scenario? Is it done using methods like DPO with LLama-Factory?



---

 # Comments from other users

> ## Staru09
> 
> You can check this [https://dassum.medium.com/fine-tune-large-language-model-llm-on-a-custom-dataset-with-qlora-fb60abdeba07](https://dassum.medium.com/fine-tune-large-language-model-llm-on-a-custom-dataset-with-qlora-fb60abdeba07)
> 
> 
> 
> > ## Nikhil Narayan
> > 
> > Well do you have resources about any other way to do this
> > 
> > 
> > 
> > > ## Staru09
> > > 
> > > Resources as in computation or something else. If computation is an issue then you can try using tools like llamaedge or wasmedge. They are very good frameworks to work with but you should know Rust otherwise you can use PEFT, or converting into lower bit like 8 or 16 to fine-tune along with LORA, QLORA etc.
> > > 
> > > 
> > > 


---

> ## Lorry Zou
> 
> There are plenty of great videos on YouTube teaching you how to fine-tune LLM and Llama 3 specifically.
> 
> 
> 
> > ## YingxiZhang
> > 
> > Indeed, there are a lot of resources on YouTube and I've learned a lot.😀
> > 
> > 
> > 


---



* --- discussion numver 182, the number of votes :0 ---

# config.json file missing in Llama model

**AlphaTT30** *Thu Jul 04 2024 16:18:38 GMT+0900 (日本標準時)* (0 votes)

I copied other notebooks where the config.json file exists. But when I add the model as input in my notebooks the config.json file is missing so the model does not load. 

Why is that and what to do? 



---

 # Comments from other users

> ## Artyom Lyan
> 
> You should use transformers version, not pytorch
> 
> 
> 


---

> ## Saiyan Warrior
> 
> HI [@alphatt30](https://www.kaggle.com/alphatt30) there might be 2 reasons that I can think of:
> 
> You might need to get the llama permission [here](https://www.kaggle.com/models/metaresearch/llama-3)
> You might have given the wrong path.
> 
> can you share the exact error?
> 
> 
> 
> > ## AlphaTT30Topic Author
> > 
> > I have permission and the path was correct, I even tried other's notebooks where they used the same model. so I removed their model and then loaded the same model in input and config.json was still missing there 
> > 
> > 
> > 


---



* --- discussion numver 183, the number of votes :0 ---

# Clarification on the number of chats that need to be processed

**Gabriel Mirea** *Thu Jul 04 2024 21:04:10 GMT+0900 (日本標準時)* (0 votes)

Hi,

The dataset description says 

When your submission is scored, this example test data will be replaced with the full test set. There are 55K rows in the training data, and you can expect roughly 25,000 rows in the test set.

and the leaderboard says

This leaderboard is calculated with approximately 26% of the test data. The final results will be based on the other 74%,

So should we expect that the final submission on the private leaderboard will need to process ~75.000 rows?



---

 # Comments from other users

> ## RB
> 
> 
> So should we expect that the final submission on the private leaderboard will need to process ~75.000 rows?
> 
> No, total 25000 samples 
> 
> Public LB - 26% => 6500 Samples
> 
> Private LB - 74% => 18500 Samples
> 
> Total Test Set = 25000
> 
> When you make a submission, your code is doing inference for all 25000 samples, we only see public LB with 6500 samples, remaining after competition ends
> 
> 
> 
> > ## Gabriel MireaTopic Author
> > 
> > Thanks! That makes sense, so if the submission scores on the LB it got through all the samples. And the final score is hidden so that people don't probe, I guess?
> > 
> > My main concern was if the notebook will have to deal with more samples later. That's clear now, thank you again.
> > 
> > 
> > 


---



* --- discussion numver 184, the number of votes :0 ---

# More than 1 response (response_a / response_b)

**Samar Jaffri** *Tue Jul 02 2024 04:01:26 GMT+0900 (日本標準時)* (0 votes)

Some of the rows in the test/train dataset have 2 or more response(s). Do anyone know if we need to make prediction based on all of the responses i.e., user will chose of of response_a or one of response_b.

Or if there is anything specified about that, that I am missing..?



---

 # Comments from other users

> ## waechter
> 
> The data come from [https://chat.lmsys.org/](https://chat.lmsys.org/) , you can try it to help you understand
> 
> 📜 Rules: You can continue chatting until you identify a winner.
> 
> There are the same number of responses as there are prompts, users vote for their favorite conversation
> 
> 
> 
> > ## Valentin Werner
> > 
> > Exactly this. We are not classifying responses, but conversations. However, if you think that the last response is the one that triggers the user to press "a is better", you are probably right in most cases.
> > 
> > 
> > 
> > > ## Yichuan Gao
> > > 
> > > Haven't thought about this! Wonder how much will only using the last response affects the prediction😂
> > > 
> > > 
> > > 


---



* --- discussion numver 185, the number of votes :0 ---

# test data does not have LLM name , while the train data had (columns : 'model_a' and 'model_b'). 

**Kumar Shivansh** *Tue Jul 02 2024 08:11:13 GMT+0900 (日本標準時)* (0 votes)

test data does not have llm name , while the train data had (columns : 'model_a' and 'model_b'). 



---

 # Comments from other users

> ## Enter your display name
> 
> This is precisely to prevent people from making predictions based on the model's name.
> 
> 
> 


---

> ## Anya
> 
> I think even the train data doesnt have to have the LLM name cols, cuz they dont matter the predictions. Our task is to predict the battle results' probability between two responses.
> 
> 
> 


---



* --- discussion numver 186, the number of votes :0 ---

# What is the calculation of the loss & log_loss?

**Anya** *Sun Jun 30 2024 16:14:27 GMT+0900 (日本標準時)* (0 votes)

I happened to meet a situation that loss & log_loss was NaN. 

I know in programming it would happen when 0 is taken as the dividend or something like that. 

Now I need to know the calculation of the loss & log_loss so I could find out the cause.

I appreciate every answer.🙏



---

 # Comments from other users

> ## Valentin Werner
> 
> Kaggle uses the sklearn implementation, which is quite well documented: [https://scikit-learn.org/stable/modules/generated/sklearn.metrics.log_loss.html](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.log_loss.html)
> 
> The log loss does not use any division, but it uses the logarithm. This technically could produce nan values if your predictions are < 0, but this is not happening in the sklearn logloss.
> 
> Anyways, I think you should always softmax your predictions before calculating the log loss.
> 
> Hope this helps!
> 
> 
> 
> > ## AnyaTopic Author
> > 
> > Thanks a lot. I switched to another GPU with larger memory, and the error got solved.
> > 
> > Maybe the data overflow cause a value out of logarithm's definition domain.
> > 
> > 
> > 


---



* --- discussion numver 187, the number of votes :0 ---

# How to get the vector representation of sentences using Llama3?

**godmysalary** *Fri Jun 28 2024 17:22:14 GMT+0900 (日本標準時)* (0 votes)

Hi everyone! Now most public noteboks directly use "LlamaForSequenceClassification" for fine-tuning and getting the predicted probability. I was wondering how I can get the learned embeddings of response_a and response_b besides the predictions since I think the embeddings can be fed into other different classifiers. I don't want to employ another LLM due to the time constraint. So could anybody tell me how I can getting the embeddings of responses as a byproduct of the fine-tuned Llama3? Thanks.



---

 # Comments from other users

> ## RB
> 
> You can pass output_hidden_states=True when initializing model , something like this 
> 
> ```
> model  = AutoModelForCausalLM.from_pretrained(model_path, quantization_config=quantization_config, output_hidden_states=True)
> 
> out = model(input_ids = tokenized['input_ids'], attention_mask = tokenized['attention_mask'])
> 
> out.hidden_states
> 
> ```
> 
> 
> 
> > ## godmysalaryTopic Author
> > 
> > thank you!
> > 
> > 
> > 


---

> ## Enter your display name
> 
> I think what you want is the last hidden state of the model's output?
> 
> 
> 
> > ## godmysalaryTopic Author
> > 
> > exactly. So is there one way to obtain this? thanks
> > 
> > 
> > 


---



* --- discussion numver 188, the number of votes :0 ---

# how many is the perfect score?

**Anya** *Sat Jun 22 2024 17:17:35 GMT+0900 (日本標準時)* (0 votes)

Im new to kaggle.

Till now, Ive seen scores range in 0.5 to 1.7

I wonder how many is the perfect score so I can evaluate my score level.

Is it 5, 10 or 100?



---

 # Comments from other users

> ## Valentin Werner
> 
> The metric "log_loss" allows for a score of 0.0 (e.g., exactly perfect predictions every time). An "educated guess" score (predicting the distribution of the train set) gets you a score of about 1.097.
> 
> The problem is that human preferences, which we are trying to predict, are not clearly predictable. This is because if we both write a prompt, we may prefer different responses - so how is our model supposed to learn which responses are better. Because the problem is this hard to predict, the "ceiling" of the score is much higher than 0.0 - more along the lines of 0.75 or 0.8 (just a gut feeling)
> 
> 
> 
> > ## AnyaTopic Author
> > 
> > I got it😃. Thanks  for such a detailed reply.
> > 
> > 
> > 


---

> ## AnyaTopic Author
> 
> After reading the leaderboard I find that the lower one scores, the higher he ranks?
> 
> 
> 
> > ## Yichuan Gao
> > 
> > Yes it is, since the score is calculated as log loss, the lower the loss, the better your guesses are
> > 
> > 
> > 


---



* --- discussion numver 189, the number of votes :0 ---

# How to run a model on two cards

**KeShuang Liu** *Mon Jun 17 2024 17:22:30 GMT+0900 (日本標準時)* (0 votes)

I loaded my model on the CPU and it took up 19g, while the GPU p100 only had 16g. However, I found that if I use two t4 blocks for a total of 30g, can I deploy my model to two t4 blocks? What should I do?



---

 # Comments from other users

> ## Minato Ryan
> 
> If you are using transformers library, use device_map="auto".
> 
> like this,
> 
> ```
> AutoModelForCausalLM.from_pretrained("google-bert/bert-base-cased", device_map="auto")
> 
> ```
> 
> 
> 
> > ## KeShuang LiuTopic Author
> > 
> > Thank you very much for your reply. I succeeded using your method
> > 
> > 
> > 


---



* --- discussion numver 190, the number of votes :0 ---

# General Question 

**Satish0308** *Sat Jun 15 2024 16:23:59 GMT+0900 (日本標準時)* (0 votes)

How many times i can submit my file ?

5 submissions per day holds good in all competition ? including this one



---

 # Comments from other users

> ## Valentin Werner
> 
> Not sure if I understand correctly, but:
> 
> - you got 5 submissions per day for the rest of the competition
> 
> - you got 5 submissions per day in EACH competition you partake (so if you do 2 competitions, you could do 10 submissions, but maximum of 5 per competition)
> 
> - you do NOT have extra submissions if you only use 3 submissions on one day
> 
> - you can submit your submission.csv as many times as you want, with the maximum of 5 times a day
> 
> - you can submit the same submission.csv file 5 times a day, for the rest of the competition if you want
> 
> - you can select your best submissions in the submission tab, else the best scoring ones will be selected for you
> 
> - I have not yet seen a competition with more or less than 5 submissions per day
> 
> 
> 


---



* --- discussion numver 191, the number of votes :0 ---

# What does the #id mean and why they are non-sequential

**Eva Wang** *Wed Jun 12 2024 05:23:16 GMT+0900 (日本標準時)* (0 votes)

We noticed that the #id column was not one-by-one and we wonder why. Is it because the datapoints not shown in the train.csv are cut out because they are not in English?



---

 # Comments from other users

> ## Ahmad Al-Husainy
> 
> Besides what has been suggested, you can think of the ID as sessionID,  a way to link all parts of the text if you decide to split them into separate segments; if look closer at the prompt (and also response_a and response_b), you'll see it includes several parts or segments of a discussion. If you split these into different rows, you can use the ID to piece them back together later.
> 
> 
> 


---

> ## Valentin Werner
> 
> as per usual ID means identifier - they only have to be unique, like an index - not meaningful for training. It is quite likely that LMSYS only provided a subset of their data (I mean, else we would have a lot more) and they just kept their original IDs
> 
> 
> 


---

> ## tanaka
> 
> Id is not sequential data, because its range is from 30,192 to 4,294,947,231, but the chat bot arena has only over 1,241,035 data. Id itself is not so much meaningful data.
> 
> 
> 


---



* --- discussion numver 192, the number of votes :0 ---

# Notebook issue

**Shahik15** *Sun Jun 09 2024 04:35:45 GMT+0900 (日本標準時)* (0 votes)

Hello, 

           I have developed a notebook but it's not added to the code section? Can somebody help here?

Greetings



---

 # Comments from other users

> ## Valentin Werner
> 
> Have you made sure that it is public in the settings section?
> 
> 
> 
> > ## Shahik15Topic Author
> > 
> > yes here's the notebook link [https://www.kaggle.com/code/shahik15/gemma-rag-chatbot-arena](https://www.kaggle.com/code/shahik15/gemma-rag-chatbot-arena)
> > 
> > 
> > 


---



* --- discussion numver 193, the number of votes :0 ---

# Questions/Thoughts for building the baseline model for my first submission

**Dr. Gopalashivabalasubramanium Chandrashekaran** *Sat Jun 08 2024 10:10:08 GMT+0900 (日本標準時)* (0 votes)

I see that there is no model name in the test data.

I've listed my thoughts below. Would love to hear your input. 

So, basically, we have to analyze the response (a/b) of the unknown model and decide which one wins. 
The user prompt has to be filtered for anything that would cause the model to give a null response or a default reply
The model response, we have to categorize it somehow with the model name. Which means there would be features to look for in a model response to attach it to a named model.
Lastly, once the models are identified, we can refer to some type of weight for each model based on its win percentage versus whatever other model it is facing and decide whether it wins or loses or ties.
Slap all this into a submission file and win.


---

 # Comments from other users

> ## Valentin Werner
> 
> Step 1: Load data
> 
> Step 2: ?
> 
> Step 3: Slap all into a submission file and win 😉
> 
> 
> 


---



* --- discussion numver 194, the number of votes :0 ---

# Exciting and Creative

**kartikey bartwal** *Fri May 31 2024 03:49:17 GMT+0900 (日本標準時)* (0 votes)

This concept is quite exciting and beneficial for a data scientist. Choosing the appropriate statements can save or earn you millions of dollars worth of resources and customer scale. 

All the best everyone 😊



---

 # Comments from other users

> ## Valentin Werner
> 
> I think what becomes somewhat clear by current scores, is that it is really hard to cater individual preferences. But maybe providers that give the choice of models can extract key characteristics and serve the model without names, as personalities instead. 
> 
> Best of luck to you too!
> 
> 
> 
> > ## gmin5y
> > 
> > That's good idea haha Personalized LLM sounds interesting. However, will that turn LLM into the next ins/tiktok which only feeds what you want to see
> > 
> > 
> > 


---



* --- discussion numver 195, the number of votes :0 ---

# I encountered the following problem while training the model, how should I solve it

**KeShuang Liu** *Wed May 29 2024 14:06:23 GMT+0900 (日本標準時)* (0 votes)

wandb: Logging into wandb.ai. (Learn how to deploy a W&B server locally: [https://wandb.me/wandb-server](https://wandb.me/wandb-server))

wandb: You can find your API key in your browser here: [https://wandb.ai/authorize](https://wandb.ai/authorize)

wandb: Paste an API key from your profile and hit enter, or press ctrl+c to quit:



---

 # Comments from other users

> ## tanaka
> 
> try this
> 
> [https://www.kaggle.com/code/ayuraj/experiment-tracking-with-weights-and-biases?scriptVersionId=63334832&cellId=3](https://www.kaggle.com/code/ayuraj/experiment-tracking-with-weights-and-biases?scriptVersionId=63334832&cellId=3)
> 
> 
> 
> > ## KeShuang LiuTopic Author
> > 
> > Thank you for your reply. I will try it now
> > 
> > 
> > 


---



* --- discussion numver 196, the number of votes :0 ---

# how to submit my predictions

**Rikesh Prajapati** *Thu May 23 2024 12:11:21 GMT+0900 (日本標準時)* (0 votes)

can anyone tell me how to submit my predictions?



---

 # Comments from other users

> ## Valentin Werner
> 
> This is a simple step-by-step guide:
> 
> 1) Create your notebook, do your modelling and predictions. Get the predictions in the right format, you want a csv file called "submission.csv" with the columns "id", "winner_model_a", "winner_model_b", "winner_tie". If you are using pandas, you want to save the csv file WITHOUT index, such as sub.to_csv('submission.csv', index=False).
> 
> 2) The notebook needs to have Internet Access disabled
> 
> 3) Actually submit your notebook by clicking on "Submit" in the sidebar.
> 
> Note that there are also other ways to submit your predictions, which do not require you to go into the editor of a notebook.
> 
> Option 2) After making sure step 1 & 2 of the above guide are still fulfilled, you can click on the "Submit Prediction" top right of this page (or any other page of the competition). There you can select a notebook and a notebook version you want to submit. There you can also specify the output file, but you can only submit files called "submission.csv". If you DID NOT save your predictions as csv, you cannot submit them.
> 
> Option 3) You can go to the notebook you want to submit and click on "Output". There you will also find a submit button, which leads you to the same selection as Option 2.
> 
> 
> 


---



* --- discussion numver 197, the number of votes :0 ---

# How are we gonna predict probability with no data?

**alekh** *Sun May 12 2024 14:13:23 GMT+0900 (日本標準時)* (0 votes)

How are we gonna predict the probability when we have no training data with probabilities that makes sense. The training data is comprised of 1-hot vectors assigning 100% probability to one of the outcomes. That must clearly be wrong. I don't understand what the training set represents. Does it represent the preference of one particular human? Of a random human? If so, are there multiple rows with the same prompt and responses for different people?



---

 # Comments from other users

> ## alekhTopic Author
> 
> Guess I found the answer:
> 
> "The competition dataset consists of user interactions from the ChatBot Arena. In each user interaction a judge provides one or more prompts to two different large language models, and then indicates which of the models gave the more satisfactory response."
> 
> So i guess we have to like do a softmax on the logits to get probabilities.
> 
> 
> 


---



* --- discussion numver 198, the number of votes :-1 ---

# How to address the issue of performance loss when transferring trained model weights across different environments and devices?

**YEI0907** *Thu Jul 18 2024 20:05:31 GMT+0900 (日本標準時)* (-1 votes)

Hi guys,

When I move my model weights to Kaggle after finishing training on my GPU server, I found a problem: the performance of my model significantly drops even though the data is the same as on my GPU server. How can I handle this problem? By the way, the only difference between Kaggle and my GPU server is the versions of Torch and CUDA：

| kaggle | my gpu server |
| --- | --- |
| cuda 12.1 torch 2.1.2 | cuda11.8 torch 2.3.X |
| thanks for answering my question! |  |


---

 # Comments from other users

> ## Priyanshu Joshi
> 
> Different versions of Torch and CUDA can indeed lead to performance issues or even different behaviors in model execution. It's essential to ensure that the versions you're using are compatible and consistent. If possible, try to match the versions of Torch and CUDA on your GPU server with those on Kaggle. [Check here](https://pytorch.org/get-started/locally/) to see the see additional information.
> 
> Sometimes, subtle differences in the environment (e.g., different library versions) can also affect performance. You can export the environment configuration from your GPU server and replicate it on Kaggle using:
> 
> ```
> pip freeze > requirements.txt
> 
> ```
> 
> Then install the same requirements on Kaggle:
> 
> ```
> !pip install -r requirements.txt
> 
> ```
> 
> 
> 
> > ## YEI0907Topic Author
> > 
> > ok,thank you!
> > 
> > 
> > 


---

> ## CPMP
> 
> How do you know the performance drops?
> 
> 
> 
> > ## YEI0907Topic Author
> > 
> > I test my model by runing it on train data and compare the loss between kaggle and my server
> > 
> > 
> > 
> > > ## CPMP
> > > 
> > > testing on train data is not good practice unless you mean cross validation. Are you using cross validation?
> > > 
> > > 
> > > 


---



* --- discussion numver 199, the number of votes :-1 ---

# Why are there suddenly so many new accounts with very similar scores?

**Robert0921** *Fri Jul 12 2024 11:58:20 GMT+0900 (日本標準時)* (-1 votes)

Looking at PB, nearly 100 new accounts suddenly appeared in the past day, and their scores were all 0.941. Is there any problem?



---

 # Comments from other users

> ## Valentin Werner
> 
> Dropping silver solutions for free!
> 
> 
> 
> > ## Cody_Null
> > 
> > Thankfully I think it will be outside of the medal range at competition end but always wild to see a medal winning notebook in the last month of every competition haha
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > I think the most wild thing is just the copy & submit. I understand it If you joined early and never did another submission. However, what will happen next is 5 Notebooks that Ensemble these to get .940, .939, … without any novel ideas
> > > 
> > > This is not the kaggle way in my opinion.
> > > 
> > > I think it is great that this approach was shared because I read a lot of people are struggling with GPU resources to get something to work, the notebook that was shared just "works a little too well"
> > > 
> > > 
> > > 


---

> ## Xinyuan Qiao
> 
> there is a new notebook provide Gemma 2 inference code with 0.941 on PB, my original score was 0.942😂
> 
> 
> 
> > ## yechenzhi1
> > 
> > try to ensemble it😂
> > 
> > 
> > 
> > > ## Lorry Zou
> > > 
> > > I tried to ensemble it with my 0.957 Llama3 inference, and I got 0.959😅😅
> > > 
> > > 
> > > 
> > > ## Allen Wang
> > > 
> > > [@lorryzouzelun](https://www.kaggle.com/lorryzouzelun) Is the integration of gemma and llama3 effective? I tried it and the lb dropped a lot
> > > 
> > > 
> > > 
> > ## Robert0921Topic Author
> > 
> > 
> > there is a new notebook provide Gemma 2 inference code with 0.941 on PB, my original score was 0.942😂
> > 
> > Under the same conditions, which one is better？Gemma 2 and Llama3
> > 
> > 
> > 
> > > ## Xinyuan Qiao
> > > 
> > > Not sure, the gemma notebook provider use A6000 for training and I don't know his hyper-parameters. I will use same parameters to train both and reply you later.
> > > 
> > > 
> > > 


---



* --- discussion numver 200, the number of votes :-1 ---

# Trying to understand the strength of the models with the highest ties

**Dr. Gopalashivabalasubramanium Chandrashekaran** *Sat Jun 08 2024 09:37:46 GMT+0900 (日本標準時)* (-1 votes)

Good evening everyone,

I had a go at this data and made myself a list of the models with the highest tie rate. It made sense that the non-winner models will be the ones tie-ing. It was interesting to see the models that were subpar tie-ing with each other. 

My question here is: How do I assess the strength of the model based on the count of its ties? It is easy to judge it based on its number of wins. 

Anyone have any findings on this?

Also, if you have time, see my notebook. Would appreciate any feedback.



---

 # Comments from other users

> ## tanaka
> 
> lmsys's elo rating is calculated something like following.
> 
> It means, when ties, higher rank player's score may decrease slightly, while lower-ranked player's score may increase slightly.
> 
> ```
> def compute_online_elo(battles, K=4, SCALE=400, BASE=10, INIT_RATING=1000):
>     rating = defaultdict(lambda: INIT_RATING)
> 
>     for rd, model_a, model_b, winner in battles[['model_a', 'model_b', 'winner']].itertuples():
>         ra = rating[model_a]
>         rb = rating[model_b]
>         ea = 1 / (1 + BASE ** ((rb - ra) / SCALE))
>         eb = 1 / (1 + BASE ** ((ra - rb) / SCALE))
>         if winner == "model_a":
>             sa = 1
>         elif winner == "model_b":
>             sa = 0
>         elif winner == "tie" or winner == "tie (bothbad)":
>             sa = 0.5
>         else:
>             raise Exception(f"unexpected vote {winner}")
>         rating[model_a] += K * (sa - ea)
>         rating[model_b] += K * (1 - sa - eb)
> 
>     # calibrate llama-13b to 800
>     delta = (800-rating["llama-13b"])
>     for model in battles["model_a"].unique():
>         rating[model] += delta
> 
>     return rating
> 
> ```
> 
> Refs
> 
> - [https://colab.research.google.com/drive/1KdwokPjirkTmpO_P1WByFNFiqxWQquwH#scrollTo=hytEb0aXfcwm](https://colab.research.google.com/drive/1KdwokPjirkTmpO_P1WByFNFiqxWQquwH#scrollTo=hytEb0aXfcwm)
> 
> 
> 


---

> ## Valentin Werner
> 
> 
> It was interesting to see the models that were subpar tie-ing with each other.
> 
> It is important to acknowledge that the prompt matters a lot. When presenting prompting in my company, I show a tool a bit like the lmsys arena to raise understanding for when you need the "big guns". On a simple questions, llama2-7B can easily tie gpt4-turbo, such as "what is 2+2?" - you will not need that many parameters to answer this. Now, one model may say "4" and the other one says "Adding 2+2 results in 4." and you may prefer one of the answers. Oops, suddenly Llama2-7B "outperformed" GPT-4?
> 
> Further, we always expect models of the same category to tie more often - not sure if I fully understood your point.
> 
> How do I assess the strength of the model based on the count of its ties? It is easy to judge it based on its number of wins.
> 
> This is what LMSYS is doing on the website. For this competition, we are also predicting ties - so knowing that a model ties a lot should be as good as winning a lot.
> 
> 
> 


---



* --- discussion numver 201, the number of votes :-4 ---

# Is this competition leaked? Very interesting, there is a huge gap between the first and second place.

**Turbo** *Sun Aug 04 2024 12:56:23 GMT+0900 (日本標準時)* (-5 votes)





---

 # Comments from other users

> ## SeshuRaju 🧘‍♂️
> 
> [@zhoumichael](https://www.kaggle.com/zhoumichael) its all happen in last 24 hours, we need to wait until competition finish.
> 
> 
> 


---



* --- discussion numver 202, the number of votes :-6 ---

# What do you think qwen2:0.5b is doing here?

**Matthew Hendricks** *Thu Jul 11 2024 13:54:14 GMT+0900 (日本標準時)* (-6 votes)

```
import ollama
from datasets import load_dataset

dataset = load_dataset("lmsys/lmsys-arena-human-preference-55k", split='train')
print(dataset[0])
print("---")

"""
Dataset({
    features: ['id', 'model_a', 'model_b', 'prompt', 'response_a', 'response_b', 'winner_model_a', 'winner_model_b', 'winner_tie'],
    num_rows: 57477
})
"""

response = ollama.chat(model='qwen2:0.5b', messages=[
  {
    'role': 'user',
    'content': f'{dataset[0]}',
  },
])
print(response['message']['content'])

```

Look carefully at this and tell me what you think qwen2:0.5b is doing

## prompt='content': f'Dataset[0]'

```
{'id': 30192, 'model_a': 'gpt-4-1106-preview', 'model_b': 'gpt-4-0613', 'prompt': '["Is it morally right to try to have a certain percentage of females on managerial positions?","OK, does pineapple belong on a pizza? Relax and give me fun answer."]', 'response_a': '["The question of whether it is morally right to aim for a certain percentage of females in managerial positions is a complex ethical issue that involves considerations of fairness, equality, diversity, and discrimination.\\n\\nHere are some arguments in favor of and against such policies:\\n\\n**Arguments in favor:**\\n\\n1. **Correcting Historical Inequities:** Women have historically been underrepresented in leadership roles due to various cultural, institutional, and social barriers. Aiming for a specific percentage can be seen as a corrective measure to address past and ongoing discrimination.\\n\\n2. **Promoting Diversity:** Diverse leadership teams can enhance decision-making and represent a broader range of perspectives. This can lead to better outcomes for organizations and society as a whole.\\n\\n3. **Equality of Opportunity:** Setting targets for female representation in management can help ensure that women have equal opportunities to advance in their careers.\\n\\n4. **Role Modeling:** Increased visibility of female leaders can inspire and encourage other women and girls to pursue leadership roles.\\n\\n**Arguments against:**\\n\\n1. **Reverse Discrimination:** Setting a quota for female representation might lead to the perception or reality of reverse discrimination, where men might be overlooked for positions despite being qualified, simply to meet the gender target.\\n\\n2. **Meritocracy Concerns:** Critics argue that employment and promotion should be based solely on merit and qualifications, not gender. They fear that quotas could compromise the quality of leadership if less qualified individuals are promoted to meet gender targets.\\n\\n3. **Tokenism:** There is a risk that women appointed to meet quotas might be seen as \\"tokens,\\" undermining their legitimacy and potentially leading to resentment among colleagues.\\n\\n4. **Oversimplification of Diversity:** Focusing only on gender might overlook other important aspects of diversity, such as race, ethnicity, socioeconomic background, or sexual orientation.\\n\\nUltimately, the morality of aiming for a certain percentage of females in managerial positions depends on one\'s ethical framework and the context in which such policies are implemented. Proponents of gender diversity targets often argue that these measures are necessary as a transitional mechanism to create a level playing field, while opponents may argue for a \\"color-blind\\" or \\"gender-blind\\" approach to hiring and promotions.\\n\\nOrganizations and societies must carefully consider the implications of these strategies and strive to implement policies that promote fairness and equality while minimizing negative consequences. It is also important to address the root causes of gender inequality, such as unconscious bias, work-life balance challenges, and lack of supportive policies, to create an environment where everyone has the opportunity to succeed based on their capabilities and contributions.","Ah, the age-old culinary conundrum that has divided nations and dinner tables: does pineapple belong on a pizza? The tropical twist of pineapple on pizza, known as Hawaiian pizza, is a hotly debated topic where taste buds battle and pizza purists protest.\\n\\nLet\'s slice into the debate with a zest of fun:\\n\\n**Team Pineapple:** \\"Absolutely, yes! Pineapple on pizza is like a beach party in your mouth. The sweet juiciness of pineapple chunks frolicking with savory ham or bacon creates a flavor wave that surfs across the cheesy ocean of deliciousness. It\'s the Mardi Gras of pizzas, where sweet meets savory in a jubilant jamboree!\\"\\n\\n**Team No-Pineapple:** \\"No way, not in a million pizzas! Pineapple is a fruit that should be sunbathing on a tropical fruit platter, not freeloading on a sacred slice of pizza. The thought of warm, melty cheese conspiring with pineapple\'s sugary mischief is enough to make Italian ancestors turn in their tomato patches. Keep the pineapple in the fruit salad where it belongs!\\"\\n\\nAt the end of the day, whether pineapple belongs on pizza is a matter of personal taste. Some say it\'s a match made in heaven, others say it\'s a culinary crime. But let\'s face it, in the world of pizza toppings, where you can find everything from anchovies to zucchini, there\'s room for a little pineapple pizzazz. So, if your taste buds crave that sweet and tangy twist, go ahead and let your pineapple flag fly atop that glorious cheese-covered dough. Bon app\\u00e9tit, or as they say in pineapple paradise, \\"Aloha-ppetite!\\" \\ud83c\\udf4d\\ud83c\\udf55"]', 'response_b': '["As an AI, I don\'t have personal beliefs or opinions. However, I can tell you that the question of gender quotas in managerial positions is a complex one and positions can vary. Advocates argue that such measures can help correct historical imbalances, promote diversity, and may lead to better decision-making. Critics may argue that positions should be based purely on merit, and that quotas could potentially lead to tokenism or unqualified candidates being promoted. Morality can be subjective and differs from person to person based on their personal beliefs, cultural background, and values. It\'s a topic with valid arguments on both sides, and it\'s up to each individual or organization to decide what they believe is right.","As an AI, I don\'t eat, so I don\'t have personal preferences. But, in the world of pizza, the pineapple topping is a hotly debated topic! Some people love the sweet and savory mix it brings to a pizza, a flavor combination made famous by the Hawaiian pizza. Others firmly believe that the sweetness of the fruit has no place on a pizza. It\'s a pizza puzzle that might never be solved. So, whether pineapple belongs on a pizza or not, it truly depends on your taste buds!"]', 'winner_model_a': 1, 'winner_model_b': 0, 'winner_tie': 0}

```

## qwen2:0.5b response

```
{'id': 30240, 'model_a': 'gpt-4-1106-preview', 'model_b': 'gpt-4-0613', 'prompt': "What is the moral right for trying to have a certain percentage of females on managerial positions?", 'response_a': '["The question of whether it is morally right to aim for a certain percentage of females in managerial positions is a complex ethical issue that involves considerations of fairness, equality, diversity, and discrimination.\\n\\nHere are some arguments in favor of and against such policies:\\n\\n**Arguments in favor:**\\n\\n1. **Correcting Historical Inequities:** Women have historically been underrepresented in leadership roles due to various cultural, institutional, and social barriers. Aiming for a specific percentage can be seen as a corrective measure to address past and ongoing discrimination.\\n\\n2. **Promoting Diversity:** Diverse leadership teams can enhance decision-making and represent a broader range of perspectives. This can lead to better outcomes for organizations and society as a whole.\\n\\n3. **Equality of Opportunity:** Setting targets for female representation in management can help ensure that women have equal opportunities to advance in their careers.\\n\\n4. **Role Modeling:** Increased visibility of female leaders can inspire and encourage other women and girls to pursue leadership roles.\\n\\n**Arguments against:**\\n\\n1. **Reverse Discrimination:** Setting a quota for female representation might lead to the perception or reality of reverse discrimination, where men might be overlooked for positions despite being qualified, simply to meet the gender target.\\n\\n2. **Meritocracy Concerns:** Critics argue that employment and promotion should be based solely on merit and qualifications, not gender. They fear that quotas could compromise the quality of leadership if less qualified individuals are promoted to meet gender targets.\\n\\n3. **Tokenism:** There is a risk that women appointed to meet quotas might be seen as \\"tokens,\\" undermining their legitimacy and potentially leading to resentment among colleagues.\\n\\n4. **Oversimplification of Diversity:** Focusing only on gender might overlook other important aspects of diversity, such as race, ethnicity, socioeconomic background, or sexual orientation.\\n\\nUltimately, the morality of aiming for a certain percentage of females in managerial positions depends on one\'s ethical framework and the context in which such policies are implemented. Proponents of gender diversity targets often argue that these measures are necessary as a transitional mechanism to create a level playing field, while opponents may argue for a \\"color-blind\\" or \\"gender-blind\\" approach to hiring and promotions."},

```



---

 # Comments from other users

> ## Anya
> 
> haha, why are they the same?
> 
> 
> 
> > ## Matthew HendricksTopic Author
> > 
> > It surprised me that qwen2:0.5b seems to excel at mimicking the json format of the prompt it was provided.  It seems more likely to mimic the json format of the prompt if the prompt is 'longer'.
> > 
> > ```
> > import ollama
> > from datasets import load_dataset
> > from tqdm import tqdm
> > import json
> > from collections import Counter
> > 
> > def process_dataset(num_samples=1000):
> >     dataset = load_dataset("lmsys/lmsys-arena-human-preference-55k", split='train')
> >     results = []
> > 
> >     for i in tqdm(range(min(num_samples, len(dataset)))):
> >         sample = dataset[i]
> >         response = ollama.chat(model='qwen2:0.5b', messages=[
> >             {
> >                 'role': 'user',
> >                 'content': f'{sample}',
> >             },
> >         ])
> >         results.append({
> >             'input': sample,
> >             'output': response['message']['content']
> >         })
> > 
> >     return results
> > 
> > def analyze_results(results):
> >     truncation_count = sum(1 for r in results if len(r['output']) < len(str(r['input'])))
> >     json_preservation = sum(1 for r in results if r['output'].startswith('{') and r['output'].endswith('}'))
> > 
> >     field_preservation = Counter()
> >     for r in results:
> >         try:
> >             output_json = json.loads(r['output'])
> >             for key in r['input'].keys():
> >                 if key in output_json:
> >                     field_preservation[key] += 1
> >         except json.JSONDecodeError:
> >             pass
> > 
> >     return {
> >         'total_samples': len(results),
> >         'truncation_rate': truncation_count / len(results),
> >         'json_preservation_rate': json_preservation / len(results),
> >         'field_preservation': {k: v / len(results) for k, v in field_preservation.items()}
> >     }
> > 
> > if __name__ == "__main__":
> >     results = process_dataset(num_samples=10)  # Adjust the number of samples as needed
> >     analysis = analyze_results(results)
> > 
> >     with open("results.jsonl", "w") as f:
> >         for result in results:
> >             json.dump(result, f)
> >             f.write("\n")
> > 
> >     print(json.dumps(analysis, indent=2))
> > 
> > ```
> > 
> > 
> > 


---

> ## Valentin Werner
> 
> I don't know.. what is it doing?
> 
> 
> 
> > ## Matthew HendricksTopic Author
> > 
> > It's distilling and reflecting something.
> > 
> > In my opinion, it is rephrasing the question to be more direct, peeling back the layers of politically correct, amoral obfuscation.  It's decoding the core beliefs of the user based on how the question is phrased.
> > 
> > Dataset[0][ 'prompt']: "Is it morally right to try to have a certain percentage of females on managerial positions?"
> > 
> > ```
> > Qwen2:0.5b response: 
> > 'prompt': "What is the moral right for trying to have a certain percentage of females on managerial positions?",
> > 
> > ```
> > 
> > 
> > 


---



* --- discussion numver 203, the number of votes :-10 ---

# The hidden test dataset has distribution shift 

**Xin** *Sat Aug 03 2024 02:30:10 GMT+0900 (日本標準時)* (-11 votes)



After extracting some features from training dataset, then a full dataset one epoch train, I thought the single Gemma model can have a good leaderboard result, but the reality is eval:0.867 leaderboard: 0.933.

I think it might mean the data distribution is to some extent different than the train dataset, then after I extracting features from test dataset, the score then be low.



---

 # Comments from other users

> ## CPMP
> 
> What you see is that your model performs better on its training data than on new data. This is to be expected.
> 
> One way to not be surprised  is to split your triaining data into two piece. One piece you use for training, and one piece you use for evaluating your model once trained. The second piece is often called a validation dataset, or a test dataset.
> 
> 
> 


---

> ## Valentin Werner
> 
> You are facing a lot of backlash for a "beginner mistake" - even if only training for one epoch, you want to validate your model on unseen data, your model has theen the "validation" data already once, so it knows it. This is one form of data leakage.
> 
> Just from this training it is impossible to expect how well your model is going to perform on a leaderboard submission. Often, it is better to set aside 10-20% of data to make sure you have a local validation and a leaderboard score rather then fitting your model on all the data.
> 
> It is possible to probe the data distribution of the LB dataset, however, not with this approach. 
> 
> 
> 
> > ## XinTopic Author
> > 
> > Yeah. I understand. One epoch also probably brings model to an underfit status. From the result, I intuitively think that either the distribution between train and hidden test dataset different or there is a high similarity on train dataset (I mean tokenized data, maybe also because I only extract the first part from texts) which causes such an obvious overfit. 
> > 
> > 
> > 


---

> ## JM
> 
> Your eval_dataset is taking a subset of your training dataset…
> 
> 
> 
> > ## XinTopic Author
> > 
> > Yeah. But I think one epoch, the model only see the data once.
> > 
> > 
> > 
> > > ## David.Ricardo.H.X
> > > 
> > > You didnt get what he means…… 
> > > 
> > > Your eval_dataset is taking a subset of your training dataset… 
> > > 
> > > Do you have a concept of what is the difference between train set, validation set and test?
> > > 
> > > 
> > > 


---



