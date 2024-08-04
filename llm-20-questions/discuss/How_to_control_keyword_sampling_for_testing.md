# How to control keyword sampling for testing?

**loh-maa** *Mon Jun 10 2024 00:41:34 GMT+0900 (日本標準時)* (1 votes)

It seems the keyword is drawn only once upon import kaggle_environments. So when working with Notebooks, it takes a VM reset to test the notebook with a new keyword, or perhaps I missed the way to re-draw the keyword? A way to control the sampling of keywords for testing would be helpful.

I tried

```
import importlib
importlib.reload(kaggle_environments)

```

but it doesn't work.



---

 # Comments from other users

> ## RS Turley
> 
> Yes, the keyword is set once kaggle_environments loads the "llm_20_questions" module. The easiest way to set the keyword manually (or randomly) is to change this variable. You'll also want to change the alts and category variables. 
> 
> I put an example in my public notebook ([https://www.kaggle.com/code/rturley/run-debug-llm-20-questions-in-a-notebook](https://www.kaggle.com/code/rturley/run-debug-llm-20-questions-in-a-notebook)), and the relevant code would be:
> 
> ```
> import kaggle_environments
> env = kaggle_environments.make(environment="llm_20_questions")
> 
> # Set the new keyword to "Duck"
> keyword = "Duck"
> alts = ["The Duck","A Duck"]
> kaggle_environments.envs.llm_20_questions.llm_20_questions.category = "Example"
> kaggle_environments.envs.llm_20_questions.llm_20_questions.keyword_obj = {'keyword':keyword,'alts':alts}
> kaggle_environments.envs.llm_20_questions.llm_20_questions.keyword = keyword
> kaggle_environments.envs.llm_20_questions.llm_20_questions.alts = alts
> 
> ```
> 
> 
> 
> > ## i_am_nothing
> > 
> > Will our guesser (questioner) agent be able to look at all possible keywords in final submission by calling some function from the environment
> > 
> > 
> > 


---

