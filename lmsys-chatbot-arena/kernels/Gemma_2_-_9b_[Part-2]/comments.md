# Comments 

> ## superferg
> 
> May I ask if you have any plans to train gemma2 for direct classification? I have obtained good scores on the local validation set, but I am unable to achieve corresponding scores on the public leaderboard. I suspect that the Llama3 inference code has been directly modified to gemma2, causing some issues.
> 
> [Details](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/518408)
> 
> 
> 
> > ## Valentin Werner
> > 
> > Make sure you are using the same processing in your inference notebook. The tokenizer, model class and input processing should be identical. For me, it often also helps to test my CV inside the submission notebook to see if this is similar score is achieved. If you quantize differently during submission than during training you may expect some discrepancy (but not along the lines of .95 -> 1.0)
> > 
> > 
> > 


---

