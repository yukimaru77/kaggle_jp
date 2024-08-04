# Replacing response A and response B for Data Augmentation

**Takamichi Toda** *Wed Jun 05 2024 09:29:20 GMT+0900 (日本標準時)* (2 votes)

The current approach in the public code often creates features from responses A and B and uses these to train classifiers. I thought that a simple data augmentation could be achieved by swapping responses A and B and the winner labels.

However, it not works.

|  | Local | Public |
| --- | --- | --- |
| baseline | 0.997 | 1.012 |
| Augument by replace A/B | 1.011 | 1.025 |

My CV strategy is a simple one-holdout, and so far it correlates well with the Public LB ([reference](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/500031#2824772)).

It may be that whether the response is A or B is also an important feature. I had seen a thread discussing bias in evaluation depending on whether the response is A or B, but it seems to have disappeared (probably [here](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/507091)).



---

 # Comments from other users

> ## Lisa DunlapCompetition Host
> 
> Not sure how helpful this is, but position bias is a known phenomenon in both humans and LLMs: both tend to favor the first answer they are presented with. We look at this in the [original LLM as a judge paper ](https://arxiv.org/abs/2306.05685) if you want some concrete numbers of how prevalent this is 
> 
> 
> 


---

> ## Valentin Werner
> 
> My assumption is that by simply swapping, you are not creating new value for the model to learn. You are instead basically training those rows twice.
> 
> Questions:
> 
> 1) with what percentage of samples are you augmenting? If you only do 10-20% you are just making the model overfit / learn more about those samples. There might be an argument to do 100% of samples to make the model learn that resp A or B literally does not matter! (even though this might not reflect reality)
> 
> 2) are you also doing the swap with ties (keeping the tie label)? If not, you introduce class imbalance and ties are less likely to be predicted.
> 
> 
> 
> > ## Takamichi TodaTopic Author
> > 
> > Thank you for the comment.
> > 
> > 1)
> > 
> > It's 100%. By the way, I am using DeBERTa, and I conducted experiments to enable the model to know which sentence is A and which is B by adding special tokens, but it was not very effective (only a slight improvement).
> > 
> > 2)
> > 
> > The label for "tie" remains "tie" even after swapping.
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > So If you do 100%, you basically just train two epochs at the price of one. This will effect lr scheduling etc.
> > > 
> > > Did you also tune parameters in your experiment (e.g., warm up ratio or epochs)
> > > 
> > > 
> > > 
> > > ## Takamichi TodaTopic Author
> > > 
> > > You may be right.
> > > 
> > > We tried three different patterns for the learning rate (smaller is better).
> > > 
> > > 
> > > 


---

