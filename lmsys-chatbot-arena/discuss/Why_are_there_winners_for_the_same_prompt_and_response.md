# Why are there winners for the same prompt and response?

**JunHua Liao** *Mon May 13 2024 22:47:54 GMT+0900 (日本標準時)* (9 votes)

Why is prompt, response_a, and response_b the same, and there is a situation where model_a wins or model_b wins? Shouldn't it be winner_tie?



---

 # Comments from other users

> ## Valentin Werner
> 
> Does it make sense? No. Did the user click it? Yes.
> 
> 
> 


---

> ## Sergey Saharovskiy
> 
> [@feattar](https://www.kaggle.com/feattar) thanks for posting your findings, I will leave it here:
> 
> 
> 
> > ## Valentin Werner
> > 
> > 
> > 
> > 
> > 


---

> ## Asher B.
> 
> According to the blog [https://huyenchip.com/2024/02/28/predictive-human-preference.html](https://huyenchip.com/2024/02/28/predictive-human-preference.html)
> 
> shared in this discussion: [https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/499847](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/499847)
> 
> These are the noises and we may improve our model by droping these instances. Thanks for sharing!
> 
> 
> 
> > ## JunHua LiaoTopic Author
> > 
> > Thanks for sharing!
> > 
> > 
> > 
> > ## Kishan Vavdara
> > 
> > I think dropping them won't help much, test data may contain similar instances. If the model predicts tie for such instances with high prob, then such instances will be penalized more increasing log loss. Solution would be ensembles :)  
> > 
> > 
> > 
> > > ## Asher B.
> > > 
> > > Thanks for correction. I think dropping should be a good idea in production, but in this competition, that's ture! 
> > > 
> > > 
> > > 
> > > ## Valentin Werner
> > > 
> > > I am not sure if I agree - if we are unsure about the test data (much like we would be in producton), shoud we not strive to create a model that is robust, in the sense of predicting the objective truth?
> > > 
> > > It might be worth testing if we should provide more balanced predictions on these labels, like [0.3, 0.2, 0.5] - as first model might be preferred due to position bias - while tie is the objective truth on these labels.
> > > 
> > > 
> > > 


---

