# More information on test dataset

**Matous Famera** *Thu Jun 13 2024 02:12:49 GMT+0900 (日本標準時)* (1 votes)

Hello, I have a few questions regarding the nature of test dataset.

I already know that 26% of the entire test dataset is used for public leaderboard and 74% is used for private leaderboard.

What is the difference between the train dataset and test dataset? Are the same LLMs used? Was the same dataset used for train dataset and test dataset?
How long is the test dataset? Or atleast how long compared to the train dataset is the test dataset?

Thanks if any of these questions can be answered



---

 # Comments from other users

> ## James Day
> 
> 
> What is the difference between the train dataset and test dataset? Are the same LLMs used? Was the same dataset used for train dataset and test dataset?
> 
> I've noticed there aren't any recently released models (e.g. Llama 3) in the training dataset, so I have a suspicion they split their data based on the date on which each comparison occurred and I would expect to receive messages from different LLMs during testing.
> 
> How long is the test dataset? Or atleast how long compared to the train dataset is the test dataset?
> 
> The data tab says "you can expect roughly 25,000 rows in the test set"
> 
> 
> 
> > ## Matous FameraTopic Author
> > 
> > 
> > There are 55K rows in the training data, and you can expect roughly 25,000 rows in the test set.
> > 
> > Does it mean that the entire test dataset has 25k rows or just the public leaderboard part?
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > The entire data has 25k rows, ~26% of them is public leaderboard (so about 6.5k rows).
> > > 
> > > As you probably guess, this makes trusting the public leaderboard score similar to trusting a single validation fold in a 4-fold cv setup. Thats why it is often recommended to build a good CV strategy and try to create a correlation between the CV score (which should be reliable) and the public LB score.
> > > 
> > > Also note, that the final score is ONLY the private LB, so the other 74% of the data. Meaning the fold, you may overfit on (the public LB) is NOT part of your winning score. This can lead to what we call "Leaderboard shakeup". These concepts apply to basically all kaggle competitions.
> > > 
> > > 
> > > 
> > > ## Matous FameraTopic Author
> > > 
> > > Thanks for clarification. I was asking that questions, because the length of the test dataset is related to variance and reliability of the score.
> > > 
> > > I'm aware of the concept of overfitting for public leaderboard.
> > > 
> > > 
> > > 


---

