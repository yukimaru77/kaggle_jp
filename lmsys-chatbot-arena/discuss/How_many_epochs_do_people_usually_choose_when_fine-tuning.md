# How many epochs do people usually choose when fine-tuning?

**KeShuang Liu** *Sat Jul 27 2024 22:40:05 GMT+0900 (日本標準時)* (1 votes)

As a beginner, I am eager for a score increase, but reality keeps hitting me. If we train for 1 epoch and 2 epochs with the same parameters and configuration respectively, will training for 2 epochs produce the same results as training for 1 epoch at the end of the first epoch, or will it be slower to become proficient?



---

 # Comments from other users

> ## Valentin Werner
> 
> There are a bunch of different questions in here. First, lets losely define what an epoch is: An epoch is a Forward and Backward Propogation through your whole Training dataset; this means, that your model saw all your training data once. Two epochs mean it saw all the training data twice.
> 
> This means, that the results of one epoch training and two epochs training will be different. However, the results of epoch 1 in a single epoch training should be around the same as the results of epoch 1 in a two epoch training (assume no learning rate scheduling).
> 
> What is a go-to number of epochs? The go-to number I see most often when finetuning pretrained models is three. However, for larger models (with peft) this value tends to be lower (for example two) and for larger datasets this value tends to be lower too. This is because the model learns more information within a single epoch.
> 
> Now, the last important note on epochs is learning rate scheduling. Often learning rates are scheduled to reduce learning rate in later epochs. Lets assume the learning rate decreased linear from start of the first epoch until the end of the third epoch. This means that the model will overfit less in the second and even less in the third epoch, while still being able to learn nuances about the training data, that can improve your score. This also means that a single epoch training with lr scheduling will have different results than a two epoch training with scheduling, as the learning rate will hit 0 much earlier in the first case. 
> 
> In general, transformer trainings are non-deterministic and you need to set a seed if you want to replicate exact results.
> 
> 
> 
> > ## KeShuang LiuTopic Author
> > 
> > Thank you for your reply.I have learned a lot from it, I will keep trying more.
> > 
> > 
> > 


---

> ## Mr.T
> 
> When I train with two epochs, I experience severe overfitting.
> 
> 
> 


---

> ## xiaotingting
> 
> The more data there is, the smaller the epochs need to be fine-tuned. Otherwise, the larger the epochs need to be fine-tuned.
> 
> 
> 


---

> ## KeShuang LiuTopic Author
> 
> Can someone help me clarify my doubts
> 
> 
> 


---

