# Comments 

> ## Kareem Abdelhamed
> 
> nice modeling bro 
> 
> 
> 


---

> ## SiddhVRTopic Author
> 
> Can anyone help diagnose why the submissions on this notebook keep failing?
> 
> Thanks
> 
> 
> 
> > ## XXX
> > 
> > hi [@siddhvr](https://www.kaggle.com/siddhvr), the competition will  re-run you code and the hidden dataset can be larger. I think may be your submission ran out of memory and failed to complete. (Of course, this is just my guess 😉)
> > 
> > 
> > 
> > > ## SiddhVRTopic Author
> > > 
> > > In that case, the prompt usually is, "Notebook ran out of memory", but what I see, in my case, it says, "Notebook threw an exception".
> > > 
> > > 
> > > 


---

> ## Luciango
> 
> Having gotten oom results when changing gemma2 checkpoint to my own fine-tuned one, if there any advices?
> 
> 
> 


---

> ## Vitalii Bozheniuk
> 
> won't it be easier to kick off LLAMA on one GPU and Gemma on another? 
> 
> 
> 
> > ## Valentin Werner
> > 
> > You are right, there should be some time gain with this approach, as you only load each model once. Other than that, not much difference. This code is probably this way, because the original inference notebook was only for one model type. It is easier to just copy it, than adjust it
> > 
> > 
> > 


---

