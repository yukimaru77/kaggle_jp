# 要約 
## コンペティションディスカッション要約

このディスカッションは、KaggleのLMSYS - Chatbot Arena 人間による好み予測チャレンジにおけるDebertaベースラインモデルに関するものです。

**Fritz Cremer**は、Deberta-v3-baseを使った簡単なベースラインモデルを作成し、そのコードを共有しました。このモデルは、トレーニングデータの一部しか使用しておらず、スコアも良くありません。しかし、Debertaを使った提出コードの例として役立ちます。

Cremerは、モデルの改善点として、以下の点を挙げています。

- 全てのデータを使用する
- K-Fold交差検証
- 応答を交換してデータを増やす
- 損失関数を変更する

特に、損失関数の変更は重要であり、2段階モデルにするのが良いかもしれません。

**Nicholas Broad**は、このベースラインモデルは基本的にランダムな推測であり、スコアはランダムな予測とほぼ同じであると指摘しました。

**Valentin Werner**は、モデルがデータから学習できていない可能性があると指摘しました。

**Fritz Cremer**は、BroadとWernerの指摘に同意し、モデルのトレーニングが不安定であることを認めました。一部の実行では、モデルはラベルの分布以上のものを学習しましたが、他の実行では完全に失敗しました。しかし、これは調整されていない最初の日の簡単なアプローチであると強調しました。

**要約:**

このディスカッションは、Debertaベースラインモデルの限界と改善点について議論しています。モデルは、トレーニングデータの一部しか使用しておらず、スコアも良くありません。また、トレーニングが不安定で、データから学習できていない可能性があります。しかし、これは最初の日の簡単なアプローチであり、改善の余地があります。


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

# Deberta Baseline - LB 1.075

**Fritz Cremer** *Fri May 03 2024 21:45:56 GMT+0900 (日本標準時)* (5 votes)

I made a very quick deberta-v3-base baseline:

[https://www.kaggle.com/code/fritzcremer/lmsys-deberta-v3-base-baseline/notebook](https://www.kaggle.com/code/fritzcremer/lmsys-deberta-v3-base-baseline/notebook)

Currently, it only uses a small fraction of the train data and doesn't get a great score. But this is how the code for a deberta submission could look like.

Possible improvements:

- Utilize all data

- K Fold cross-validation

- Swap the responses for more data

- Formulate the loss differently

Especially the last one. I think it could make sense to have a two stage model. In the first stage, just predict if a response won a duel or not (without providing the other response), in the second stage, using two such predictions + hand crafted features to predict the better response. I think this looks like a very interesting competition, with not one straight forward path.

Let me know what you think!



---

 # Comments from other users

> ## Nicholas Broad
> 
> Just so you know, this is basically just random guessing.
> 
> ```
> from sklearn.metrics import log_loss
> log_loss([1], [[1/3, 1/3, 1/3]], labels=[0,1,2])
> 
> # 1.0986122886681098
> 
> ```
> 
> 
> 
> > ## Valentin Werner
> > 
> > The Notebook exactly replicates the label distribution. It seems that a basic starter with huggingface Trainer is not able to learn from the data.
> > 
> > 
> > 
> > ## Fritz CremerTopic Author
> > 
> > [@nbroad](https://www.kaggle.com/nbroad) Yes, I know. It was more like a general setup to fit a model for this task with huggingface. I found that the training was very unstable, on some runs the model learned more than just the label distribution (e.g. on LB the notebook has 1.075 with the submitted version), and on others it failed completely. But then again, it is not a well tuned approach at all, just a quick first day approach 😄
> > 
> > 
> > 


---



</div>
<div class="column-right">

# 日本語訳

# Deberta ベースライン - LB 1.075
**Fritz Cremer** *2024年5月3日 金曜日 21:45:56 GMT+0900 (日本標準時)* (5 votes)

Deberta-v3-base を使った非常に簡単なベースラインを作成しました。
[https://www.kaggle.com/code/fritzcremer/lmsys-deberta-v3-base-baseline/notebook](https://www.kaggle.com/code/fritzcremer/lmsys-deberta-v3-base-baseline/notebook)

現時点では、トレーニングデータのほんの一部しか使用しておらず、スコアも良くありません。しかし、これは Deberta を使った提出コードの例です。

改善点としては、以下のようなものがあります。

- 全てのデータを使用する
- K-Fold 交差検証
- 応答を交換してデータを増やす
- 損失関数を変更する

特に最後の項目は重要です。2段階モデルにするのが良いかもしれません。最初の段階では、応答がデュエルで勝ったかどうかを予測するだけ（もう一方の応答は提供しない）、2段階目では、そのような予測を2つと手作業で作成した特徴量を使って、より良い応答を予測します。これは非常に興味深いコンペティションで、明確な道筋がないように思えます。

ご意見をお聞かせください！

---
# 他のユーザーからのコメント
> ## Nicholas Broad
> 
> ご存知かもしれませんが、これは基本的にランダムな推測です。
> 
> ```
> from sklearn.metrics import log_loss
> log_loss([1], [[1/3, 1/3, 1/3]], labels=[0,1,2])
> 
> # 1.0986122886681098
> 
> ```
> 
> 
> 
> > ## Valentin Werner
> > 
> > ノートブックはラベルの分布を正確に複製しています。Huggingface Trainer を使った基本的なスターターでは、データから学習できないようです。
> > 
> > 
> > 
> > ## Fritz Cremerトピック作成者
> > 
> > [@nbroad](https://www.kaggle.com/nbroad) はい、知っています。これは、Huggingface でこのタスクに適したモデルを構築するための一般的な設定のようなものでした。トレーニングが非常に不安定であることがわかりました。一部の実行では、モデルはラベルの分布以上のものを学習しました（たとえば、LB では、提出されたバージョンでノートブックが 1.075 を記録しています）。しかし、他の実行では完全に失敗しました。しかし、繰り返しになりますが、これは全く調整されていないアプローチであり、最初の日の簡単なアプローチです 😄
> > 
> > 
> > 
---



</div>