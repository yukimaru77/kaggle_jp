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

