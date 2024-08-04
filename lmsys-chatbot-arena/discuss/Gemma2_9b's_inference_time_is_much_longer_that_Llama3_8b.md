# Gemma2 9b's inference time is much longer that Llama3 8b?

**Dylan Liu** *Wed Jul 17 2024 15:55:30 GMT+0900 (日本標準時)* (2 votes)

With same submission code, my Llama3 8b model takes ~4h to finish the inference, but my Gemma2 9b takes ~8h. Are you experiencing the same?



---

 # Comments from other users

> ## Ashwani
> 
> I haven't seen such difference. For me its 25% more time in gemma than lamma. 
> 
> If you want to further reduce inference time, check dynamic padding for each batch. 😀
> 
> 
> 


---

> ## Sparsh Tewatia
> 
> 2 billion parameters more at work my friend.
> 
> 
> 
> > ## Dylan LiuTopic Author
> > 
> > 2 billion parameters? I thought it was 1b different. But even so, double inference time is still not much explainable.
> > 
> > 
> > 
> > > ## Sparsh Tewatia
> > > 
> > > gemma always claims less parameter if you count it shows 10.2 billion parameters , also LLAMA 3 uses grouped query attention , and has around 120 K tokens in tokenizer while Gemma uses self attention and has 250 K tokens in tokenizer which can explain the difference in speed.
> > > 
> > > 
> > > 


---

> ## Yichuan Gao
> 
> I would check the data type for both weights and compute_dtype. If you are using bfloat16 in compute, it will be MUCH slower since T4 does not support bfloat16, and need to emulate it by other methods. In my experience, Gemma2 9b and Mistral 7b inference time does not have much a difference (3~4h range), provides using 4bit weights and float16 dtype.
> 
> 
> 


---

> ## Valentin Werner
> 
> For me, also training time with same parameters is 50% slower than Llama3-8b which seems insane. But its all in the architecture, as Sparsh pointed out.
> 
> 
> 
> > ## Robert0921
> > 
> > For LoRa, even though Gemma2 is more accurate than Llama3, I was unable to achieve better results due to the 9-hour time limit.
> > 
> > 
> > 


---

> ## Robert0921
> 
> Not only inference, but also training takes longer, because 9b>8b？
> 
> 
> 


---

