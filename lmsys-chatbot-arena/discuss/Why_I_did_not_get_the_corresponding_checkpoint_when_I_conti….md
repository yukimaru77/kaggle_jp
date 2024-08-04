# Why I did not get the corresponding checkpoint when I continued training from the checkpoint and reset save_steps? My save_steps=5000 before, and now I changed it to 200, but after 200 steps, I did not get the corresponding checkpoint.

**KeShuang Liu** *Sun Jul 28 2024 21:09:52 GMT+0900 (日本標準時)* (2 votes)

training_args = TrainingArguments(

    output_dir=config.output_dir,

    overwrite_output_dir=True,

    report_to="none",

    num_train_epochs=config.n_epochs,

    per_device_train_batch_size=config.per_device_train_batch_size,

    gradient_accumulation_steps=config.gradient_accumulation_steps,

    per_device_eval_batch_size=config.per_device_eval_batch_size,

    logging_steps=10,

    eval_strategy="epoch",

    save_strategy="steps", 

    save_steps=200,        # 每5000步保存一次

    # eval_steps=2000, 

    optim=config.optim_type,

    fp16=True,

    learning_rate=config.lr,

    warmup_steps=config.warmup_steps,

    resume_from_checkpoint="/liukeshuang/lora_model/gemma_bnb_4_g8/checkpoint-2873"

)



---

 # Comments from other users

> ## Piotr Gabrys
> 
> [EDIT] It's uncertain whether this code solves the problem.
> 
> Hi! You can do it like this:
> 
> ```
> training_args = TrainingArguments(
> output_dir=config.output_dir,
> overwrite_output_dir=True,
> report_to="none",
> num_train_epochs=config.n_epochs,
> per_device_train_batch_size=config.per_device_train_batch_size,
> gradient_accumulation_steps=config.gradient_accumulation_steps,
> per_device_eval_batch_size=config.per_device_eval_batch_size,
> logging_steps=10,
> eval_strategy="epoch",
> save_strategy="steps",
> save_steps=200, # 每5000步保存一次
> # eval_steps=2000,
> optim=config.optim_type,
> fp16=True,
> learning_rate=config.lr,
> warmup_steps=config.warmup_steps
> 
> trainer = Trainer(
>         model=model,
>         args=training_args,
>         train_dataset=dataset['train'],
>         eval_dataset=dataset['test'],
>         tokenizer=tokenizer,
>     )
> 
> trainer.train("/liukeshuang/lora_model/gemma_bnb_4_g8/checkpoint-2873")
> 
> ```
> 
> reference: [https://github.com/huggingface/transformers/issues/7198](https://github.com/huggingface/transformers/issues/7198)
> 
> Hope that helps!
> 
> 
> 
> > ## KeShuang LiuTopic Author
> > 
> > Thanks for your reply, I will try
> > 
> > 
> > 
> > > ## Piotr Gabrys
> > > 
> > > Has it worked?
> > > 
> > > 
> > > 
> > > ## KeShuang LiuTopic Author
> > > 
> > > I used [@nbroad](https://www.kaggle.com/nbroad) method and it works fine.
> > > 
> > > 
> > > 


---

> ## Nicholas Broad
> 
> It's because you are resuming from checkpoint. It will use your old value when you resume. I think you can overwrite training_args.bin in your checkpoint to have the new values and it should work
> 
> 
> 


---

> ## Dlond Mike
> 
> same issue
> 
> 
> 


---

