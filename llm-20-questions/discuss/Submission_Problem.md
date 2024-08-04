# Submission problem

**Naive Experimentalist** *Fri Jun 14 2024 04:45:36 GMT+0900 (日本標準時)* (2 votes)

Hi there.

I was able to submit my very first and very weak agent based on flan t5 large model.

Now I developed a new one (hopefully much smarter) using both Gemma and Flan T5. When submitting I have the validation round error, but logs are empty. I have no idea where to find help with this one. How to debug it? Before when having validation round problems, I saw some errors in the logs.

My logs look as follows:

log0: [[{"duration": 26.110363, "stdout": "", "stderr": ""}]]

log1: [[{"duration": 26.111393, "stdout": "", "stderr": ""}]]

Also no errors in the notebook execution log: Successfully ran in 483.4s

I have absolutely no idea what to do. Maybe someone was in this situation before.

UPDATE (Jun 14, 2024):

After a thorough analysis, it turned out that the Kaggle environment, when trying to run an agent and failing to match the appropriate name, calls the last function defined in the file. This may be obvious to everyone else, but it was a surprising discovery for me.

BTW, I still don't know how to name agents correctly so that the Kaggle environment calls them directly. For now, I have worked around this by defining a def proxy(obs) function at the end, which calls the appropriate agent depending on obs.role. 



---

 # Comments from other users

> ## waechter
> 
> You can add print in your agent function to help you debug, you will see them in stdout
> 
> 
> 
> > ## Naive ExperimentalistTopic Author
> > 
> > You are right. I thought the only problem with validation round can be when raising error from my notebook during the play, therefore didn't make traditional print-based debugging. Will do and try.Thx
> > 
> > 
> > 


---

> ## 玛丽·伊丽莎白·马特米斯
> 
> I have absolutely no idea too
> 
> 
> 


---
