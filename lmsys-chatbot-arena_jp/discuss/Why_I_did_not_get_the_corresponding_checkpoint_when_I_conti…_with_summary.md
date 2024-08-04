# 要約 
このディスカッションは、Kaggleコンペティションの参加者が、トレーニングの再開時にチェックポイントから対応するチェックポイントを取得できない問題について議論しています。

**問題:**

* ユーザーは、`save_steps` を 5000 から 200 に変更した後、200 ステップ後も対応するチェックポイントを取得できませんでした。

**解決策:**

* **Piotr Gabrys** は、`Trainer.train()` メソッドにチェックポイントのパスを渡すことで、トレーニングを再開することを提案しました。これは、`TrainingArguments` にチェックポイントのパスを直接渡すよりも、より適切な方法です。
* **Nicholas Broad** は、チェックポイントから再開すると、古い `training_args.bin` が使用されるため、問題が発生すると指摘しました。新しい `training_args.bin` を使用するには、古いファイルを上書きする必要があると説明しました。

**結論:**

* ユーザーは、**Nicholas Broad** の提案に従って、`training_args.bin` を上書きすることで問題を解決しました。

**追加情報:**

* このディスカッションは、Hugging Face Transformers ライブラリを使用しているユーザーにとって役立つ情報です。
* チェックポイントからトレーニングを再開する際には、`training_args.bin` を確認することが重要です。


---
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


