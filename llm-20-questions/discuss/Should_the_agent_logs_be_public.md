# Should the agent logs be public?

**Khoi Nguyen** *Sun May 19 2024 18:39:15 GMT+0900 (日本標準時)* (11 votes)

This is the log of the latest game of (at the time of writing) 1st place Team Rigging vs 33rd place Pavel Pavlov:

I think the team names are wrong (!?) but anyway that's not the point, what happened here is that Team Rigging (I think) used the binary search method to deduce the final guess, they started with asking if the keyword is in one of the categories, then if first character is in the fist half of alphabet, and when the pool is small enough they started asking if the answer is in a sublist until they have the correct guess. 

There it goes, I knew the winning asker's strategy for that game. 

In previous bot arena competitions I guess the bot behavior was much harder to reverse engineer just from the game log, but for 20 Questions the method above is a proven strategy. At the worst case I can just download all the questions from the top teams and analyze them to build my own, is that fair?



---

 # Comments from other users

> ## Rob Mulla
> 
> I think it's intended by the competition designers. Similar to past agent based competitions: [halite](https://www.kaggle.com/competitions/halite), [connect-x](https://www.kaggle.com/competitions/connectx), you can openly see the strategy of each team as the game plays out. We don't know the exact logic and code used to produce the questions, but that can be easily inferred when the solutions are very simple.
> 
> For what it's worth this our current solution is only works because we know the subset of categories and words used in the public/(pre-deadline) leaderboard. Because of this, I don't think ultimately the public leaderboard is going to be a good indication of agents what will perform well on the private/post-deadline leaderboard.
> 
> Top teams might choose to not submit their best agents until right before the deadline so that their strategy isn't revealed. But in the end the public leaderboard is pretty useless anyways so 🤷‍♂️
> 
> 
> 


---

> ## Bovard Doerschuk-Tiberi
> 
> [@suicaokhoailang](https://www.kaggle.com/suicaokhoailang) We will be changing out the list of words after the submission deadline and then we'll wait for the scores to stabilize. Any agent assuming a fixed word list will perform quite poorly.
> 
> Final Evaluation
> 
>   At the submission deadline on August 13, 2024, submissions will be locked. From August 13, 2024 to August 27th, 2024 we will continue to run episodes against a new set of unpublished, secret words. At the conclusion of this period, the leaderboard is final.
> 
> 
> 


---

> ## Nicholas Broad
> 
> Why aren't there 4 team names shown? Shouldn't there be two for each team? One questioner and one answerer for each
> 
> edit: maybe the other two teams are at the bottom? It is a bit confusing who is on what team and what role, though
> 
> 
> 
> > ## Bovard Doerschuk-Tiberi
> > 
> > Yes, two teams are at the bottom. The team names at the top are a visual bug, I'll fix that.
> > 
> > 
> > 


---

