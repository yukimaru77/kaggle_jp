# Why is this agent getting points for this?

**OminousDude** *Mon Jun 03 2024 11:13:00 GMT+0900 (日本標準時)* (0 votes)

I am activaly checking the LB and when I saw this I knew something was off. How did hsling get +27 for this? Is there another bug in the loss function or something?

[https://www.kaggle.com/competitions/llm-20-questions/leaderboard?dialog=episodes-episode-54945938](https://www.kaggle.com/competitions/llm-20-questions/leaderboard?dialog=episodes-episode-54945938)

This one didn't have a score increase (it was 0) but still what?!?!

[https://www.kaggle.com/competitions/llm-20-questions/leaderboard?dialog=episodes-episode-54945203](https://www.kaggle.com/competitions/llm-20-questions/leaderboard?dialog=episodes-episode-54945203)



---

 # Comments from other users

> ## Bovard Doerschuk-Tiberi
> 
> First game:
> 
> [1st] hsling 601 (+27)
> 
> [1st] Phạm Huỳnh Thiên Phú 599 (+7)
> 
> [Err] mhericks 578 (-74)
> 
> [1st] Toon 597 (+28)
> 
> mhericks agent errored out, so it counts as a loss for that agent and all other agents get 1st place. When they win they compare their collective rating vs mhericks rating which should give them an expected probability of winning. In this case all of the agents are relatively the same rated.
> 
> However this is also a second component of our scoring system, an uncertainty term that decays as agents play more game. In this case both Toon and hsling have a larger uncertainty term (so they get more rating from the game) than Pham team (who receives less rating)
> 
> Second game:
> 
> [1st] hsling 599 (-0)
> 
> [1st] ITASps 599 (-0)
> 
> [1st] Gauranshu Rathee 596 (+1)
> 
> [1st] Guan 600 (-0)
> 
> The game result here was a tie (everyone on 1st place) and everyone is similarly rated so the expected change in rating should be quite small. Besides the -0 here, this looks expected.
> 
> Let me know if you have any other questions!
> 
> 
> 
> > ## OminousDudeTopic Author
> > 
> > Thank you very much for this explanation didn't see the error in the first one!
> > 
> > 
> > 


---
