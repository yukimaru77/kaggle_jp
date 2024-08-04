# Using template for instruct model?

**Weiren** *Thu Jul 11 2024 15:42:49 GMT+0900 (日本標準時)* (0 votes)

I heard that using instruct model would perform slightly better. But when I was using Llama-8b and Llama-8b-instruct without template,  they got the same LB score.

Does the template matters? I had tried using template but the score was even worse. Also, I found that using a template causes the logloss stuck…

Some details:

1 epoch

4 batch size * 2 accumulation_steps

and just trying different lora params 🤡

Any thoughts or insights on this?



---

 # Comments from other users

> ## hn
> 
> Actually anecdotally I use the Llama3 template as well for instruct and I think it’s worse off than no template for some reason. 
> 
> 
> 


---

