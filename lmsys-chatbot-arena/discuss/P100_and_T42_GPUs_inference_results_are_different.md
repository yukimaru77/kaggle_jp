# P100 and T4*2 GPUs inference results are different

**Femca7** *Tue Jul 16 2024 09:47:35 GMT+0900 (日本標準時)* (1 votes)

Recently, I found that the inference results differ when using a single GPU compared to using two GPUs. Another issue is that the inference results on my local machine and on Kaggle also have slight differences.

Does anyone know the reason for this?

Using one GPU:  

id     winner_model_a  winner_model_b  winner_tie 

1233961     0.245430    0.517676    0.236894

Using two GPUs:  

id     winner_model_a  winner_model_b  winner_tie 

1233961     0.238452    0.535787    0.225761



---

 # Comments from other users

> ## Valentin Werner
> 
> I also noticed that the scores are different across transformer versions.
> 
> 
> 


---

