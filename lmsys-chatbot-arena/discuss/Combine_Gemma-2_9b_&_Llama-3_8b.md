# Combine Gemma-2 9b & Llama-3 8b

**G John Rao** *Fri Jul 26 2024 17:50:20 GMT+0900 (日本標準時)* (7 votes)

Hi everyone, 

I have the two highest-scoring LB notebooks together in each device of T4 GPU.

LB: 0.945

[notebook](https://www.kaggle.com/code/jaejohn/lmsys-combine-gemma-2-9b-llama-3-8b)



---

 # Comments from other users

> ## xiaotingting
> 
> The effect is better after integrating the two models, but is there any way to fuse the two models other than directly adding them together?
> 
> 
> 
> > ## G John RaoTopic Author
> > 
> > You can surely explore weighted averaging, stacking, bagging, etc. I am sure it'll improve the predictions. 
> > 
> > 
> > 


---

> ## Akeryu Ryuu
> 
> I tried this and the results weren't that good, lb of 1.15. And with each submission taking about 8~9 hours each, tuning the submission weights to lb is hard so hopefully you have better luck than me.
> 
> 
> 
> > ## Valentin Werner
> > 
> > Results this bad might indicate that you did not align indices properly. You may want to sort by index before ensembling
> > 
> > 
> > 
> > > ## Akeryu Ryuu
> > > 
> > > Thank you for the advice but I don't really believe that's the problem because I was joining the submissions by id before ensembling. 
> > > 
> > > This is the code I used
> > > 
> > > ```
> > > gemma_sub = pd.read_csv("gemma_submission.csv")
> > > llama_sub = pd.read_csv("llama_submission.csv")
> > > 
> > > merged_submission = pd.merge(gemma_sub, llama_sub, on='id', suffixes=("_1", "_2"))
> > > 
> > > merged_submission["winner_model_a"] = (merged_submission["winner_model_a_1"] + merged_submission["winner_model_a_2"])/2
> > > merged_submission["winner_model_b"] = (merged_submission["winner_model_b_1"] + merged_submission["winner_model_b_2"])/2
> > > merged_submission["winner_tie"] = (merged_submission["winner_tie_1"] + merged_submission["winner_tie_2"])/2
> > > 
> > > final_submission = merged_submission[["id", "winner_model_a", "winner_model_b", "winner_tie"]]
> > > 
> > > ```
> > > 
> > > 
> > > 
> > > ## Valentin Werner
> > > 
> > > Did you validate individual performance of these models? Have you maybe mixed up the input format you used for training with another input format? Or maybe you have mixed up the IDs during inference?
> > > 
> > > Mathematically it is EXTREMELY unlike that two models that perform below / at .950 together go to 1.15. In general, to achieve 1.1x your models need to be overconfident in wrong labels.
> > > 
> > > 
> > > 
> > > ## Akeryu Ryuu
> > > 
> > > Thanks to your comment, I decided to double-check my setup. After about half an hour of searching, I discovered that I hadn't loaded the fine-tuned LoRA weights for the Gemma model. It turns out I missed those two lines while copying the code. So, a big thank you for pointing this out.
> > > 
> > > 
> > > 


---

> ## Ravshan Kutkovin
> 
> Can you explain more about Combine Gemma-2 9b & Llama-3 8b?
> 
> 
> 
> > ## G John RaoTopic Author
> > 
> > Another user did a good job explaining everything, here: [https://www.kaggle.com/code/nabojyotipandey/dual-model-inference-gemma2-9b-llama3-8b](https://www.kaggle.com/code/nabojyotipandey/dual-model-inference-gemma2-9b-llama3-8b)
> > 
> > 
> > 


---

