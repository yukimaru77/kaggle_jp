# Does increase the batch size of gemma2 9b in training do some help?

**Dlond Mike** *Sun Jul 28 2024 09:06:07 GMT+0900 (日本標準時)* (0 votes)

i new here and i'm quite confused about this



---

 # Comments from other users

> ## xiaotingting
> 
> It seems that we need to use grid search to find a suitable learning rate when the batch size is fixed. If the graphics card has some spare capacity, we can actually scale the batch size and learning rate proportionally. Generally speaking, we can think that scaling the batch size and learning rate proportionally is equivalent.
> 
> 
> 
> > ## Z Hello
> > 
> > Should the learning rate and batch size be increased or decreased simultaneously?
> > 
> > 
> > 


---

> ## ano
> 
> I also want to know how everyone chooses batch size, learning rate and architecture (like gate_proj, q_proj… when using lora)
> 
> 
> 
> > ## Dlond MikeTopic Author
> > 
> > 🥹some tips?
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > All the insights coming in 9 days 😉
> > > 
> > > 
> > > 


---

