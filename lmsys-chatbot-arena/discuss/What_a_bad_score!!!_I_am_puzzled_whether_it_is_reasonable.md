# What a bad score!!! I am puzzled whether it is reasonable?

**Turbo** *Tue Jul 30 2024 13:28:30 GMT+0900 (日本標準時)* (4 votes)

I encountered inference score bad problem.

I used gemma-2 to classify and got local cv(20% data) = 0.9366, lb=0.968.

Also, I used llama-3 to regression and got local cv(20% data) = 0.916, lb=0.934.

What a bad result!!!.

Inspired by [@jsday96](https://www.kaggle.com/jsday96), so I tried to both inference on kaggle and local. The results are shown below. The results are train data head 10. The difference is very small. I am puzzled whether it is reasonable?



---

 # Comments from other users

> ## KeShuang Liu
> 
> After reading your discussion, I tested my model, which was very useful to me. I don't know why my local prediction is so different from the prediction on Kaggle, which leads to a big difference between cv and lb. I think this is the reason. This gave me new ideas. Thank you very much for your discussion.
> 
> 
> 
> > ## TurboTopic Author
> > 
> > Hey, the results have big difference. Maybe some bugs in the code which you need to check.
> > 
> > 
> > 


---

> ## Helmut12
> 
> I think that may be normal in kaggle competition. Is this related to overfitting of the data? Like there is a significant pattern in our test set. I heard that there is a huge discrepancy between LB and the final result in a previous competition because of overfitting.
> 
> 
> 


---

> ## justin1357
> 
> cv is lower than lb, that's normal.
> 
> 
> 
> > ## TurboTopic Author
> > 
> > low 0.02. Others said the results of cv and lb are very small.
> > 
> > 
> > 
> > > ## justin1357
> > > 
> > > In my exp, cv low 0.02 too
> > > 
> > > 
> > > 


---

