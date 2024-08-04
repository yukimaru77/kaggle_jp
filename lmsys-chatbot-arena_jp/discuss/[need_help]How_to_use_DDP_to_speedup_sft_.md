# [助けが必要] DDP を使って SFT を高速化する方法

**bao** *2024年7月24日 水曜日 18:42:20 GMT+0900 (日本標準時)* (0 票)

こんにちは、Kagglers の皆さん。

私は [コード](https://www.kaggle.com/code/shelterw/training-llama3-8b-4-bit-qlora-sft/notebook) を使用し、以下のように引数を変更しました。

```python
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

しかし、GPU0 の使用率は 97% を超えているのに対し、GPU1 は 20% しか使用されていません。場合によっては 0% の場合もあります。トレーニング全体が 1 つの GPU を使用した場合よりも遅くなっています。どのように修正すればよいでしょうか？

---

# 他のユーザーからのコメント

> ## CPMP
> 
> DDP を使用するには、2 つのプロセスを生成する必要があります。Hugging Face のドキュメントには、いくつかの例があります。[https://huggingface.co/docs/transformers/v4.43.0/en/perf_train_gpu_many#scalability-strategy](https://huggingface.co/docs/transformers/v4.43.0/en/perf_train_gpu_many#scalability-strategy)
> 
> 
> 
> > ## baoTopic Author
> > 
> > ありがとうございます。試してみます。
> > 
> > 
> > 
> > > ## CPMP
> > > 
> > > accelerate ライブラリを試すこともできます。私は自分で使ったことはありませんが、独自の DDP コードを書くよりも簡単そうです。
> > > 
> > > 
> > > 
---
> ## Pranshu Bahadur
> 
> Hugging Face の Trainer はすでに DDP を使用しているので、`accelerator` を設定しないようにしてください。
> 
> モデルの読み込み時に `device_map = 'auto'` を設定してください。
> 
> モデルは Unsloth ですか？
> 
> 彼らは、1xT4 が 5 倍高速であると述べています。
> 
> [https://huggingface.co/unsloth/llama-3-8b-bnb-4bit](https://huggingface.co/unsloth/llama-3-8b-bnb-4bit)
> 
> [Screenshot_2024-07-24-17-08-15-27_40deb401b9ffe8e1df2f1cc5ba480b12.jpg](https://storage.googleapis.com/kaggle-forum-message-attachments/2934339/20965/Screenshot_2024-07-24-17-08-15-27_40deb401b9ffe8e1df2f1cc5ba480b12.jpg)
> 
> > ## baoTopic Author
> > 
> > `accelerator` の設定を削除し、モデルの読み込み時に `device_map = 'auto'` を設定しました。しかし、同じ問題が発生しました。
> > 
> > 
> > 
> > > ## Pranshu Bahadur
> > > 
> > > はい、Unsloth の量子化されたモデルは 1xT4 で高速にトレーニングされるためです。
> > > 
> > > P100 だけを使用してみましたか？
> > > 
> > > また、トレーニング中のメモリ使用量のスクリーンショットを共有できますか？
> > > 
> > > 
> > > 
> > > ## baoTopic Author
> > > 
> > > 私は 2x3090 を使用しています。スクリーンショットは前回の返信メッセージにありました。
> > > 
> > > 
> > > 
> > > ## Pranshu Bahadur
> > > 
> > > ああ、そうすると、はるかに大きなバッチサイズを使用できるため、現在 1 つしか使用されていないのです。
> > > 
> > > 
> > > 
---


