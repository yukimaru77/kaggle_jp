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

