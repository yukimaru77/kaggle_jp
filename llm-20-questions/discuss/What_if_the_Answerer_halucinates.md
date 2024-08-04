# What if the Answerer halucinates

**FelipeDamasceno** *Sat May 18 2024 22:33:15 GMT+0900 (日本標準時)* (3 votes)

Hello everyone, I am not sure if I understood everything about the evaluation, but it seems to me that the one who will be answering the questions is also a LLM, so I was wandering, what if the LLM that answers the questions give the wrong answer? In that case the other LLM will not be able to get the right secret word. Is there something in the evaluation that penalize the LLM in this case? Is there a way to know if the LLM answered the question wrong?



---

 # Comments from other users

> ## Nicholas Broad
> 
> The penalty is that you are less likely to win the game. You will drop in the rankings and get paired with bad models
> 
> 
> 
> > ## FelipeDamascenoTopic Author
> > 
> > but, is it the penalty for the bad answerer or the model playing against it? Because you can have a model that is good at making questions and finding the secret word, but the answer to questions is not really good as the idea is to have two different models, one for questions and finding the model and other to answer to questions, correct? 
> > 
> > 
> > 
> > > ## Bovard Doerschuk-Tiberi
> > > 
> > > Each submission has a ranking that changes after each match. An agent that often responds incorrectly will most likely never win a match (and thus consistently drop in rating).
> > > 
> > > Yes, for that match the model paired with the bad answerer will also lose rating for that game, but can go on to gain rating with other partners in other matches.
> > > 
> > > Note that since you are matched with agents around your skill level, this becomes less of a problem the higher in the leaderboard you go.
> > > 
> > > 
> > > 


---

> ## Aatif Fraz
> 
> Yes, then that team is doomed, the answerer LLM as well. It is a cooperative 2v2, you have to get lucky with teammates I guess. 
> 
> 
> 


---
