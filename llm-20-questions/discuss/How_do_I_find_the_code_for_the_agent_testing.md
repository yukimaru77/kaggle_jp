# How do I find the code for the agent testing?

**OminousDude** *Thu Jul 04 2024 09:07:24 GMT+0900 (日本標準時)* (0 votes)

I am trying to load my model on my local machine from my "submission.tar.gz" file how do I get the model/agent_fn so that I could test it? Thank you in advance for any help!



---

 # Comments from other users

> ## Melinda
> 
> Do you mean you want to run the kaggle env locally on your machine? Or are you trying to do something else? At any rate this is how I run it locally.  Maybe something in here is what you're looking for. It assumes your submission.tar.gz is unzipped in a way that main.py is in a folder ./submission/lib (adapted from [https://www.kaggle.com/code/rturley/run-debug-llm-20-questions-in-a-notebook](https://www.kaggle.com/code/rturley/run-debug-llm-20-questions-in-a-notebook))
> 
> ```
> # These are just dummy agents so that I'm not running 4 versions of my agent.
> def simple_agent1(obs, cfg):
>     # if agent is guesser and turnType is "ask"
>     if obs.turnType == "ask": response = "Is it a duck?"
>     elif obs.turnType == "guess": response = "duck"
>     elif obs.turnType == "answer": response = "no"
>     return response
> 
> def simple_agent2(obs, cfg):
>     # if agent is guesser and turnType is "ask"
>     if obs.turnType == "ask": response = "Is it a bird?"
>     elif obs.turnType == "guess": response = "bird"
>     elif obs.turnType == "answer": response = "no"
>     return response
> 
> from kaggle_environments import make
> import kaggle_environments
> keyword = "argentina"
> alts = ["argentina"]
> kaggle_environments.envs.llm_20_questions.llm_20_questions.category = "Place"
> kaggle_environments.envs.llm_20_questions.llm_20_questions.keyword_obj = {'keyword':keyword,'alts':alts}
> kaggle_environments.envs.llm_20_questions.llm_20_questions.keyword = keyword
> kaggle_environments.envs.llm_20_questions.llm_20_questions.alts = alts
> 
> env = make("llm_20_questions", debug=True)
> game_output = env.run(agents=[simple_agent1, simple_agent2, "./submission/lib/main.py", "./submission/lib/main.py"])
> env.render(mode="ipython", width=800, height=400)
> 
> ```
> 
> I also have some code in my main.py that looks to see if it's running on my machine or not, based on environment variables, and if it is, it loads the model from the right relative path and sets the device type appropriately for my machine.
> 
> 
> 
> > ## OminousDudeTopic Author
> > 
> > Ok thank you I think this should work for me thanks!
> > 
> > 
> > 


---
