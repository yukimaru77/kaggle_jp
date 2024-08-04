# Comments 

> ## Songling
> 
> Can't find this file, can someone help me?
> 
> WARNING: Location '../input/llm-pip-2024-7-4/' is ignored: it is either a non-existing path or lacks a specific scheme.
> 
> ERROR: Could not find a version that satisfies the requirement bitsandbytes (from versions: none)
> 
> ERROR: No matching distribution found for bitsandbytes
> 
> WARNING: Location '../input/llm-pip-2024-7-4/' is ignored: it is either a non-existing path or lacks a specific scheme.
> 
> WARNING: Location '../input/llm-pip-2024-7-4/' is ignored: it is either a non-existing path or lacks a specific scheme.
> 
> WARNING: Location '../input/llm-pip-2024-7-4/' is ignored: it is either a non-existing path or lacks a specific scheme.
> 
> ERROR: Could not find a version that satisfies the requirement peft (from versions: none)
> 
> ERROR: No matching distribution found for peft
> 
> 
> 


---

> ## Shimei
> 
> Hi,thank you for sharing this wonderful notebook!
> 
> but after fine tuning your training notebook, i get the following error when inference
> 
> OSError: /kaggle/input/llama3-sft/checkpoint-2800 does not appear to have a file named config.json. Checkout 'https://huggingface.co//kaggle/input/llama3-sft/checkpoint-2800/tree/None' for available files.
> 
> 
> 
> > ## Romanov_Alex
> > 
> > Same there, have you tried how to fix it?
> > 
> > 
> > 
> > > ## duncangao
> > > 
> > > sam here. I wonder how to fix it
> > > 
> > > 
> > > 


---

> ## Huang Jing Stark
> 
> Any specifig reason to set MAX_LENGTH = 2400?
> 
> 
> 
> > ## ShelterWTopic Author
> > 
> > Just to give the model more information.
> > 
> > 
> > 


---

> ## Rabbit
> 
> I would like to ask how your model loads from huggingface to kaggle?
> 
> 
> 
> > ## ShelterWTopic Author
> > 
> > Create a new notebook, open the Internet, download the model using snapshot download, and use this notebook as the new dataset
> > 
> > 
> > 
> > > ## Rabbit
> > > 
> > > Thank you
> > > 
> > > 
> > > 


---

> ## Dlond Mike
> 
> but you,my friend,you are truly hero.
> 
> 
> 


---

> ## PaulRRR
> 
> I use llama3.1 but I get the error:ValueError: rope_scaling must be a dictionary with with two fields, type and factor, got {'factor': 8.0, 'high_freq_factor': 4.0, 'low_freq_factor': 1.0, 'original_max_position_embeddings': 8192, 'rope_type': 'llama3'}
> 
> 
> 
> > ## zhudong1949
> > 
> > update transformers version
> > 
> > 
> > 


---

> ## Aaryan Gupta
> 
> Hey, are the datasets for this notebook private? Since the code is throwing error on paths not found.
> 
> 
> 


---

> ## 박민욱peterminpark
> 
> WAIT
> 
> Is the model /kaggle/input/sft-llama3-lora-9231 public?
> 
> Also i trained models from using the training code to get fold0-fold4 models and tested them but they are stuck in the 0.94 - 0.95 range
> 
> 
> 
> > ## PaulRRR
> > 
> > Hello, can you run this inference code？
> > 
> > 
> > 


---

> ## Lorry Zou
> 
> I downloaded the whole repository from Huggingface and made a dataset for inference, but I got this error when loading:
> 
> Error no file named pytorch_model.bin, model.safetensors, tf_model.h5, model.ckpt.index or flax_model.msgpack found in directory /kaggle/input/llama-3-8b-instruct-bnb-4bit-1.
> 
> Anyone encountered the same problem and know how to deal with it?
> 
> 
> 
> > ## Lorry Zou
> > 
> > Now I got another error:
> > 
> > Incorrect path_or_model_id: '/kaggle/input/llama-3-8b-instruct-bnb-4bit'. Please provide either the path to a local folder or the repo_id of a model on the Hub.
> > 
> > Can anyone help me please.
> > 
> > 
> > 


---

> ## OHIRA
> 
> Hi thanks for great work !!!
> 
> if you use 8bit LoRA, then can you do inference within the time limit ?
> 
> how much time ?
> 
> if you know please tell me.
> 
> 
> 
> > ## ShelterWTopic Author
> > 
> > as well as 4bits
> > 
> > 
> > 
> > > ## OHIRA
> > > 
> > > Thank you!
> > > 
> > > 
> > > 
> > > ## hn
> > > 
> > > hello, I tried to use gemma2-9b, but somehow always get exception if I use 8 bits and a total length of say [256+640+640] = [1536] and above. Have you experienced it before? I reduced to 4 bits and [256+512+512] and the inference ran. hmm
> > > 
> > > 
> > > 


