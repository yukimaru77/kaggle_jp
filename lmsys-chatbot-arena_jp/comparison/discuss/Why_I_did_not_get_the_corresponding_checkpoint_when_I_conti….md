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


<style>
.column-left{
  float: left;
  width: 47.5%;
  text-align: left;
}
.column-right{
  float: right;
  width: 47.5%;
  text-align: left;
}
.column-one{
  float: left;
  width: 100%;
  text-align: left;
}
</style>


<div class="column-left">

# original

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



</div>
<div class="column-right">

# 日本語訳

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




</div>