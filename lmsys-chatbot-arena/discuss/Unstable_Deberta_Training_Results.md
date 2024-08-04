# Unstable Deberta Training Results

**Valentin Werner** *Sat Jun 15 2024 18:19:14 GMT+0900 (日本標準時)* (29 votes)

I spent a lot of time trying the boosting approach without any tf-idf or transformer embeddings and am now moving back to training transformers. Now, early in the competition I trained a deberta-3-large model, which did not break any records, but at least learned something (like 1.039). However, all my current attempts are failing to learn yet again - even with the same parameters as the last time I trained.

Have you experienced similar results where doing rather small changes (e.g., the structure of the input string) results in the model suddenly being unable to learn at all? What are the "best practices" you learned for training deberta / llama & co during this competition (if you dont mind sharing).

Cheers!



---

 # Comments from other users

> ## James Day
> 
> I got 0.997 with deberta-v3-large by having it produce an embedding for each side of the conversation separately, then passing those embeddings to a small 2 layer fully connected classifier. That was my first baseline approach in this competition. It certainly isn't the most accurate, but worked better than what you're describing.
> 
> I haven't really had any stability problems in this competition, but most stability problems where a model fails to converge to anything better than random guessing that I've encountered in the past have stemmed from a misconfigured learning rate schedule, so you might want to try tinkering with that if you haven't already.
> 
> 
> 
> > ## Valentin WernerTopic Author
> > 
> > Welcome back to the competition, James - I remember you die some impressive training in DAIGT too. Looking forward to See you on top of the lb again!
> > 
> > Do I understand correctly that you are only using the embeddings or did you combine two deberta Models and add layers on top of it?
> > 
> > 
> > 
> > > ## James Day
> > > 
> > > My 0.997 baseline used the same deberta backbone to process each "side" of the conversation (where each side is essentially a concatenation of the initial prompt, model X's first response, the follow up prompt (if available), model X's second response… up to a 768 token max context length). The embeddings from the CLS token on each side (A & B) were then concatenated and fed to a small classification head. In other words, there was a single debeta model with a couple extra layers stacked on top. The whole thing was trainable - I did not use a frozen pretrained backbone to compute the embeddings.
> > > 
> > > The approach described above is easily beaten by scaling up to using Llama 3 8B as the foundation model.
> > > 
> > > 
> > > 


---

> ## Takamichi Toda
> 
> I am sharing what has been effective in my experiments. 
> 
> Now difficulty in securing computational resources, I am conducting experiments with DeBERTa xsmall. Please note that you may not achieve the same results due to environmental differences.
> 
> ### Label Smoothing
> 
> I am using CrossEntropyLoss and setting the label_smoothing parameter to 0.2. The reason is that competition data can be labelled differently for the same data, and I thought it could be said to be a kind of noisy data.
> 
> ### Within-task Pre-training
> 
> I train the Masked Language Model using the competition data and use these weights for fine-tuning.
> 
> ### Dropout Off
> 
> I adjusted the Dropout Ratio, but 0 was the most effective. 
> 
> Although I have heard that Dropout should be off for regression problems, this is not. I do not understand why the absence of Dropout yielded better accuracy.🧐
> 
> ### Adversarial Training
> 
> I tried AWP, and it was effective. I also plan to test other methods such as FGM.
> 
> 
> 
> > ## Valentin WernerTopic Author
> > 
> > have you had stable results between XSmall and Large? for me, the smaller models are not converging, so I only trained Large. This obviously has terrible Iteration Speed for the experiments.
> > 
> > Thanks for sharing!
> > 
> > 
> > 
> > ## Valentin WernerTopic Author
> > 
> > Once I tried training with AWP the model instantly learned nothing again - its quite interesting
> > 
> > 
> > 
> > > ## Takamichi Toda
> > > 
> > > Hmm, I wonder why.
> > > 
> > > Which model are you using? I am still using DeBERTa xsmall, so it might be due to the difference in model size.
> > > 
> > > How about applying a small value to the AWP Learning Rate?
> > > 
> > > In my case, it's 1e-4. By the way, the overall learning rate is 2e-5.
> > > 
> > > 
> > > 
> > > ## Valentin WernerTopic Author
> > > 
> > > I will have to look further into AWP, I guess. I have not used it before and took an existing kaggle notebook as basis. 
> > > 
> > > I had no success with any small model and only ever got close to 1.00 with deberta-3-large. I am also using effective batch size of 8 (2 x 4) and a lr of about 8e-6 - so that is muuuuch lower than yours… Time to do some more experiments :)
> > > 
> > > 
> > > 


---

> ## Valentin WernerTopic Author
> 
> I trained a deberta-3-large model yesterday and achieved 1.005 - same training params today get me about 1.07. It seems very unreliable to me - I have yet to schiebe good scores with lora
> 
> 
> 
> > ## James Day
> > 
> > Weird. For me the random variation from run to run is < 0.01. CV & LB are very well correlated too (pearson r = 0.97).
> > 
> > It sounds to me like something is broken or misconfigured in your training pipeline. It isn't a problem inherent to the data itself.
> > 
> > 
> > 
> > > ## yechenzhi1
> > > 
> > > Hi, may I ask how do you get your CV split? I randomly split 10% from the training dataset, and the score from CV and LB are very different, my CV score is 0.889, and LB is 0.922. 
> > > 
> > > 
> > > 


---

