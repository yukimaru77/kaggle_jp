# Submit problem(please help me)

**tiny wood** *Fri Jul 05 2024 09:43:09 GMT+0900 (日本標準時)* (1 votes)

I am a beginner in this competition.

I just tried to submit a notebook but it's keep saying "Validation Episode failed(Error)".

I also try to read the log after failure, but the log is empty

What is the problem?



---

 # Comments from other users

> ## davide
> 
> I am having the same issue, and it does not seem related to my code or to the agent's behavior.
> 
> This is the log I see from one of the agent:
> 
> [[{"duration": 0.002077, "stdout": "", "stderr": "Traceback (most recent call last):\n  File \"/opt/conda/lib/python3.10/site-packages/kaggle_environments/agent.py\", line 43, in get_last_callable\n    code_object = compile(raw, path, \"exec\")\n  File \"/kaggle_simulations/agent/main.py\", line 1\n    include the main.py code under this for submission\n            ^^^\nSyntaxError: invalid syntax\n\nDuring handling of the above exception, another exception occurred:\n\nTraceback (most recent call last):\n  File \"/opt/conda/lib/python3.10/site-packages/kaggle_environments/agent.py\", line 159, in act\n    action = self.agent(*args)\n  File \"/opt/conda/lib/python3.10/site-packages/kaggle_environments/agent.py\", line 125, in callable_agent\n    agent = get_last_callable(raw_agent, path=raw) or raw_agent\n  File \"/opt/conda/lib/python3.10/site-packages/kaggle_environments/agent.py\", line 64, in get_last_callable\n    raise InvalidArgument(\"Invalid raw Python: \" + repr(e))\nkaggle_environments.errors.InvalidArgument: Invalid raw Python: SyntaxError('invalid syntax', ('/kaggle_simulatio"}]]
> 
> Maybe anyone can help? [@bovard](https://www.kaggle.com/bovard) 
> 
> 
> 


---

> ## OminousDude
> 
> There are two logs: Agent 0 and Agent 1. Are you sure that you check both of them?
> 
> 
> 


---

> ## Code Hacker
> 
> Me too… Help me…
> 
> 
> 
> > ## Krens
> > 
> > The last time I encountered "Validation Episode failed (Error)" was because I removed the restrictions on the answers "yes" and "no" during debugging, which resulted in the error being thrown when the agent answered other answers during submission. In addition, you also need to pay attention to whether the run timeout, whether the number of characters exceeds the limit, etc.
> > 
> > 
> > 


---
