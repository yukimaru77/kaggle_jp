# The hidden test dataset has distribution shift 

**Xin** *Sat Aug 03 2024 02:30:10 GMT+0900 (日本標準時)* (-11 votes)



After extracting some features from training dataset, then a full dataset one epoch train, I thought the single Gemma model can have a good leaderboard result, but the reality is eval:0.867 leaderboard: 0.933.

I think it might mean the data distribution is to some extent different than the train dataset, then after I extracting features from test dataset, the score then be low.



---

 # Comments from other users

> ## CPMP
> 
> What you see is that your model performs better on its training data than on new data. This is to be expected.
> 
> One way to not be surprised  is to split your triaining data into two piece. One piece you use for training, and one piece you use for evaluating your model once trained. The second piece is often called a validation dataset, or a test dataset.
> 
> 
> 


---

> ## Valentin Werner
> 
> You are facing a lot of backlash for a "beginner mistake" - even if only training for one epoch, you want to validate your model on unseen data, your model has theen the "validation" data already once, so it knows it. This is one form of data leakage.
> 
> Just from this training it is impossible to expect how well your model is going to perform on a leaderboard submission. Often, it is better to set aside 10-20% of data to make sure you have a local validation and a leaderboard score rather then fitting your model on all the data.
> 
> It is possible to probe the data distribution of the LB dataset, however, not with this approach. 
> 
> 
> 
> > ## XinTopic Author
> > 
> > Yeah. I understand. One epoch also probably brings model to an underfit status. From the result, I intuitively think that either the distribution between train and hidden test dataset different or there is a high similarity on train dataset (I mean tokenized data, maybe also because I only extract the first part from texts) which causes such an obvious overfit. 
> > 
> > 
> > 


---

> ## JM
> 
> Your eval_dataset is taking a subset of your training dataset…
> 
> 
> 
> > ## XinTopic Author
> > 
> > Yeah. But I think one epoch, the model only see the data once.
> > 
> > 
> > 
> > > ## David.Ricardo.H.X
> > > 
> > > You didnt get what he means…… 
> > > 
> > > Your eval_dataset is taking a subset of your training dataset… 
> > > 
> > > Do you have a concept of what is the difference between train set, validation set and test?
> > > 
> > > 
> > > 


---

