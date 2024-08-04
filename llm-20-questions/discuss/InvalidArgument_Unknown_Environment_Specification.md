# InvalidArgument: Unknown Environment Specification

**Mitul** *Fri May 31 2024 16:34:41 GMT+0900 (日本標準時)* (2 votes)

Getting this error while making env 

InvalidArgument                           Traceback (most recent call last)

Cell In[119], line 2

      1 from kaggle_environments import make

      2 env = make(environment="llm_20_questions")

File ~\PycharmProjects\kaggle.venv\Lib\site-packages\kaggle_environments\core.py:108, in make(environment, configuration, info, steps, logs, debug, state)

    106 elif has(environment, path=["interpreter"], is_callable=True):

    107     return Environment(**environment, configuration=configuration, info=info, steps=steps, logs=logs, debug=debug, state=state)

--> 108 raise InvalidArgument("Unknown Environment Specification")

InvalidArgument: Unknown Environment Specification

from kaggle_environments import make

env = make(environment="llm_20_questions")



---

 # Comments from other users

> ## Bovard Doerschuk-Tiberi
> 
> A new version has been pushed to PyPI, pip install should work as normal now.
> 
> 
> 


---

> ## loh-maa
> 
> Same error when using kaggle-environments installed locally via pip, it's gone when importing from a cloned repo.
> 
> 
> 
> > ## MitulTopic Author
> > 
> > Thanks, its working now  
> > 
> > 
> > 
> > ## Rinku Sahu
> > 
> > How did you do it? I am trying use the cloned repo. but it is giving error
> > 
> > 
> > 


---

> ## neelpanchal
> 
> Even i am getting this same error
> 
> 
> 


---

