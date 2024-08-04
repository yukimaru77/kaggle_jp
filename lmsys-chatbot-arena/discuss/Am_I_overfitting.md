# Am I overfitting?

**KeShuang Liu** *Sat Jul 27 2024 12:07:19 GMT+0900 (日本標準時)* (1 votes)





---

 # Comments from other users

> ## Valentin Werner
> 
> Overfitting is best analyzed in combination with validation loss. If you validation loss has a similar drop to your training loss (which I guess would win the competition at these scores), you are not overfitting. In general, if training loss goes down while validation loss is either plateauing or going back up, you are likely overfitting.
> 
> Another way of estimating overfitting is to look at what performance you expect and what you see on the train loss. We would not expect the model to go to .800 or even below it - therefore, it is likely to overfit. However, this does not mean that the model was best before this downward shift at steps 550 - you should use a validation score to evaluate how well the model predicts on unseen data
> 
> 
> 
> > ## KeShuang LiuTopic Author
> > 
> > Yes, but my validation set can only be calculated after this epoch is completed, and it takes a long time, so I am considering whether to stop it directly
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > You can set how often you want to evaluate. It does indeed take a lot of time, so I think evaluating 2-4 times is feasible.
> > > 
> > > 
> > > 
> > > ## KeShuang LiuTopic Author
> > > 
> > > Yes, my model should be overfitting. Its loss on the validation set is 0.99
> > > 
> > > 
> > > 


---

> ## xiaotingting
> 
> It has to be combined with the indicators of the validation set. If the loss on the validation set is large, but very low on the training set, it is overfitting, and you can consider adding regularization such as weight decay. If the loss on both the validation set and the training set is low, it means the model is effective.
> 
> 
> 
> > ## KeShuang LiuTopic Author
> > 
> > The next validation metric will be calculated in a few hours, and I am considering whether to abandon this training directly
> > 
> > 
> > 


---

> ## Rise_Hand
> 
> Wow so Crazy! 600 epochs !!! Which kind of model you are using 
> 
> 
> 
> > ## KeShuang LiuTopic Author
> > 
> > steps,haha
> > 
> > 
> > 


---

> ## AYUSH KHAIRE
> 
> [@liukeshuang](https://www.kaggle.com/liukeshuang) yes about 580 to 600 you are overfitting. 
> 
> 
> 
> > ## KeShuang LiuTopic Author
> > 
> > Then I probably don't need to continue training now
> > 
> > 
> > 


---

