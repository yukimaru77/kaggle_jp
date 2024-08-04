# Game environment still not stable? 🤔

**Kuldeep Rathore** *Mon Jun 24 2024 21:21:31 GMT+0900 (日本標準時)* (0 votes)

How come the below game ended in the round one and the points are allotted? 

Episode link: [https://www.kaggle.com/competitions/llm-20-questions/leaderboard?dialog=episodes-episode-55162391](https://www.kaggle.com/competitions/llm-20-questions/leaderboard?dialog=episodes-episode-55162391)

[@bovard](https://www.kaggle.com/bovard) 



---

 # Comments from other users

> ## waechter
> 
> The agent from Chris Deotte is in error, see Answer: none and [Err] 
> 
> Probably due to the keywords/category change.
> 
> 
> 
> > ## Kuldeep RathoreTopic Author
> > 
> > Got it but the point is other two opponents got +19 which is fine, but Giba got +5 which shouldn’t be there. Ideally if one of the player of a team is giving error then that person should get negative score but the second team member should get 0 instead of giving +5.
> > 
> > 
> > 
> > > ## waechter
> > > 
> > > I agree, this a been pointed out in the discussion [https://www.kaggle.com/competitions/llm-20-questions/discussion/508415](https://www.kaggle.com/competitions/llm-20-questions/discussion/508415) 
> > > 
> > > They made a change:
> > > 
> > > A fix for this should be rolling out tomorrow. The reward when an agent fails after this should be net zero. For example the failing agent might get -21 and the other three get an average of +7 each.
> > > 
> > > But i'm not sure it works as intented since here the reward is 19+19+5-13 != zero
> > > 
> > > 
> > > 
> > > ## Bovard Doerschuk-Tiberi
> > > 
> > > The values themselves won't equal zero, especially depending upon the uncertainty of each agent. 
> > > 
> > > 
> > > 


---

