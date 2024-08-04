# Is the Kaggle provided compute enough to join this competition?

**Andreas Bisi** *Tue May 28 2024 13:29:59 GMT+0900 (日本標準時)* (5 votes)

After participating in the Home Credit competition, I am looking forward to joining a new one. The objective of this new competition seems interesting. From a quick look at public notebooks, it appears that two popular models are LightGBM and Llama 3 8B. For the latter, is it possible to do any fine-tuning on Kaggle, or will I need to rent A100 instances?



---

 # Comments from other users

> ## Ivan Vybornov
> 
> I would not recommend finetuning on kaggle, from my experience finetuning llama with QLoRA on TPU is extremely painful timewise therefore I had to rent a RTX 4090, which does the job roughly for 8 hours.
> 
> 
> 
> > ## Dr. Gopalashivabalasubramanium Chandrashekaran
> > 
> > Thank you for your input. In your experience, how much more time will fine tuning on kaggle take vs your RTX 4090's 8 hours? Will it take 2-3x longer? I don't want to rent a RTX 4090 lol
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > Agreed on paying for Experiments. I think 2-4x is realistic. If I remember correctly, peft llama3 for some epochs took about 20 hours on kaggle and ca 8 hours on 4090. Main reason is that you can only use 2x T4 for this, which are even slower.
> > > 
> > > 
> > > 


---

> ## Kishan Vavdara
> 
> You can use kaggle TPU's for finetuning. 
> 
> 
> 


---

> ## bogoconic1
> 
> I would not advise using Kaggle compute to fine tune, unless you don’t have another choice. Quick experiments with small turnaround is beneficial in a competition and using a faster GPU like A100 helps. Also, in Kaggle, you only have 30 GPU hours + 20 TPU hours (if you know how to use it) per week
> 
> 
> 


---

> ## Valentin Werner
> 
> If you are only playing to win, then it might not work on kaggle compute. If you are here to learn, embrace the challenge and try to come up with solutions that work with the kaggle compute.
> 
> 
> 


---