---

> ## Qihang Wang
> 
> Hi , I would like to ask why you set 
> 
> label_token_id = [128250]
> 
> 
> 
> > ## ShelterWTopic Author
> > 
> > [128250] is llama3 special token, doesn't make any sense, just take the label position and avoid other normal tokens.
> > 
> > 
> > 


---

> ## Dlond Mike
> 
> Hi,can you give a simple conclusion about what's new in this new notebook?
> 
> 
> 


---

> ## YEI0907
> 
> How long did it take for your inferencing time? I also used an autoregressive architecture, but the inference time increased significantly
> 
> 
> 


---

> ## YEI0907
> 
> 老哥，你的这个架构推理时间花了多久呀？我也用了自回归模型进行推理，但是推理时间比直接分类长了很多
> 
> 
> 
> > ## ShelterWTopic Author
> > 
> > max_len=2400 -> 6h -> 0.935
> > 
> > max_len=1024 -> 3h -> 0.938
> > 
> > 
> > 


---

> ## Rabbit
> 
> I have tried your method, why do I cv0.927 but lb only 0.960
> 
> 
> 
> > ## ShelterWTopic Author
> > 
> > sad, could be overfitting？
> > 
> > 
> > 
> > ## PaulRRR
> > 
> > Hello, may I ask if you can run this inference code？
> > 
> > 
> > 
> > > ## Rabbit
> > > 
> > > I finetune the code
> > > 
> > > 
> > > 


---

> ## lllleeeo
> 
> That‘s a really great work！Have you compared the score with classifier head？
> 
> 
> 
> > ## ShelterWTopic Author
> > 
> > Of course, this method works better with almost the same parameters
> > 
> > 
> > 


---

> ## Octavio Grau
> 
> This notebook throws an error for me (0.935 version). Any hint guys? [@shelterw](https://www.kaggle.com/shelterw) thanks for publishing!
> 
> 
> 
> > ## ShelterWTopic Author
> > 
> > what error ?
> > 
> > 
> > 
> > > ## Songling
> > > 
> > > [@shelterw](https://www.kaggle.com/shelterw) 
> > > 
> > > WARNING: Location '../input/llm-pip-2024-7-4/' is ignored: it is either a non-existing path or lacks a specific scheme.
> > > 
> > > ERROR: Could not find a version that satisfies the requirement bitsandbytes (from versions: none)
> > > 
> > > ERROR: No matching distribution found for bitsandbytes
> > > 
> > > WARNING: Location '../input/llm-pip-2024-7-4/' is ignored: it is either a non-existing path or lacks a specific scheme.
> > > 
> > > WARNING: Location '../input/llm-pip-2024-7-4/' is ignored: it is either a non-existing path or lacks a specific scheme.
> > > 
> > > WARNING: Location '../input/llm-pip-2024-7-4/' is ignored: it is either a non-existing path or lacks a specific scheme.
> > > 
> > > ERROR: Could not find a version that satisfies the requirement peft (from versions: none)
> > > 
> > > ERROR: No matching distribution found for peft
> > > 
> > > 
> > > 
> > > ## ShelterWTopic Author
> > > 
> > > sorry, man, updated.
> > > 
> > > 
> > > 


---

> ## Nikhil Tumbde
> 
> Thanks for the notebook! I was trying to implement unsloth versions of LLMs but couldn't. This is really helpful. 
> 
> Can you tell me how long it takes for scoring?
> 
> 
> 
> > ## ShelterWTopic Author
> > 
> > ~6h
> > 
> > When set max_len =1024 , It's going to take 3h  and score 0.938
> > 
> > 
> > 
> > > ## Nikhil Tumbde
> > > 
> > > Thanks!
> > > 
> > > I have one last question (can be open ended, sorry for that). I am a new to NLP space, faced too many errors while trying to convert unsloth to seq classification from its causal LM version. Is there a way to find out what are the expected outputs and inputs for each function, I tried chatgpt but it wasn't that helpful? for eg
> > > 
> > > Llama3ForSFT should return - CausalLMOutputWithPast(
> > > 
> > >         loss=loss,
> > > 
> > >         logits=true_logits,
> > > 
> > >     )
> > > 
> > > 2.tokenize should return - {
> > > 
> > >     "input_ids": input_ids,
> > > 
> > >     "attention_mask": attention_mask,
> > > 
> > >     "labels": labels
> > > 
> > > } 
> > > 
> > > Thanks for your time!
> > > 
> > > 


---

