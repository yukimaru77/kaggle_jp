# 要約 
## ディスカッション要約: 重みとバイアスのログを避ける方法

このディスカッションは、Kaggle の LMSYS - Chatbot Arena 人間による好み予測チャレンジに参加しているユーザー suri@7 が、モデルのトレーニング中に重みとバイアスのログを避ける方法について質問したことから始まりました。

ユーザー suri@7 は、`TrainingArguments` を使用してモデルをトレーニングしようとしていましたが、重みとバイアスのトークンIDを求められていました。彼らは、重みとバイアスをモデルに適用したくありませんでした。

ユーザー waechter は、`TrainingArguments` の `report_to` パラメータを `'none'` に設定することで、リモートログを無効にできることを指摘しました。`report_to` パラメータは、結果とログを報告する統合のリストを指定します。`'none'` を設定すると、統合には報告されません。

その後、suri@7 は、モデルのトレーニング後にオフラインで予測を提出する方法について質問しました。彼らは、モデルを Kaggle 入力パスに保存すると、予測に提出されたときにロードされないことに気づきました。

waechter は、`output_dir` パラメータが `kaggle/input` ディレクトリに設定されているため、読み取り専用である `kaggle/input` ディレクトリに書き込もうとしていることを指摘しました。彼は、事前トレーニング済みモデルは `kaggle/working` ディレクトリに保存する必要があることを説明しました。

最終的に、suri@7 は waechter のアドバイスに従い、問題を解決することができました。

**要約:**

* ユーザーは、モデルのトレーニング中に重みとバイアスのログを避ける方法について質問しました。
* `TrainingArguments` の `report_to` パラメータを `'none'` に設定することで、リモートログを無効にできます。
* モデルは、`kaggle/working` ディレクトリに保存する必要があります。
* ユーザーは、waechter のアドバイスに従って問題を解決することができました。


---
## 重みとバイアスのログを避ける方法

**suri@7** *2024年7月10日 水曜日 18:24:36 日本標準時* (0票)

モデルのトレーニングを試みたところ、重みとバイアスのトークンIDを求められました。重みとバイアスをモデルに適用したくありません。

```python
training_args = TrainingArguments(
  output_dir="./kaggle/input/lmsys-chatbot-arena/bert_model",
  learning_rate=2e-5,
  per_device_train_batch_size=3,
  per_device_eval_batch_size=3,
  num_train_epochs=2,
  weight_decay=0.01,
  evaluation_strategy="epoch",
  save_strategy="epoch",
  load_best_model_at_end=True,
)
trainer = Trainer(
  model=model,
  args=training_args,
  train_dataset=train_dataset,
  eval_dataset=test_dataset,
  tokenizer=tokenizer,
  data_collator=data_collator,
  #compute_metrics=compute_metrics,
)
trainer.train()
```

---

## 他のユーザーからのコメント

> ## waechter
> 
> リモートログを使用しない場合は、`TrainingArguments` に `report_to='none'` を設定してください。
> 
> `report_to` (str または List[str], オプション、デフォルトは "all") — 結果とログを報告する統合のリスト。サポートされているプラットフォームは "azure_ml"、"clearml"、"codecarbon"、"comet_ml"、"dagshub"、"dvclive"、"flyte"、"mlflow"、"neptune"、"tensorboard"、"wandb" です。"all" を使用すると、インストールされているすべての統合に報告され、"none" を使用すると、統合には報告されません。
> 
>   [https://huggingface.co/docs/transformers/en/main_classes/trainer](https://huggingface.co/docs/transformers/en/main_classes/trainer) から
> 
> 
> 
> > ## suri@7トピック作成者
> > 
> > 助けてくれてありがとう [@waechter](https://www.kaggle.com/waechter) 、モデルのトレーニング後、オフラインで予測を提出する方法を知りたいです。モデルを Kaggle 入力パスに保存すると、予測に提出されたときにロードされません。
> > 
> > 
> > 
> > > ## waechter
> > > 
> > > `output_dir="./kaggle/input/lmsys-chatbot-arena/bert_model",`
> > > 
> > > これは間違っていると思います。なぜなら、読み取り専用である `kaggle/input` ディレクトリに書き込もうとしているからです。
> > > 
> > > 事前トレーニング済みモデルは `kaggle/working` ディレクトリに保存する必要があります: `output_dir="kaggle/working/bert_model"`
> > > 
> > > 
> > > 
> > > ## suri@7トピック作成者
> > > 
> > > わかりました、ありがとう
> > > 
> > > 
> > > 
---

**翻訳のポイント:**

*  `TrainingArguments` の `report_to` パラメータについて、日本語で自然な説明を追加しました。
*  `kaggle/input` ディレクトリが読み取り専用であることを明確に説明しました。
*  `kaggle/working` ディレクトリにモデルを保存する必要があることを強調しました。
*  ユーザーのコメントを日本語で自然な文章に翻訳しました。

