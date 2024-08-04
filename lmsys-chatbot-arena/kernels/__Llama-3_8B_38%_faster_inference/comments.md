# Comments 

> ## Crystal Veil
> 
> Great LLM finetuning code
> 
> 
> 


---

> ## Zac Wing
> 
> impressive work!
> 
> 
> 


---

> ## toolman
> 
> thx, great work
> 
> 
> 


---

> ## Matt McDonagh
> 
> I didn't even know dynamic padding was a thing.
> 
> I love learning new tricks. Some are massive. Some are little edges. They all make us better.
> 
> Thanks for sharing this work.
> 
> 
> 


---

> ## Kishan Vavdara
> 
> Great work [@emiz6413](https://www.kaggle.com/emiz6413) ! Thank you, We needed this!
> 
> 
> 


---

> ## jiangli59
> 
> Can you provide the instruction about how to  enable Memory-Efficient Attention?
> 
> 
> 
> > ## Eisuke MizutaniTopic Author
> > 
> > What I did was setting global flag to enable memory-efficient attention to true by calling
> > 
> > ```
> > torch.backends.cuda.enable_mem_efficient_sdp(True)
> > 
> > ```
> > 
> > Please note that mem_efficient_sdp is enabled by default, so this is redundant.
> > 
> > 
> > 


---

> ## Lorry Zou
> 
> Nice work [@emiz6413](https://www.kaggle.com/emiz6413) ! Could you share a little bit about how you trained the model? Did you train on Kaggle or another platform? How long did it take and maybe some hyperparameter tricks? Thank you very much!
> 
> 
> 
> > ## Eisuke MizutaniTopic Author
> > 
> > [@lorryzouzelun](https://www.kaggle.com/lorryzouzelun)  The model is trained in [@kishanvavdara](https://www.kaggle.com/kishanvavdara)'s another [notebook](https://www.kaggle.com/code/kishanvavdara/lmsys-llama-3-tpu-train). 50% of the training data is used and takes about 2 hours using kaggle TPU.
> > 
> > 
> > 
> > > ## Lorry Zou
> > > 
> > > Thank you for your reply! So you just used [@kishanvavdara](https://www.kaggle.com/kishanvavdara)'s model weights for inferencing without fine-tuning for yourself? 
> > > 
> > > 
> > > 
> > > ## Eisuke MizutaniTopic Author
> > > 
> > > Yes, that's correct.
> > > 
> > > 
> > > 


---

> ## bao
> 
> Thanks for your sharing，i have a question is that why don't you do padding when call tokenizer with padding=True ？ but use pad_without_fast_tokenizer_warning to padding？
> 
> 
> 
> > ## Eisuke MizutaniTopic Author
> > 
> > That is the very part doing dynamic padding.
> > 
> > 
> > 


---

