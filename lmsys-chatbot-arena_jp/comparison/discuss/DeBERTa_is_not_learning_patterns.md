# 要約 
このKaggleコンペティションのディスカッションは、DeBERTaモデルがチャットボットの好み予測タスクでうまく学習できていないという問題について議論しています。

**Valentin Werner**は、モデルが常に最も頻繁なラベルを予測し、学習していないことに気づき、同じような経験をした人がいるかどうか尋ねています。

**Rich Olson**は、同じ問題に遭遇し、より多くのデータでトレーニングすることで解決したと答えています。彼は、小さなサブセットでトレーニングしたときはうまくいかなかったが、すべてのデータでトレーニングした後、リーダーボードスコアが1.030に改善したと述べています。しかし、精度は40代前半にとどまり、トレーニングデータの量の影響を受けている可能性があるとも指摘しています。

**Gaurav Rawat**は、損失曲線と精度の変動について質問し、Rich Olsonは、LGBMのイテレータを増やしても損失がゆっくりとしか減少していないと答えています。彼は、DeBERTaの埋め込みを最大限に活用するには、LGBMよりも別のモデルが必要になるかもしれないと考えています。

**Huang Jing Stark**も、評価損失が減少していないという同じ問題に直面しています。

**Valentin Werner**は、自分のコードを共有し、設定、トークナイザー、モデルの読み込み、メトリック、トレーニングの詳細を説明しています。彼は、トレーニングデータの10%をサンプリングし、2エポックのみトレーニングしているため、トレーニング時間は約35分であると述べています。

**Ho Dinh Trieu**は、トレーニング時間がかかるかどうか尋ね、Valentin Wernerは、トレーニングデータの10%をサンプリングし、2エポックのみトレーニングしているため、トレーニング時間は約35分であると答えています。

**Gaurav Rawat**は、ベースラインで得られた最高の損失について質問し、Valentin Wernerは、損失が1.07あたりで止まっており、これは単に分布を予測した場合と同じであると答えています。

このディスカッションから、DeBERTaモデルがチャットボットの好み予測タスクでうまく学習できていないという問題が、多くの参加者に見られることがわかります。解決策としては、より多くのデータでトレーニングすることや、LGBMよりも別のモデルを使用することが考えられます。


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

# DeBERTa is not learning patterns?

**Valentin Werner** *Mon May 06 2024 18:08:22 GMT+0900 (日本標準時)* (6 votes)

Hello everybody - I am currently facing the issue that my starter notebook always predicts label 0 (which is most prevalent in the subset of the dataset that I am using).

I did not have this experience in the past, where even though labels are balanced, the model is not learning.

Did you experience the same and were you able to solve it?



---

 # Comments from other users

> ## Rich Olson
> 
> I had the same experience with deberta:
> 
> [https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/501848](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/501848)
> 
> Short version: Things didn't converge for me until I started training with more data.  
> 
> Definitely had that "huh - this isn't work" feeling training on a small subset.  Got LB 1.030 after training on all the data.
> 
> Notebook here:
> 
> [https://www.kaggle.com/code/richolson/deberta](https://www.kaggle.com/code/richolson/deberta) (copy and paste as you please)
> 
> 
> 
> > ## Valentin WernerTopic Author
> > 
> > Interesting! 1.030 is definetly an improvement, did you also evaluate accuracy? wondering whether it is still in the 30s/40s..
> > 
> > 
> > 
> > > ## Rich Olson
> > > 
> > > Well - my validation on 20% of train is:
> > > 
> > > Log Loss: 1.0217662463425792
> > > 
> > > Accuracy: 0.48329853862212946
> > > 
> > > Considering my LB score is a little lower - I'd guess mid 40s at best.
> > > 
> > > Since the amount of train data seems to be a factor - wondering if tossing a bunch more train at it might help. (there are some datasets…)
> > > 
> > > Considering run-time is about 3 hours - could maybe double the train data.  I haven't really looked at if I can do anything to speed things up yet though.
> > > 
> > > 
> > > 
> > > ## Gaurav Rawat
> > > 
> > > Nice how do the loss curves look they seems to be like fluctuating with no end . Also the accuracy you got at what step earlier or later epochs . As I see that also fluctuates 
> > > 
> > > 
> > > 
> > > ## Rich Olson
> > > 
> > > so - in another notebook that uses deberta - I've gone up to 1000 LGBM iterators - and it still seems like loss is slowly falling… (and LB score improving…)
> > > 
> > > [https://www.kaggle.com/code/richolson/deberta-tf-idf-word2vec-length](https://www.kaggle.com/code/richolson/deberta-tf-idf-word2vec-length) (LB 1.011 on last run)
> > > 
> > > I've added tf-idf, word2vec and length features in that one - so hard to say what's going on…  taking it as a suggestion I may need to use something more than LGBM to fully use the deberta embeddings…
> > > 
> > > 
> > > 


---

> ## Huang Jing Stark
> 
> Facing same issue here, my eval_loss is not decreasing 
> 
> 
> 


---

> ## Valentin WernerTopic Author
> 
> Code in case you care
> 
> Config:
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
> Tokenizer (note that I also tried without new tokens and got same result)
> 
> ```
> # Prepare Tokenizer
> tokenizer = AutoTokenizer.from_pretrained(CFG.model)
> 
> new_tokens = set(CFG.add_tokens) - set(tokenizer.vocab.keys())
> tokenizer.add_tokens(list(new_tokens))
> 
> def tokenize(examples):
>     """use with huggingface datasets"""
>     return tokenizer(
>         examples["train_input"], 
>         truncation=True,
>         max_length=CFG.max_length
>     )
> 
> data_collator = DataCollatorWithPadding(tokenizer=tokenizer)
> 
> [... dataset preparation ...]
> 
> ```
> 
> Model loading (note that I also tried without num_labels and got same result):
> 
> ```
> # Initialize model
> model = AutoModelForSequenceClassification.from_pretrained(
>     CFG.model,
>     num_labels=3
> )
> model.resize_token_embeddings(len(tokenizer))
> 
> ```
> 
> Metric used:
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
> Training:
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
> > hi [@valentinwerner](https://www.kaggle.com/valentinwerner),does the train takes long? 
> > 
> > 
> > 
> > > ## Valentin WernerTopic Author
> > > 
> > > No, I sample 10% of the training data and only train 2 epochs. Takes about 35 min on kaggle GPU.
> > > 
> > > I also noticed that other notebooks have the same issue.
> > > 
> > > 
> > > 
> > > ## Gaurav Rawat
> > > 
> > > What was the best loss you got from the baseline not getting it past 1 right now and seems not converging at this moment for me . 😀 
> > > 
> > > 
> > > 
> > > ## Valentin WernerTopic Author
> > > 
> > > Same for me, I also tried rephrasing the task but cannot make it lear at all.
> > > 
> > > Loss is stuck at 1.07 or so; which is what you get when you just predict the distribution
> > > 
> > > 
> > > 


---



</div>
<div class="column-right">

# 日本語訳

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




</div>