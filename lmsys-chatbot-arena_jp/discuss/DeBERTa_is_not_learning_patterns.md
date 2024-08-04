# DeBERTaがパターンを学習していない？
**Valentin Werner** *2024年5月6日 月曜日 18:08:22 GMT+0900 (日本標準時)* (6 votes)

皆さん、こんにちは。現在、私のスターターノートブックが常にラベル0を予測するという問題に直面しています（これは私が使用しているデータセットのサブセットで最も頻繁に見られるラベルです）。

過去には、ラベルがバランスされていてもモデルが学習しないという経験はありませんでした。

同じような経験をした方はいますか？解決策を見つけられましたか？

---
# 他のユーザーからのコメント
> ## Rich Olson
> 
> DeBERTaで同じ経験をしました。
> 
> [https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/501848](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/501848)
> 
> 要約すると、より多くのデータでトレーニングを開始するまでは、私の場合、収束しませんでした。
> 
> 小さなサブセットでトレーニングしたときは、「あれ？これはうまくいかない」という感覚がありました。すべてのデータでトレーニングした後、LB 1.030になりました。
> 
> ノートブックはこちらです。
> 
> [https://www.kaggle.com/code/richolson/deberta](https://www.kaggle.com/code/richolson/deberta) （コピーして自由に使用してください）
> 
> 
> 
> > ## Valentin Wernerトピック作成者
> > 
> > 面白いですね！1.030は間違いなく改善されていますが、精度も評価しましたか？30代後半/40代前半のままでしょうか...
> > 
> > 
> > 
> > > ## Rich Olson
> > > 
> > > ええ、トレーニングの20%で検証したところ、次のようになりました。
> > > 
> > > 対数損失: 1.0217662463425792
> > > 
> > > 精度: 0.48329853862212946
> > > 
> > > LBスコアが少し低いことを考えると、せいぜい40代前半でしょう。
> > > 
> > > トレーニングデータの量も影響しているようなので、もっと大量のトレーニングデータを投入すれば改善するかもしれません。（いくつかのデータセットがあります...）
> > > 
> > > 実行時間は約3時間なので、トレーニングデータを2倍にすることは可能です。ただし、速度を上げる方法についてはまだ調べていません。
> > > 
> > > 
> > > 
> > > ## Gaurav Rawat
> > > 
> > > 損失曲線はどうなっていますか？収束せずに変動しているように見えます。また、精度が得られたのは、初期の段階ですか、それとも後のエポックですか？私の場合、精度も変動しているようです。
> > > 
> > > 
> > > 
> > > ## Rich Olson
> > > 
> > > DeBERTaを使用する別のノートブックでは、LGBMのイテレータを1000まで増やしましたが、損失は依然としてゆっくりと減少しているようです...（そしてLBスコアも改善しています...）
> > > 
> > > [https://www.kaggle.com/code/richolson/deberta-tf-idf-word2vec-length](https://www.kaggle.com/code/richolson/deberta-tf-idf-word2vec-length) （前回のランではLB 1.011）
> > > 
> > > このノートブックには、TF-IDF、Word2Vec、長さの機能を追加したので、何が起こっているのかはわかりません... DeBERTaの埋め込みを最大限に活用するには、LGBMよりも何か別のものを使用する必要があるのかもしれません...
> > > 
> > > 
> > > 
---
> ## Huang Jing Stark
> 
> 私も同じ問題に直面しています。eval_lossが減少していません。
> 
> 
> 
---
> ## Valentin Wernerトピック作成者
> 
> 気になった方のためにコードを載せておきます。
> 
> 設定:
> 
> ```
> class CFG:
>     model = "microsoft/deberta-v3-small"
>     add_tokens = ["<[PROMPT]>","<[RESP_A]>","<[RESP_B]>","<[...]>","\n"]
>     output_dir="."
>     learning_rate=2e-5
>     per_device_train_batch_size=2
>     per_device_eval_batch_size=2
>     num_train_epochs=2
>     weight_decay=0.01
>     evaluation_strategy="epoch"
>     save_strategy="epoch"
>     max_length=2048
>     warmup_ratio=0.1
>     fp16=True
> 
> ```
> 
> トークナイザー（新しいトークンなしでも試しましたが、結果は同じでした）
> 
> ```
> # トークナイザーの準備
> tokenizer = AutoTokenizer.from_pretrained(CFG.model)
> 
> new_tokens = set(CFG.add_tokens) - set(tokenizer.vocab.keys())
> tokenizer.add_tokens(list(new_tokens))
> 
> def tokenize(examples):
>     """huggingface datasetsで使用"""
>     return tokenizer(
>         examples["train_input"], 
>         truncation=True,
>         max_length=CFG.max_length
>     )
> 
> data_collator = DataCollatorWithPadding(tokenizer=tokenizer)
> 
> [... データセットの準備 ...]
> 
> ```
> 
> モデルの読み込み（num_labelsなしでも試しましたが、結果は同じでした）
> 
> ```
> # モデルの初期化
> model = AutoModelForSequenceClassification.from_pretrained(
>     CFG.model,
>     num_labels=3
> )
> model.resize_token_embeddings(len(tokenizer))
> 
> ```
> 
> 使用されているメトリック:
> 
> ```
> accuracy = evaluate.load("accuracy")
> 
> def compute_metrics(eval_pred):
>     predictions, labels = eval_pred
>     predictions = np.argmax(predictions, axis=1)
>     return accuracy.compute(predictions=predictions, references=labels)
> 
> ```
> 
> トレーニング:
> 
> ```
> training_args = TrainingArguments(
>     output_dir=CFG.output_dir,
>     learning_rate=CFG.learning_rate,
>     per_device_train_batch_size=CFG.per_device_train_batch_size,
>     per_device_eval_batch_size=CFG.per_device_eval_batch_size,
>     num_train_epochs=CFG.num_train_epochs,
>     weight_decay=CFG.weight_decay,
>     evaluation_strategy=CFG.evaluation_strategy,
>     save_strategy=CFG.save_strategy,
>     fp16=CFG.fp16
> )
> 
> trainer = Trainer(
>     model=model,
>     args=training_args,
>     train_dataset=ds["train"],
>     eval_dataset=ds["test"],
>     tokenizer=tokenizer,
>     data_collator=data_collator,
>     compute_metrics=compute_metrics,
> )
> 
> trainer.train()
> 
> ```
> 
> 
> 
> > ## Ho Dinh Trieu
> > 
> > [@valentinwerner](https://www.kaggle.com/valentinwerner)さん、トレーニングは時間がかかりますか？
> > 
> > 
> > 
> > > ## Valentin Wernerトピック作成者
> > > 
> > > いいえ、トレーニングデータの10%をサンプリングし、2エポックのみトレーニングしています。KaggleのGPUで約35分かかります。
> > > 
> > > 他のノートブックでも同じ問題が発生していることに気づきました。
> > > 
> > > 
> > > 
> > > ## Gaurav Rawat
> > > 
> > > ベースラインで得られた最高の損失はどのくらいでしたか？私の場合、1を下回ることができず、収束していないようです。😀
> > > 
> > > 
> > > 
> > > ## Valentin Wernerトピック作成者
> > > 
> > > 私も同じです。タスクを言い換えてみましたが、まったく学習させることができませんでした。
> > > 
> > > 損失は1.07あたりで止まっており、これは単に分布を予測した場合と同じです。
> > > 
> > > 
> > > 
---


