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

