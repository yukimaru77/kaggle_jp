# Are you able to provide more info about what types of words can be keywords?

**Nicholas Broad** *Thu May 16 2024 07:08:41 GMT+0900 (日本標準時)* (8 votes)

It's common for animals and physical objects (e.g. pencil) to be keywords, but could concepts like "justice" or random verbs like "jump" be options for the keyword?

edit: I see in your code you say, "The keyword is a specific person, place, or thing."

Is the list of keywords and categories in [keywords.py](https://www.kaggle.com/competitions/llm-20-questions/data) exhaustive?

Why are there keywords that are multiple words? 

```
"keyword": "washington dc",
"alts": ["washington dc"]

```



---

 # Comments from other users

> ## G John Rao
> 
> I can answer the 2nd part. 
> 
> Why are there keywords that are multiple words?
> 
> I think the focus is, multiple words can mean one thing, one idea, one concept. A name of a country may have multiple words but it represents a single nation.
> 
> 
> 
> > ## Nicholas BroadTopic Author
> > 
> > Sure, I just think the phrasing in the rules (“guess the secret word”) implies that it will be a single word. I’d prefer if it said “guess the secret word(s)”
> > 
> > 
> > 
> > > ## G John Rao
> > > 
> > > Yeahh, but the focus should be on, one word can also mean multiple things. For example, "May" could mean different things in the English language. This competition goes deeper, a lot deeper. 
> > > 
> > > 
> > > 


---

> ## Duke Silver
> 
> wondering if just the main keyword is passed to the lmm and the others are just answers that are also acceptable, or are all of them given to the lmm?
> 
> 
> 
> > ## Chris Deotte
> > 
> > From EDA on the interface [here](https://www.kaggle.com/code/rturley/run-debug-llm-20-questions-in-a-notebook) (and my own local work), our answerer bot only gets the main keyword.
> > 
> > 
> > 


---

> ## Nicholas BroadTopic Author
> 
> [@bovard](https://www.kaggle.com/bovard),
> 
> Are you able to comment on this?
> 
> 
> 
> > ## Bovard Doerschuk-Tiberi
> > 
> > Keywords will always be a person, place or thing. We are strongly considering adding more keywords / categories in keywords.py during the competition. After the submission deadline we'll use a new, unpublished keyword list that agents will not have access to.
> > 
> > Let me know if you have other questions!
> > 
> > 
> > 


---
