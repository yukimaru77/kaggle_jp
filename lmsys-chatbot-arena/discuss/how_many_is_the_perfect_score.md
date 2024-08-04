# how many is the perfect score?

**Anya** *Sat Jun 22 2024 17:17:35 GMT+0900 (日本標準時)* (0 votes)

Im new to kaggle.

Till now, Ive seen scores range in 0.5 to 1.7

I wonder how many is the perfect score so I can evaluate my score level.

Is it 5, 10 or 100?



---

 # Comments from other users

> ## Valentin Werner
> 
> The metric "log_loss" allows for a score of 0.0 (e.g., exactly perfect predictions every time). An "educated guess" score (predicting the distribution of the train set) gets you a score of about 1.097.
> 
> The problem is that human preferences, which we are trying to predict, are not clearly predictable. This is because if we both write a prompt, we may prefer different responses - so how is our model supposed to learn which responses are better. Because the problem is this hard to predict, the "ceiling" of the score is much higher than 0.0 - more along the lines of 0.75 or 0.8 (just a gut feeling)
> 
> 
> 
> > ## AnyaTopic Author
> > 
> > I got it😃. Thanks  for such a detailed reply.
> > 
> > 
> > 


---

> ## AnyaTopic Author
> 
> After reading the leaderboard I find that the lower one scores, the higher he ranks?
> 
> 
> 
> > ## Yichuan Gao
> > 
> > Yes it is, since the score is calculated as log loss, the lower the loss, the better your guesses are
> > 
> > 
> > 


---

