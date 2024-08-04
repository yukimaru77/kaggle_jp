# How to run a model on two cards

**KeShuang Liu** *Mon Jun 17 2024 17:22:30 GMT+0900 (日本標準時)* (0 votes)

I loaded my model on the CPU and it took up 19g, while the GPU p100 only had 16g. However, I found that if I use two t4 blocks for a total of 30g, can I deploy my model to two t4 blocks? What should I do?



---

 # Comments from other users

> ## Minato Ryan
> 
> If you are using transformers library, use device_map="auto".
> 
> like this,
> 
> ```
> AutoModelForCausalLM.from_pretrained("google-bert/bert-base-cased", device_map="auto")
> 
> ```
> 
> 
> 
> > ## KeShuang LiuTopic Author
> > 
> > Thank you very much for your reply. I succeeded using your method
> > 
> > 
> > 


---

