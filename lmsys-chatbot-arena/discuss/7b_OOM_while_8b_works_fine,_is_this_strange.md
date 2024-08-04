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

