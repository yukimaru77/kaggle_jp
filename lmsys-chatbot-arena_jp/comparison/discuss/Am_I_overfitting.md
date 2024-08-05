# 要約 
このディスカッションは、Kaggleコンペティション参加者であるKeShuang Liu氏が、自身のモデルが過学習しているのではないかと懸念していることから始まりました。

Valentin Werner氏は、過学習の兆候として、トレーニング損失が低下している一方で、検証損失が頭打ちになっているか上昇している場合を挙げました。また、モデルのパフォーマンスが期待されるレベルに達していない場合も、過学習の可能性を示唆しています。

KeShuang Liu氏は、検証セットの計算に時間がかかるため、過学習の判断に時間がかかっていることを説明しました。Valentin Werner氏は、検証を定期的に行うことで、過学習を早期に検出できることを提案しました。

xiaotingting氏は、検証セットの指標とトレーニングセットの指標を比較することで、過学習を判断できることを指摘しました。また、過学習を防ぐために、ウェイト減衰などの正則化を追加することを提案しました。

KeShuang Liu氏は、検証指標が数時間後に計算されるため、トレーニングを中止するかどうか検討していることを明らかにしました。

Rise_Hand氏は、KeShuang Liu氏が600エポックまでトレーニングを行っていることに驚き、モデルの種類について質問しました。

AYUSH KHAIRE氏は、KeShuang Liu氏のモデルが約580から600エポックで過学習している可能性を示唆しました。

最終的に、KeShuang Liu氏は、モデルが過学習している可能性が高いことから、トレーニングを中止する必要があると結論付けました。

このディスカッションは、過学習の兆候、過学習の判断方法、過学習を防ぐための対策について、有益な情報を提供しています。


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

# Am I overfitting?

**KeShuang Liu** *Sat Jul 27 2024 12:07:19 GMT+0900 (日本標準時)* (1 votes)





---

 # Comments from other users

> ## Valentin Werner
> 
> Overfitting is best analyzed in combination with validation loss. If you validation loss has a similar drop to your training loss (which I guess would win the competition at these scores), you are not overfitting. In general, if training loss goes down while validation loss is either plateauing or going back up, you are likely overfitting.
> 
> Another way of estimating overfitting is to look at what performance you expect and what you see on the train loss. We would not expect the model to go to .800 or even below it - therefore, it is likely to overfit. However, this does not mean that the model was best before this downward shift at steps 550 - you should use a validation score to evaluate how well the model predicts on unseen data
> 
> 
> 
> > ## KeShuang LiuTopic Author
> > 
> > Yes, but my validation set can only be calculated after this epoch is completed, and it takes a long time, so I am considering whether to stop it directly
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > You can set how often you want to evaluate. It does indeed take a lot of time, so I think evaluating 2-4 times is feasible.
> > > 
> > > 
> > > 
> > > ## KeShuang LiuTopic Author
> > > 
> > > Yes, my model should be overfitting. Its loss on the validation set is 0.99
> > > 
> > > 
> > > 


---

> ## xiaotingting
> 
> It has to be combined with the indicators of the validation set. If the loss on the validation set is large, but very low on the training set, it is overfitting, and you can consider adding regularization such as weight decay. If the loss on both the validation set and the training set is low, it means the model is effective.
> 
> 
> 
> > ## KeShuang LiuTopic Author
> > 
> > The next validation metric will be calculated in a few hours, and I am considering whether to abandon this training directly
> > 
> > 
> > 


---

> ## Rise_Hand
> 
> Wow so Crazy! 600 epochs !!! Which kind of model you are using 
> 
> 
> 
> > ## KeShuang LiuTopic Author
> > 
> > steps,haha
> > 
> > 
> > 


---

> ## AYUSH KHAIRE
> 
> [@liukeshuang](https://www.kaggle.com/liukeshuang) yes about 580 to 600 you are overfitting. 
> 
> 
> 
> > ## KeShuang LiuTopic Author
> > 
> > Then I probably don't need to continue training now
> > 
> > 
> > 


---



</div>
<div class="column-right">

# 日本語訳

# 過学習している？
**KeShuang Liu** *2024年7月27日土曜日 12:07:19 GMT+0900 (日本標準時)* (1票)
---
# 他のユーザーからのコメント
> ## Valentin Werner
> 
> 過学習は、検証損失と合わせて分析するのが最適です。検証損失がトレーニング損失と同様に低下している場合（このスコアでコンペティションに勝つ可能性が高いと思いますが）、過学習していません。一般的に、トレーニング損失が低下している一方で、検証損失が頭打ちになっているか上昇している場合は、過学習している可能性があります。
> 
> 過学習を推定するもう1つの方法は、期待されるパフォーマンスとトレーニング損失で観察されるパフォーマンスを比較することです。モデルが0.800まで、またはそれ以下にまで低下することは期待できません。そのため、過学習している可能性があります。ただし、これはステップ550でのこの下降シフトの前にモデルが最適であったことを意味するわけではありません。検証スコアを使用して、モデルが未知のデータに対してどの程度うまく予測できるかを評価する必要があります。
> 
> 
> 
> > ## KeShuang Liuトピック作成者
> > 
> > はい、しかし私の検証セットは、このエポックが完了した後にしか計算できず、時間がかかるため、直接停止するかどうか検討しています。
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > 評価する頻度を設定できます。確かに時間がかかりますので、2〜4回評価するのが現実的だと思います。
> > > 
> > > 
> > > 
> > > ## KeShuang Liuトピック作成者
> > > 
> > > はい、私のモデルは過学習しているはずです。検証セットでの損失は0.99です。
> > > 
> > > 
> > > 
---
> ## xiaotingting
> 
> 検証セットの指標と組み合わせる必要があります。検証セットでの損失が大きく、トレーニングセットでの損失が非常に小さい場合は、過学習しています。ウェイト減衰などの正則化を追加することを検討できます。検証セットとトレーニングセットの両方での損失が小さい場合は、モデルが効果的であることを意味します。
> 
> 
> 
> > ## KeShuang Liuトピック作成者
> > 
> > 次の検証指標は数時間後に計算されます。このトレーニングを直接放棄するかどうか検討しています。
> > 
> > 
> > 
---
> ## Rise_Hand
> 
> わあ、すごい！600エポック！！どんなモデルを使っているのですか？
> 
> 
> 
> > ## KeShuang Liuトピック作成者
> > 
> > ステップ、はは
> > 
> > 
> > 
---
> ## AYUSH KHAIRE
> 
> [@liukeshuang](https://www.kaggle.com/liukeshuang) はい、約580から600で過学習しています。
> 
> 
> 
> > ## KeShuang Liuトピック作成者
> > 
> > それでは、おそらく今はトレーニングを続ける必要はありません。
> > 
> > 
> > 
---



</div>