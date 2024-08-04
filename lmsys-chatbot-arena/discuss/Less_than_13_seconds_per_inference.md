# Less than 1.3 seconds per inference?

**Rishiraj Acharya** *Fri May 03 2024 14:21:19 GMT+0900 (日本標準時)* (17 votes)

There are approximately 25000 rows in test data and 9 hours runtime translates to less than 1.3 seconds per inference. Does this make usage of Large Language Models obsolete for this competition? I might not know of any LLM that runs this fast but I'm open to learning.



---

 # Comments from other users

> ## Raja Biswas
> 
> For my subs, the inference runtimes were as below (T4 x2):
> 
> - deberta-v3-large (~1.5hrs)
> 
> - mistral 7b (~4hr)
> 
> - llama3 8b (~4hr)
> 
> Max sequence length used: 1.8k
> 
> 
> 


---

> ## Siddhantoon
> 
> You can even batch process the data, why run every row sequentially.
> 
> 
> 


---

> ## Fritz Cremer
> 
> I published a deberta-v3-base notebook which predicts in under an hour. I think even deberta-v3-large should be no problem:
> 
> [https://www.kaggle.com/code/fritzcremer/lmsys-deberta-v3-base-baseline](https://www.kaggle.com/code/fritzcremer/lmsys-deberta-v3-base-baseline)
> 
> 
> 


---

> ## Angela
> 
> You are right. It seems that it is unable to utilize prompt engineering for LLM in this competition. 
> 
> 
> 


---

