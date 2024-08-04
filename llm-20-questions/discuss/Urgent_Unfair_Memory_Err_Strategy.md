# Urgent: Unfair Memory Err Strategy

**CchristoC** *Tue Jul 09 2024 13:20:08 GMT+0900 (日本標準時)* (5 votes)

I found that if someone's agent gets an Err, all the other 3 Agents will get a + Point.

This can be misused by questioner prompting as much words as possible (lengthy prompts), so that if the answerer's agent has less available memory, it will result in an Err and all points will be given to the other 3 agents, while the Err agent get a - point.

Even if they all didn't guess the correct keyword.

This strategy is vulnerable to those who don't have a condition to give a backup answer when there is no output from the agent, especially for those who are using big size LLMs and lengthy answerer prompt too.

Should be fixed by not giving + points to the other 3 if an agent gets an Err. (Only - point to the Err agent.)



---

 # Comments from other users

> ## Chris Deotte
> 
> This was discussed [here](https://www.kaggle.com/competitions/llm-20-questions/discussion/508415) and other threads.
> 
> 
> 
> > ## CchristoCTopic Author
> > 
> > But it's still not fixed yet?
> > 
> > 
> > 
> > > ## RS Turley
> > > 
> > > I don't see an issue. The rules are pretty clear that a question can be up to 2000 characters. Each agent should be responsible not to run out of time or memory. 
> > > 
> > > 
> > > 
> > > ## Chris Deotte
> > > 
> > > 
> > > But it's still not fixed yet?
> > > 
> > > The non-error teams used to receive like +150 points! It is much better than it was.
> > > 
> > > 
> > > 


---

> ## Coldstart Coder
> 
> Thanks for the heads up, will need to put in safe guards for my own agents to make sure it doesn't error out like that.
> 
> 
> 


---

