# The best score of each team on LB is only the best of the most recent 3 submissions

**Kha Vo** *Wed Jun 05 2024 23:37:18 GMT+0900 (日本標準時)* (3 votes)

I have a bot with 796 score which should place 2nd. But when I submitted some new submissions, those pushed my 796-score bot out of the LB ranking.

Is this what we should expect? I guess an absolute best score should be displayed there on LB.

And how are the final bots selected for scoring at the end?

[@bovard](https://www.kaggle.com/bovard) 



---

 # Comments from other users

> ## Bovard Doerschuk-Tiberi
> 
> There were significant problems with keeping all submissions active (compute, leaderboard implications) so our current system only keeps the most recent three submissions. 
> 
> When the submission deadline hits, only your active agents will be considered for the final leaderboard
> 
> 
> 
> > ## Kha VoTopic Author
> > 
> > Thanks for clarifying. However it is still strange if Kaggle doesn’t allow us to choose which bots to operate. Day to day experiment and submission can be plentiful, and selecting different bot versions can spread a long period of time. 
> > 
> > 
> > 
> > > ## Bovard Doerschuk-Tiberi
> > > 
> > > Thanks for the feedback!
> > > 
> > > Arbitrary switching agents in and out causes a few different vectors to game the system so enabling that is unlikely.
> > > 
> > > We have considered the ability to mark a submission as "evergreen" so it doesn't get disabled (but still counts towards your total). How does that sound to you?
> > > 
> > > 
> > > 


---

> ## mhericks
> 
> I think that this is due to the fact, that one can only have three active agents. Since there is (currently) no way to select which agents are evaluated, only the 3 most recent submissions keep participating. Also, as the score of an agent (in some way) depends on all other agents on the leaderboard and the exact scoring mechanism used at the time, it would not be correct to take the maximum score of all agents ever submitted if the agent corresponding to the maximum is no longer re-evaluated constantly. 
> 
> Still, I totally agree that there should be a way to select which agents to participate in the leaderboard games. 
> 
> 
> 


---

