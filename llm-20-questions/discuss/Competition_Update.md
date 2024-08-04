# Competition Update

**Bovard Doerschuk-Tiberi** *Wed Jul 31 2024 05:47:37 GMT+0900 (日本標準時)* (17 votes)

Hey all,

Here is an update on what to expect from the final weeks of the competition.

- Active agents reduced from 3 to 2 (starting this week, which will increase the game rate)

- Question character length limit reduced from 2000 to 750 (the extra character limit was unused other than for “binary search” type questions)

- Remove “Locations” from the keyword set. (starting this week, the “locations” problem space it too small)

When the competition closes:

- The unseen secret “things” keyword list will be swapped in

- The leaderboard will be reset

- The post-evaluation period will start at 2 weeks, but will likely be extended.

Thank you all for participating! This competition is the first of its kind and we appreciate your patience while we learned along the way. We’ll take what we learned in this competition to make future competitions even better!

Happy Kaggling!

Bovard

EDIT: 

On the secret "things" keyword list

- it is taken from roughly same keyword list as the current list. 

- it will not re-use any of the current words in the keyword list

- it will not be accessible in keywords.py



---

 # Comments from other users

> ## torino
> 
> [@Hi](https://www.kaggle.com/Hi) [@bovard](https://www.kaggle.com/bovard) ,
> 
> Remove “Locations” from the keyword set. (starting this week, the “locations” problem space it too small)
> 
> That means in private keywords, the keywords will not have locations(place, landmark, mountain, river...) and only thing keywords, right?
> 
> Then agents reduced from 3 -> 2, is it keep 2 newest agents or 2 highest score agents?
> 
> 
> 
> > ## Bovard Doerschuk-Tiberi
> > 
> > Yes, keep only the "things" keywords.
> > 
> > It will be the 2 newest agents
> > 
> > 
> > 


---

> ## Ariocx
> 
> So keywords can only be “things”？
> 
> 
> 
> > ## Bovard Doerschuk-Tiberi
> > 
> > yes, that is correct
> > 
> > 
> > 


---

> ## Nicholas Broad
> 
> Is [this comment](https://www.kaggle.com/competitions/llm-20-questions/discussion/512358#2872495) no longer relevant?
> 
> Yes, the current leaderboard will be the seed of your agent going into the final evaluation period. We will ensure that agents receive enough games for the leaderboard to stabilize under the new set of words, so even if your agent is severly under ranked it should not be an issue.
> 
> 
> 
> > ## Bovard Doerschuk-Tiberi
> > 
> > Yes, that will no longer be the case.
> > 
> > 
> > 


---

> ## Andrew Tratz
> 
> A suggestion, for this or for other simulations in the future: allow participants to permanently inactivate specific bots, reducing their bot quota usage. This way, there's no need to inactivate high-scoring bots in order to continue experimenting, and if they are permanently disabled then there's no risk of anyone sandbagging by temporarily disabling and later re-enabling a strong bot. I think this would create a more robust competition with few downsides.
> 
> 
> 
> > ## Fayez Siddiqui
> > 
> > Great suggestion, I also think having the freedom of Agent selection would be great.
> > 
> > 
> > 
> > > ## OminousDude
> > > 
> > > Not a good idea as people could just enable a high-scoring old agent
> > > 
> > > 
> > > 


---

> ## Tran Anh Quan
> 
> So in the final leaderboard are there only “Things” keywords used for evaluation? Will there be no “Person” or “Place” keywords at all?
> 
> 
> 
> > ## Bovard Doerschuk-Tiberi
> > 
> > yes, only "things"
> > 
> > 
> > 


---

> ## BORAHMLEE
> 
> Hi, Do you use purely secret keywords in your final evaluation? Or do you combine them with current keywords to make the evaluation?
> 
> 
> 


---

> ## francesco fiamingo
> 
> Thanks a lot! I think we are building the best community in the world, amazed to be part of it, one technical question , i need to decide to merge with other teams, if i will do, how many agents the team can use? 2 per component of the team or two for whole team? 
> 
> 
> 
> > ## torino
> > 
> > I guess we will have only have 2 agents for whole team.
> > 
> > 
> > 
> > > ## francesco fiamingo
> > > 
> > > Wow…but this means that is better not to merge….
> > > 
> > > 
> > > 
> > > ## torino
> > > 
> > > As author said 
> > > 
> > > Active agents reduced from 3 to 2 (starting this week, which will increase the game rate)
> > > 
> > > assume if we have 10 agents for team 5 members, maybe game rate will divide from 2 agents to 10 agents, It also means less opportunity for each agent.
> > > 
> > > 
> > > 
> > ## Bovard Doerschuk-Tiberi
> > 
> > Only 2 agents per team. Once you merge together two teams they only count as a single team so they would only have 2 active agents
> > 
> > 
> > 


---

> ## Duc-Vu Nguyen
> 
> Dear [@bovard](https://www.kaggle.com/bovard),
> 
> I have a question about "It will not be accessible in keywords.py". Does this mean that we cannot know secret words by reading keywords.py or any other sources provided by the organizer?
> 
> Best regards,
> 
> 
> 
> > ## mxmm2123
> > 
> > yes, keyword.py in final lb can't access.
> > 
> > 
> > 
> > ## Bovard Doerschuk-Tiberi
> > 
> > 
> > Does this mean that we cannot know secret words by reading keywords.py or any other sources provided by the organizer?
> > 
> > That is correct. You will not be able to see the keyword list by any means.
> > 
> > 
> > 


---

> ## FullEmpty
> 
> Thank you for your update. I've walked through discussions, but this doesn't seem to be discussed.
> 
> Questions are limited to 2000  750 characters
> 
>   Guesses are limited to 100 characters
> 
> Is the limit applied per round or for total questions throughout the rounds?
> 
> Agents are given 60 seconds per round to answer
> 
>   Agents have an additional 300 overage seconds to use throughout the game
> 
> I think this means each of the questioning/guessing agent and the answering agent has 60 seconds. But when does the 60 seconds for the questioning/guessing agent start — at the point when the round begins, when the agent asks a question, or right after the answering agent responds for guessing?
> 
> 
> 
> > ## FullEmpty
> > 
> > Can anyone help???
> > 
> > 
> > 
> > > ## torino
> > > 
> > > Hi [@gowillgo](https://www.kaggle.com/gowillgo) ,
> > > 
> > > ```
> > > Questions are limited to 2000 750 characters
> > > Guesses are limited to 100 characters
> > > 
> > > ```
> > > 
> > > it apply for each question, and each guess, not cumulative across entire game.
> > > 
> > > then game work as below:
> > > 
> > > 60s first - agent 1(ask/guess)
> > > 
> > > - load model(only in step 1, ~40s for model 8b 8bit)
> > > 
> > > - return first question
> > > 
> > > - if > 60s, subtract to budget 300s
> > > 
> > > -> agent 1 stop
> > > 
> > > immediately count 60s of agent 2(answer)
> > > 
> > > - load model(~40s)
> > > 
> > > - answer question or anything you want
> > > 
> > > - if > 60s, subtract to budget 300s
> > > 
> > > -> agent 2 stop
> > > 
> > > immediately count 60s of agent 1(ask/guess)
> > > 
> > > - return guess(model was load in step 1)
> > > 
> > > …
> > > 
> > > 
> > > 
> > > ## FullEmpty
> > > 
> > > [@pnmanh2123](https://www.kaggle.com/pnmanh2123) That's so crisp clear to understand - many thanks!!! 
> > > 
> > > 
> > > 
> > > ## torino
> > > 
> > > You are welcome!
> > > 
> > > 
> > > 


---

> ## Bhanu Prakash M
> 
> Are all the items in the things category physical objects?
> 
> Can I rule out the possibility of there being virtual or abstract things?
> 
> 
> 
> > ## Bovard Doerschuk-Tiberi
> > 
> > The current list of words is roughly representative of the final list. 
> > 
> > 
> > 


---

