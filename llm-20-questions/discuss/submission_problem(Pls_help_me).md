# submission problem(Pls help me) 

**philipha2** *Wed Jul 03 2024 19:48:30 GMT+0900 (日本標準時)* (1 votes)

I am a beginner in this competition. 

I just tried to submit a notebook but it's keep saying "Validation Episode failed(Error)" 

What is the problem?



---

 # Comments from other users

> ## Sumo
> 
> hi, you can download the agent logs and see the failure. You'll see either a traceback of a crash, or something about the model taking way too long to load / respond
> 
> 
> 
> > ## Dheeraj Bhukya
> > 
> > I have tried different LLMs, Gemma 2b-it worked but got “validation episode failed” for Gemma 7b-it-quant and Phi 3-mini. I checked agent logs it’s an empty json file. Idk why?
> > 
> > 
> > 
> > ## Mitsutani
> > 
> > Any idea of what it could be if the logs are completely empty?
> > 
> > 
> > 
> > > ## Sumo
> > > 
> > > normally those will be in other logs, like there are 3 files, the replay logs, agent1, agent2 (or something, I haven't submitted in a while). But the exception can be in any of those files.
> > > 
> > > 
> > > 
> > > ## gguillard
> > > 
> > > Check the notebook logs for any clue.  My submission logs were empty, I figured there was an apt error in the notebook logs because I disabled internet while the notebook was trying to install pigz.
> > > 
> > > 
> > > 


---
