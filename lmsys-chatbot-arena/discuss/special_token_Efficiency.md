# special token Efficiency

**박민욱peterminpark** *Fri Jul 19 2024 07:18:04 GMT+0900 (日本標準時)* (0 votes)

many organized their dataset into  +  +  input text form. I tried adding , ,  as special tokens and trained a model but the result was not good does anyone know why this is the case.



---

 # Comments from other users

> ## cm391
> 
> have you resized the embedding to take into account that you have added new tokens?
> 
> Gemma contains some spare special tokens in its tokenizer - you could just repurpose those!
> 
> 
> 
> > ## 박민욱peterminparkTopic Author
> > 
> > thx
> > 
> > I did resize my model.
> > 
> > recycling unused special token is a good idea. I'll try that out
> > 
> > 
> > 


---

