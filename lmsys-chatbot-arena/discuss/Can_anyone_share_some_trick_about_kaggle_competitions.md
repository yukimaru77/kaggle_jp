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

