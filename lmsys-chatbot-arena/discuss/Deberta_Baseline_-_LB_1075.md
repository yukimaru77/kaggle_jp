# Deberta Baseline - LB 1.075

**Fritz Cremer** *Fri May 03 2024 21:45:56 GMT+0900 (日本標準時)* (5 votes)

I made a very quick deberta-v3-base baseline:

[https://www.kaggle.com/code/fritzcremer/lmsys-deberta-v3-base-baseline/notebook](https://www.kaggle.com/code/fritzcremer/lmsys-deberta-v3-base-baseline/notebook)

Currently, it only uses a small fraction of the train data and doesn't get a great score. But this is how the code for a deberta submission could look like.

Possible improvements:

- Utilize all data

- K Fold cross-validation

- Swap the responses for more data

- Formulate the loss differently

Especially the last one. I think it could make sense to have a two stage model. In the first stage, just predict if a response won a duel or not (without providing the other response), in the second stage, using two such predictions + hand crafted features to predict the better response. I think this looks like a very interesting competition, with not one straight forward path.

Let me know what you think!



---

 # Comments from other users

> ## Nicholas Broad
> 
> Just so you know, this is basically just random guessing.
> 
> ```
> from sklearn.metrics import log_loss
> log_loss([1], [[1/3, 1/3, 1/3]], labels=[0,1,2])
> 
> # 1.0986122886681098
> 
> ```
> 
> 
> 
> > ## Valentin Werner
> > 
> > The Notebook exactly replicates the label distribution. It seems that a basic starter with huggingface Trainer is not able to learn from the data.
> > 
> > 
> > 
> > ## Fritz CremerTopic Author
> > 
> > [@nbroad](https://www.kaggle.com/nbroad) Yes, I know. It was more like a general setup to fit a model for this task with huggingface. I found that the training was very unstable, on some runs the model learned more than just the label distribution (e.g. on LB the notebook has 1.075 with the submitted version), and on others it failed completely. But then again, it is not a well tuned approach at all, just a quick first day approach 😄
> > 
> > 
> > 


---

