# Comments 

> ## Cody_Null
> 
> Great work Chris, I was just curious if you knew anything about performance loss with VLLM? I know nothing about it and was just trying to get an idea of what I should expect if I use this in other notebooks
> 
> 
> 
> > ## Chris DeotteTopic Author
> > 
> > I don't think there is any performance loss because of vLLM. The package vLLM just runs our models. It is other choices like vllm.SamplingParams, quantize or not, what type of quantization, max_model_length, tokenizer truncation that affects performance.
> > 
> > 
> > 
> > > ## Cody_Null
> > > 
> > > Great! I didn’t know if it was similar to ONNX or exactly what I needed haha
> > > 
> > > 
> > > 
> > > ## Chris DeotteTopic Author
> > > 
> > > We don't need to do any conversion of our models (like ONNX). We can take both non-quantized and quantized models directly from Hugging Face and run inference on them. (In other words, it doesn't change our models at all).
> > > 
> > > 
> > > 


---

> ## SeshuRaju 🧘‍♂️
> 
> [@cdeotte](https://www.kaggle.com/cdeotte) Thanks for sharing, 
> 
> is this model fine tuned with sft or dpo? 
> 
> how much gpu needed to fine tune? 
> 
> 
> 
> > ## Chris DeotteTopic Author
> > 
> > This model was finetuned with SFT. Depending on chosen LoRA rank parameter r, max_model_len, batch_size, and the amount of train data, we can finetune on any amount of GPUs.
> > 
> > During finetuning, we quantize 34B into 4bit reducing it's size to 20GB. So the only requirement is that the combined VRAM of your GPUs exceeds 20GB by enough to train with. We can probably finetune on Kaggle's 2xT4 with total VRAM 32GB if we reduce the above mentioned parameters.
> > 
> > 
> > 
> > > ## SeshuRaju 🧘‍♂️
> > > 
> > > 
> > > Thanks [@cdeotte](https://www.kaggle.com/cdeotte), due to limited Kaggle gpu hours, i am trying to train on 16GB VRAM. I'm exploring is any other methods to train with batch=1, r=3 and max_model_len=1024
> > > 
> > > chosen LoRA rank parameter r, max_model_len, batch_size, and the amount of train data, we can finetune on any amount of GPUs. - how we can fit 34B -> 4bit compressed -> 20GB ( further can be reduced in below 16GB ? ) [@cdeotte](https://www.kaggle.com/cdeotte) 
> > > 
> > > 
> > > 
> > > ## Chris DeotteTopic Author
> > > 
> > > I'm not sure how to finetune 34B LLM on 16GB VRAM. I think the minimum is closer to 32GB VRAM. There is a nice youtube video [here](https://www.youtube.com/watch?v=XpoKB3usmKc) explaining some details about efficient finetuning. During finetuning, we need memory for
> > > 
> > > - model weights
> > > 
> > > - gradients
> > > 
> > > - optimizer
> > > 
> > > To reduce memory the most, we load model in 4bit quantized (i.e. QLoRA to reduce model weights memory usage), we can use llm_int8_enable_fp32_cpu_offload to allow swapping model weights between GPU and CPU memory, we finetune with PEFT with small r parameter (i.e. QLoRA), we use gradient checkpointing (to reduce gradient memory usage), and we use paged_adam_8bit optimizer (with small batches and small max token length). This optimizer swaps saved variables from GPU to CPU as needed and uses 8bit to reduce the size of optimizer variables. 
> > > 
> > > 
> > > 
> > > ## SeshuRaju 🧘‍♂️
> > > 
> > > Thanks [@cdeotte](https://www.kaggle.com/cdeotte) - i use page_ada_8bit, QLoRA, PEFT. will try gradient checkpointing. I'm trying 
> > > 
> > > ```
> > > device_map = {
> > >     "encoder": "cuda:0", 
> > >     "decoder": "cpu",    
> > >     "lm_head": "cpu",    
> > > }
> > >  load_in_8bit_fp32_cpu_offload=True, 
> > > 
> > > ```
> > > 
> > > 
> > > 


---

> ## ano
> 
> Thanks for sharing this great model! If you can share, could you tell me what dataset did you use for training? Did you use the whole training dataset or part of it? Or any external dataset?
> 
> 
> 
> > ## Chris DeotteTopic Author
> > 
> > I finetuned this model with 80% of competition data. I used all data excluding every 5th row. So the correct validation would be to use the following data pd.read_csv("train.csv").iloc[0::5]. Currently this notebook uses pd.read_csv("train.csv").iloc[:128] but a more accurate quick validation would be 
> > 
> > ```
> > VALIDATE = 128
> > test = test.iloc[0:VALIDATE*5:5]
> > 
> > ```
> > 
> > Then we use 128 samples from the first index%5==0.
> > 
> > 
> > 


---

> ## JM
> 
> Are you actually seeing 5 hours on submit stage? Mine is going way over
> 
> 
> 
> > ## Chris DeotteTopic Author
> > 
> > No, I am not seeing 5 hours. Mine is taking between 8 and 9 hours. If I release another version of this notebook, I will fix the time estimate code in code cell #10 (which involves removing "inference errors"). And I will update the introduction paragraph to say "under 9 hours" and not "in 5 hours".
> > 
> > 
> > 
> > > ## ano
> > > 
> > > Any idea why the estimated inference time (5 hours) is so different from the actual one (8-9 hours)? I also experimented to infer about 1000 samples and got the similar estimated inference time for 25000 samples (5-6 hours). 
> > > 
> > > 
> > > 


---

> ## Luan Ngo Dinh
> 
> Hello, I would like to ask how the results of quantizing GPTQ compare to AWQ, and whether it is feasible on Kaggle compared to AWQ?
> 
> 
> 
> > ## Chris DeotteTopic Author
> > 
> > To use GPTQ we set quantization="gptq" in the vLLM parameters (and save our model as GPTQ beforehand). I have not tried it on Kaggle but I have used both AWQ and GPTQ successfully in the past on T4 GPUs. The accuracy of each was basically similar. And the inference times were similar too.
> > 
> > 
> > 
> > > ## Akhila datta dola
> > > 
> > > Thank you for sharing !
> > > 
> > > Just wanted to ask does vLLM support on the fly 4-bit quantization like in bitsandbytes. How do they compare in general with gptq and awq?
> > > 
> > > 
> > > 


---

> ## Luan Ngo Dinh
> 
> Thank you for your wonderful sharing!!! 
> 
> May I ask why there were 'There were 33 inference errors out of 128 inferences' in infenrence process ? 
> 
> 
> 
> > ## Chris DeotteTopic Author
> > 
> > For 33 out of 128 input text, the model did not predict any generation text. Therefore we have no tokens to extract probabilities from for those 33. Our try/except code block catches this and predicts [1/3, 1/3, 1/3] in these cases.
> > 
> > 
> > 
> > > ## Luan Ngo Dinh
> > > 
> > > Do you mean the model did not generate the tokens 'a', 'b', 'tie' even though it was fine-tuned?
> > > 
> > > 
> > > 
> > > ## Chris DeotteTopic Author
> > > 
> > > Yes. The problem is because we have truncated our model to max_model_len=1024 (for speed). Therefore when input text is larger than 1024 then vLLM truncate to 1024 and there is no more room to output any generated text. With smarter prompt engineering and/or truncation strategy we can avoid these inference errors.
> > > 
> > > 
> > > 
> > > ## floriandev
> > > 
> > > just working on the "prompt engineering and/or truncation strategy", good to know I might be on the right track ;-)
> > > 
> > > 
> > > 


---

> ## Xinian Guo
> 
> Hi, Is the model finetuning by competitins data ?
> 
> 
> 
> > ## Chris DeotteTopic Author
> > 
> > Yes. This model (notebook version 8) is finetuned with comp data. Notebook version 6 [here](https://www.kaggle.com/code/cdeotte/infer-34b-with-vllm?scriptVersionId=188642633) is zero shot without finetuning.
> > 
> > 
> > 
> > > ## yechenzhi1
> > > 
> > > Hi, may I ask what the LB score is for the fine-tuned version?
> > > 
> > > 
> > > 
> > > ## floriandev
> > > 
> > > I got 0.972 with that notebook. Good luck ;-)
> > > 
> > > 
> > > 


---

> ## Qihang Wang
> 
> Hello  Chris, .  I would like to confirm your process: 
> 
> CMIIW
> 
> qlora fine-tuning 4bit model ? 
> merge qlora to the model ?
> convert 4bit to ?
> AWQ quantize
> Using vLLM for inference
> 
> I'm not very familiar with the first three steps and I'm not sure if this is how you're doing it.
> 
> Could you explain them in a bit more detail?
> 
> 
> 


---

