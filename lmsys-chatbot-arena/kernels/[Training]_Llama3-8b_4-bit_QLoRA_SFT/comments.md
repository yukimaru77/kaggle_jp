# Comments 

> ## KeShuang Liu
> 
> Hello, I would like to know why max_length is set to 1024 for training and 2400 for inference. Have you tried using max_length=2400 for training?
> 
> 
> 


---

> ## OHIRA
> 
> Thanks for great work!!!
> 
> I have a question about the code.
> 
> If I set load_best_model_at_end = True  such as
> 
> args = TrainingArguments(
>     output_dir='/kaggle/output',
>     overwrite_output_dir = True,
>     evaluation_strategy = "steps",
>     save_strategy = "steps",
>     save_steps=20,
>     save_total_limit=5,
>     logging_strategy="steps",
>     logging_steps=20,
>     warmup_steps=20,
>     optim="adamw_8bit",
>     learning_rate=2e-4,
>     per_device_train_batch_size=2,
>     per_device_eval_batch_size=4,
>     gradient_accumulation_steps=2,
>     num_train_epochs=1,
>     fp16=True,
>     metric_for_best_model="log_loss",
>     greater_is_better = False,
>     report_to="none",
>     load_best_model_at_end = True
> )
> 
> I can get five best model parameters in eval set?
> 
> or I can get five last model parameters?
> 
> 
> 


---

> ## daichisaito-cs
> 
> Thank you for sharing your outstanding work!
> 
> I have one question:
> 
> How many epochs are needed to reproduce the scores of 0.9231 for Eval and 0.936 for LB?
> 
> The default number of training epochs is set to 1. Is this the same value used to achieve those scores?
> 
> Thanks
> 
> 
> 
> > ## ShelterWTopic Author
> > 
> > yep.       
> > 
> > 
> > 


---

> ## Lorry Zou
> 
> Have you try to train Gemma2 9B using this method(next-word-prediction) as well? For Llama3, this method seems to have much better performance than directly using LlamaForSequenceClassification.
> 
> 
> 


---

> ## Stringersolo
> 
> Hey [@shelterw](https://www.kaggle.com/shelterw) , thank you for sharing, I have a problems with reproducing the same result. More specifically, during training the metrics are basically the same, but when scoring on LB it's about 1.2, which is very strange and close to average/random prediction
> 
> I've also tried to read the weights directly, but it didnt help:
> 
> model_0.load_state_dict(torch.load(RAW_WEIGHTS), strict=False)
> 
> 
> 
> > ## ShelterWTopic Author
> > 
> > This may be due to lm head weight reloading randomly while loading the model.
> > 
> > Update the transformers and peft version, or choose to inherit the LlamaCausalModel class instead of LlamaPretrainedModel.
> > 
> > This also happened to me when I used Gemma2, which is weird.
> > 
> > Refer to [here](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/518408#2912471).
> > 
> > 
> > 
> > > ## Stringersolo
> > > 
> > > thank you [@shelterw](https://www.kaggle.com/shelterw) , I am gonna try it, at this link they suggested to save a score layer:
> > > 
> > > torch.save(classifier.score.state_dict(), f'{output_directory_path}/score_state_dict.pth')
> > > 
> > > in your case it would be:
> > > 
> > > torch.save(trainer.model.lm_head.state_dict(), f'output/lm_head_dict.pth')
> > > 
> > > right?
> > > 
> > > 
> > > 


---

> ## Yi-Fu Chen
> 
> May I ask why you need to implement Llama3ForSFT instead of using AutoModelForCausalLM directly? Is there any special reason?
> 
> 
> 
> > ## ShelterWTopic Author
> > 
> > For  label_token logits  and loss.
> > 
> > 
> > 


---

> ## Eido Mike
> 
> outstanding works! thanks for sharing it
> 
> 
> 


---

> ## AbaoJiang
> 
> Hi [@shelterw](https://www.kaggle.com/shelterw),
> 
> Thanks for sharing. I noticed that you used CAUSAL_LM task for training. Have you compared the performance with the one trained with the SEQ_CLS task based on LlamaForSequenceClassification?
> 
> 
> 
> > ## ShelterWTopic Author
> > 
> > I did not compare llama3-8b with SEQ_CLS, my previous experiments based on llama3-8b were worse, but it was better than gemma2-9b with SEQ_CLS.
> > 
> > 
> > 


---

> ## __ChrisQ__
> 
> Hi, thanks for the notebook.
> 
> One question: if you use all data, how do you calculate the eval score?
> 
> 
> 
> > ## ShelterWTopic Author
> > 
> > The 'compute_metrics' function in the script will be calculated automatically after 1epoch
> > 
> > 
> > 
> > > ## raconion
> > > 
> > > The 'compute_metrics' functions uses 20% of the training data for cross validation. Did you use the eval data to train the model further after evaluation? Sorry, I am not understanding what you refer to by "use all data". Does it mean that you use all data for 5 fold CV or you train the model with all data?
> > > 
> > > 
> > > 
> > > ## ShelterWTopic Author
> > > 
> > > Just use 80% of the data for training and 20% for validation.
> > > 
> > > 
> > > 
> > > ## raconion
> > > 
> > > Thank you for your clarification :)
> > > 
> > > 
> > > 


---

