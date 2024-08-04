# Llama 3.1 7b vs Gemma 9b (sft)?

**SeshuRaju 🧘‍♂️** *Sun Jul 28 2024 02:44:32 GMT+0900 (日本標準時)* (5 votes)

Local cv for Gemma is better than Llama 3.1 -> is it same for you too?

- same settings as sft, qlora, 4bit, same batch size.

Gemma 9b:  

  Step 10: loss = 2.3923

  Step 20: loss = 2.0361

  Step 30: loss = 1.4534

  Step 40: loss = 1.6852

  Step 50: loss = 1.3092

LLama 3.1 7b:

  Step 10: loss = 2.6542

  Step 20: loss = 3.2993

  Step 30: loss = 2.4278

  Step 40: loss = 2.0152

  Step 50: loss = 2.3515



---

 # Comments from other users

> ## Helmut12
> 
> By looking through the Code page, I think Gemma should be better for this competition.
> 
> 
> 


---

> ## sayoulala
> 
> The training loss alone is not enough to determine which is not performing well.
> 
> 
> 


---

> ## Ashwani
> 
> In my limited experiments, gemma9b is performing better than llama3.1 and llama3. 
> 
> Both llama3.1 & llama3 are giving similar performance with llama3.1 marginally better. 
> 
> 
> 
> > ## Merlyn Wang
> > 
> > Same here.
> > 
> > 
> > 


---

> ## CPMP
> 
> This is train loss or validation loss?
> 
> 
> 
> > ## SeshuRaju 🧘‍♂️Topic Author
> > 
> > it's training loss in the post [@cpmpml](https://www.kaggle.com/cpmpml) 
> > 
> > validation loss per epoch wise.
> > 
> >   for local cv - Llama 3.1 - 1.097 and Gemma - 0.981
> > 
> > 
> > 
> > > ## CPMP
> > > 
> > > 1.09 is a model that did not learn. Something is wrong here IMHO.
> > > 
> > > 
> > > 


---

