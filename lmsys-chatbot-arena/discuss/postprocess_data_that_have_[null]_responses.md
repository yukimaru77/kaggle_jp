# postprocess data that have [null] responses

**ano** *Fri Aug 02 2024 22:59:02 GMT+0900 (日本標準時)* (1 votes)

Training dataset have some data whose responses for both A and B are [null].

[https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/502303](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/502303)

Therefore, I implemented the code to postprocess null data, assuming the same percentage of winner_model_a, winner_model_b and winner_tie for the train and test dataset. However, the score got worse a little bit. Has anyone had the same experience?



---

 # Comments from other users

> ## Valentin Werner
> 
> I think the problem we are facing is how random the results for these samples are. 
> 
> Guessing average distributions for these samples might be a good approach (if actually both are null), but I think you are focusing on a very niche problem for your post-processing. On the 57k training samples, 19 samples fit into this pattern according to the post you link. Assuming same distribution in the dataset you are doing postprocessing for 10 samples. And 2-3 of which would be in the public lb.
> 
> As the 19 samples in the training set are not a representative sample size to start with, it is quite likely that you should just "trust your model". 
> 
> 
> 
> > ## anoTopic Author
> > 
> > I appreciate your detailed explanation. It seems like the randomness of the results for these samples is indeed a significant factor. The null data in the test dataset, which you estimated to be only 2-3 affecting the public leaderboard, is just too small.
> > 
> > In this case, it might be ineffective to assume the same distribution based on these few samples.
> > 
> > 
> > 


---

