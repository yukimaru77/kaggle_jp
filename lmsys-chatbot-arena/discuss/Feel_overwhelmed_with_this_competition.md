# Feel overwhelmed with this competition  

**ducnh279** *Thu Jul 04 2024 04:37:33 GMT+0900 (日本標準時)* (13 votes)

Hi everyone,

Unlike other NLP competitions I've participated in, I believe that decoder-only models might outperform DeBERTa in this one. Running experiments with LLMs is very computationally and financially expensive for me, especially in this competition.

- For DeBERTa (large), I can manage to get LB: 0.993 (tuned) with 6-hour training using 2 x T4 on Kaggle

- For LLMs,  I've just run only one experiment with Mistral 7B (4-bit quantized + LoRA) and got LB: 0.991. 

For fine-tuning LLMs, one experiment is very slow and expensive to finish one fold in 15 hours with 1 A10G on Lightning Studios. If there is no special magic to get 0.9 to 0.95. I believe that by tuning (batch size, learning rate, warm-up steps, prompts), trying training tricks to stablize the training and avoid early performance saturation, or simply being able to run more than 1 epoch, I think I could get closer to LB: <= 0.95.

As a student, I find Kaggle competitions increasingly challenging and computationally expensive, particularly due to the limited access to free hardware. Relying on free GPUs from Kaggle and Colab, I often feel constrained and overwhelmed when competing.

Do you think I need to invest big bucks for this competition to pay off? As a broke student, I might have to hit up the Bank of Mom and Dad for a 'strategic investment'  haha😂



---

 # Comments from other users

> ## kagglethebest
> 
> Same feeling. 😂 I am trying to find a way to get nice score by using Deberta Base on Kaggle GPUs. If my trials are not worked, I will give up this competition.
> 
> 
> 
> > ## ducnh279Topic Author
> > 
> > Don't give up [@judith007](https://www.kaggle.com/judith007)! Let's fight until the last minute!
> > 
> > By the way, I recommend trying DeBERTa large and learning how to utilize two GPUs. I achieved a 0.988 score with DeBERTa large, which is the same score as the first public notebook using the 8-bit quantized LLaMA 8B.
> > 
> > 
> > 


---

> ## Valentin Werner
> 
> 
> 
> 
> 
> > ## Valentin Werner
> > 
> > Jokes aside, always prefer training models on hosted rental services rather than buying an expensive GPU. You can first validate on the slow kaggle GPUs / TPU or Google Collab etc. before going to the rental. The math for buying a 3090TI / 4080 / 4090 for Data Science it is not really mathing. I have a 4090 which is great for experiments, but I still cannot scale to the same experiments as the Kaggle TPU on it. 
> > 
> > It feels really bad being gates by compute resources. Stuff you can try out if renting is not an option: Some cloud providers provide research compute for limited time; you can ask your university / professors if they have compute you can do (maybe try to sell it as extra curicular, present your results in the end for some bonus points; my university had a 4x V100 setup with 128GB total that was mostly idling and my professor almost begged me to train some stuff on there so its used when nobody does research); 
> > 
> > 
> > 
> > > ## ducnh279Topic Author
> > > 
> > > Hahaha your meme tells my story! 
> > > 
> > > After this competition, I would learn about TPU training! Thanks SO much for sharing your experience!
> > > 
> > > 
> > > 


---

> ## Cody_Null
> 
> Glad someone else was able to get 7b models like mistral working in 4bit. Mine had a bug but didn’t seem like it was going to beat the llama models anyway :/ I understand your position though. It does feel that way sometime 
> 
> 
> 
> > ## ducnh279Topic Author
> > 
> > Thanks for your understanding! For sure, 7b models quantized in 4-bit will be definitely degraded in performance. You can use scaling law to set up the hyparams and try training techniques before running on the whole training set. Sorry I can't talk more about this before the competition ends.
> > 
> > 
> > 


---

> ## Taimo
> 
> Kaggle is a good starting point for students.
> 
> For educational purposes, Kaggle should remain such a place even though the size of models continues to be big. 
> 
> Google (Alphabet) should invest in more high-spec hardware for Kaggle.
> 
> 
> 
> > ## ducnh279Topic Author
> > 
> > For educational purposes, Kaggle should remain such a place even though the size of models continues to be big.
> > 
> > Agreed! I learned a lot through Kaggle competitions and the sharings from Kagglers! The "large" in models and datasets are not a too big problem with me! I will definitely continue learning and competing.
> > 
> > Google (Alphabet) should invest in more high-spec hardware for Kaggle.
> > 
> > We all hope so! hahaha
> > 
> > 
> > 


---

> ## xiaotingting
> 
> After I became a graduate student, I was fine and could use the server in the lab. But because I had to submit a paper recently and needed to do additional experiments, and there were other people in the lab using the server, I could only use it when they were not using it. If I want to fine-tune a large model, I really need a card. I currently rent two A100 cards to prepare for the experiments here, and each training takes at least two days. It is more cost-effective to rent it for the whole day, about 200 yuan for two cards a day, and it costs more than a thousand yuan to rent it for a week.
> 
> 
> 
> > ## KeShuang Liu
> > 
> > I was interning at the company and they provided me with two A800s, but due to my technical issues, I was unable to achieve good results.
> > 
> > 
> > 


---

