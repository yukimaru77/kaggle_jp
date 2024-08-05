# How far can a boosting get you?

**Ivan Vybornov** *Sat Jun 08 2024 05:37:05 GMT+0900 (日本標準時)* (1 votes)

I am curious what is a score upper bound on using solely a boosting?

The best performing public notebook that only utilizes a GBDTs so far is [https://www.kaggle.com/code/andreasbis/lmsys-chatbot-arena-tf-idf#Model-Training-%F0%9F%A7%A0](https://www.kaggle.com/code/andreasbis/lmsys-chatbot-arena-tf-idf#Model-Training-%F0%9F%A7%A0)

But the difference with llama3 inference is more than significant (1.011 vs 0.989) which makes me wonder if one should even bother trying to get below 0.98 with it.



---

 # Comments from other users

> ## Valentin Werner
> 
> I was wondering the same. Different than the notebook you mentioned above I went a pure Text characteristic based Feature approach (Length, Paragraph Count, …) and got to around 1.036
> 
> This is so far away from Raja's current score that I think it is not worth to be the main model for the prediction
> 
> If you are not going for the win and instead want to learn about boosting and feature engineering, I would suggest you try to get below 1.0 yourself
> 
> 
> 


---
