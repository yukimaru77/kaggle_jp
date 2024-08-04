# チェックポイントからトレーニングを再開したときに、対応するチェックポイントを取得できなかった理由

**KeShuang Liu** *2024年7月28日 日曜日 21:09:52 日本標準時* (2票)

```python
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
```

以前は `save_steps=5000` でしたが、今は `200` に変更しました。しかし、200ステップ後も対応するチェックポイントを取得できませんでした。

---
# 他のユーザーからのコメント

> ## Piotr Gabrys
> 
> [編集] このコードが問題を解決するかどうかは不明です。
> 
> こんにちは！このようにすることができます。
> 
> ```python
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
> )
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
> 参照: [https://github.com/huggingface/transformers/issues/7198](https://github.com/huggingface/transformers/issues/7198)
> 
> お役に立てれば幸いです！
> 
> 
> 
> > ## KeShuang Liuトピック作成者
> > 
> > ご回答ありがとうございます。試してみます。
> > 
> > 
> > 
> > > ## Piotr Gabrys
> > > 
> > > うまくいきましたか？
> > > 
> > > 
> > > 
> > > ## KeShuang Liuトピック作成者
> > > 
> > > [@nbroad](https://www.kaggle.com/nbroad) の方法を使用しました。うまくいきました。
> > > 
> > > 
> > > 
---
> ## Nicholas Broad
> 
> チェックポイントから再開しているためです。再開すると、古い値が使用されます。チェックポイントの `training_args.bin` を上書きして新しい値を使用すれば、うまくいくと思います。
> 
> 
> 
---
> ## Dlond Mike
> 
> 同じ問題です。
> 
> 
> 
---


