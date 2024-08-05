# What is the role of llm_20_questions.py

**Matthew S Farmer** *Wed Jun 12 2024 05:41:55 GMT+0900 (日本標準時)* (0 votes)

I am having trouble understanding the role of the input .py file when thinking of this competition in context and the way that a submission should be formatted. 

Do the agents defined in the input notebook override any prompts set in our submissions? 

Should we be referencing this input file during agent creation? 

I apologize if the answer is painfully obvious, I am trying to learn here. 



---

 # Comments from other users

> ## loh-maa
> 
> You don't need to worry about llm_20_questions.py, it's part of the environment to run the game. You need to implement agent_fn function, e.g.:
> 
> ```
> def agent_fn(obs, cfg):
>     if obs.turnType == "ask":
>         response = "Is it a duck?"
>     elif obs.turnType == "answer":
>         response = "no"
>     elif obs.turnType == "guess":
>         response = "two ducks"
>     return response
> 
> ```
> 
> [This notebook](https://www.kaggle.com/code/rturley/run-debug-llm-20-questions-in-a-notebook) should help you understand.
> 
> 
> 


---

