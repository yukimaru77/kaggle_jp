# Model randomly taking 30-100x the avg time to run

**OminousDude** *Fri Jun 28 2024 22:55:45 GMT+0900 (日本標準時)* (0 votes)

I am currently getting a lot of errors like this:

Why is this happening most of my runs take only about 4 to 6 seconds. Has anyone else had this error? Thanks in advance!



---

 # Comments from other users

> ## Sumo
> 
> not sure how relevant our experiences are, but we found a couple cases that can lead into this issue
> 
> - huggingface model offloading some weights to the CPU instead of putting them all on GPU,there's a flag to disable this behaviour
> 
> - model not reaching its stop token:
> the model is a base model rather than a chat or an instruct model, these model just go on forever
> the model is used behind some library with its internal retry mechanism (looking at you dspy), these libraries tend to prompt the model over and over until it got the right structure from the model, and this leads to some cryptic time variances
> 
> looking at your times there's a massive jump, which might hint you're making some conditional switching? like switching between hard-coded questions to an actual llm? If that's the case it's probably where to check first
> 
> 
> 
> > ## OminousDudeTopic Author
> > 
> > Thank you very much!
> > 
> > 
> > 


---

> ## Matthew S Farmer
> 
> Haven't seen this in mine. 
> 
> 
> 


---

