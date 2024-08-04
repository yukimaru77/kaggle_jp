# [need help]How to use DDP to speedup sft ?

**bao** *Wed Jul 24 2024 18:42:20 GMT+0900 (日本標準時)* (0 votes)

hello，kagglers,

I use [codes ](https://www.kaggle.com/code/shelterw/training-llama3-8b-4-bit-qlora-sft/notebook) and change args like below:

```
 args = TrainingArguments(
        output_dir='/gemini/output',
        overwrite_output_dir = True,
        evaluation_strategy = "epoch",
        save_strategy = "steps",
        save_steps=200,
        save_total_limit=2,
        logging_strategy="steps",
        logging_steps=20,
        warmup_steps=20,
        optim="adamw_8bit",
        learning_rate=2e-4,
        per_device_train_batch_size=8,
        per_device_eval_batch_size=8,
        gradient_accumulation_steps=16,
        num_train_epochs=1,
        fp16=True,
        metric_for_best_model="log_loss",
        greater_is_better = False,
        report_to="none",
        accelerator="ddp"  
    )

    trainer = Trainer(
        args=args,
        model=model,
        train_dataset=ds.select(train_idx),
        eval_dataset=ds.select(eval_idx),
        data_collator=DataCollatorForSeq2Seq(tokenizer=tokenizer),
        compute_metrics=compute_metrics,
    )
    trainer.train()

```

but GPU0 utility can reach 97%+， GPU1 only got 20%- even 0%。  the total training is slower than one GPU，how to fix it ?



---

 # Comments from other users

> ## CPMP
> 
> In order to use ddp you have to spawn two processes. Here are some example from HF documentation: [https://huggingface.co/docs/transformers/v4.43.0/en/perf_train_gpu_many#scalability-strategy](https://huggingface.co/docs/transformers/v4.43.0/en/perf_train_gpu_many#scalability-strategy)
> 
> 
> 
> > ## baoTopic Author
> > 
> > Thanks, I will try it.
> > 
> > 
> > 
> > > ## CPMP
> > > 
> > > You can try the accelerate library as well. I never used it myself, but it looks simpler to use than writing your own DDP code.
> > > 
> > > 
> > > 


---

> ## Pranshu Bahadur
> 
> Hf trainer already uses ddp try not setting any accelerator
> 
> And device_map = 'auto' when loading the model
> 
> Is your model unsloth?
> 
> Because they mention that 1xT4 is 5x faster at the end
> 
> [https://huggingface.co/unsloth/llama-3-8b-bnb-4bit](https://huggingface.co/unsloth/llama-3-8b-bnb-4bit)
> 
> [Screenshot_2024-07-24-17-08-15-27_40deb401b9ffe8e1df2f1cc5ba480b12.jpg](https://storage.googleapis.com/kaggle-forum-message-attachments/2934339/20965/Screenshot_2024-07-24-17-08-15-27_40deb401b9ffe8e1df2f1cc5ba480b12.jpg)
> 
> > ## baoTopic Author
> > 
> > I remove the accelerator setting, and set device_map = 'auto' when loading the model. But got the same 
> > 
> > 
> > 
> > > ## Pranshu Bahadur
> > > 
> > > Yeah its because of unsloth quantized models training faster on 1xt4
> > > 
> > > Have you tried just using a P100?
> > > 
> > > Also can you share screenshot of memory usage while training?
> > > 
> > > 
> > > 
> > > ## baoTopic Author
> > > 
> > > I use 2x3090. the screenshot was in my last reply message.
> > > 
> > > 
> > > 
> > > ## Pranshu Bahadur
> > > 
> > > Oh then you can use way higher batch size that's why only 1 is being used right now
> > > 
> > > 
> > > 


---

