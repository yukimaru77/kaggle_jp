# Will all agents play with the same frequency on the hidden test set?

**JK-Piece** *Wed Jul 17 2024 00:01:09 GMT+0900 (日本標準時)* (3 votes)

Currently, old agents do not play much. In these settings, old agents with high scores have the chance to remain the leaders, and old ones with low scores have almost no chance to grow in skill. Therefore, I have questions regarding the evaluation on the hidden test set.

Will all agents play at the same frequency on the new vocabulary of keywords?

Will the skill rating be reset to 600 for all agents before the rerun?

[@Host](https://www.kaggle.com/Host) #Kaggle



---

 # Comments from other users

> ## RS Turley
> 
> The competition host has the freedom to adjust the frequency of matches based on their observations regarding the quality of the score convergence toward a stable set of final rankings, so (1) might be hard for them to answer without losing that flexibility.
> 
> Regarding (2), if you look at the internal scoring data, you’ll notice that an agent has a mean score that we observe on the leaderboard and also a standard deviation. The standard deviation decreases after each match, reflecting more certainty around that agent’s score. I believe in similar Kaggle environment competitions, the host reset each agent’s standard deviation but not the mean.
> 
> 
> 


---
