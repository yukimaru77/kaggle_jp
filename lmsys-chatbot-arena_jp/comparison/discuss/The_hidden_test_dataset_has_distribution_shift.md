# 要約 
このディスカッションは、Kaggleコンペティション参加者が、トレーニングデータと隠されたテストデータの間に分布シフトがあるのではないかと疑っていることから始まります。参加者は、Gemmaモデルをトレーニングデータで1エポックだけトレーニングしたところ、ローカル評価では良い結果が出ましたが、リーダーボードではスコアが低くなったと報告しています。

他の参加者は、この現象はモデルがトレーニングデータに過剰適合しているためであり、検証データセットを使用せずにトレーニングデータ全体でモデルを評価したことが原因であると指摘しています。

参加者は、トレーニングデータとテストデータの分布が異なる可能性があることを認識し、その原因として、トークン化されたデータやテキストの最初の部分だけを抽出したことが挙げられています。

このディスカッションは、機械学習モデルのトレーニングと評価における重要な概念である、過剰適合とデータリークについて説明しています。参加者は、モデルを評価するために検証データセットを使用することの重要性を学び、トレーニングデータとテストデータの分布の違いを考慮する必要があることを理解しました。


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

# The hidden test dataset has distribution shift 

**Xin** *Sat Aug 03 2024 02:30:10 GMT+0900 (日本標準時)* (-11 votes)



After extracting some features from training dataset, then a full dataset one epoch train, I thought the single Gemma model can have a good leaderboard result, but the reality is eval:0.867 leaderboard: 0.933.

I think it might mean the data distribution is to some extent different than the train dataset, then after I extracting features from test dataset, the score then be low.



---

 # Comments from other users

> ## CPMP
> 
> What you see is that your model performs better on its training data than on new data. This is to be expected.
> 
> One way to not be surprised  is to split your triaining data into two piece. One piece you use for training, and one piece you use for evaluating your model once trained. The second piece is often called a validation dataset, or a test dataset.
> 
> 
> 


---

> ## Valentin Werner
> 
> You are facing a lot of backlash for a "beginner mistake" - even if only training for one epoch, you want to validate your model on unseen data, your model has theen the "validation" data already once, so it knows it. This is one form of data leakage.
> 
> Just from this training it is impossible to expect how well your model is going to perform on a leaderboard submission. Often, it is better to set aside 10-20% of data to make sure you have a local validation and a leaderboard score rather then fitting your model on all the data.
> 
> It is possible to probe the data distribution of the LB dataset, however, not with this approach. 
> 
> 
> 
> > ## XinTopic Author
> > 
> > Yeah. I understand. One epoch also probably brings model to an underfit status. From the result, I intuitively think that either the distribution between train and hidden test dataset different or there is a high similarity on train dataset (I mean tokenized data, maybe also because I only extract the first part from texts) which causes such an obvious overfit. 
> > 
> > 
> > 


---

> ## JM
> 
> Your eval_dataset is taking a subset of your training dataset…
> 
> 
> 
> > ## XinTopic Author
> > 
> > Yeah. But I think one epoch, the model only see the data once.
> > 
> > 
> > 
> > > ## David.Ricardo.H.X
> > > 
> > > You didnt get what he means…… 
> > > 
> > > Your eval_dataset is taking a subset of your training dataset… 
> > > 
> > > Do you have a concept of what is the difference between train set, validation set and test?
> > > 
> > > 
> > > 


---



</div>
<div class="column-right">

# 日本語訳

# 隠されたテストデータセットに分布シフトがある

**Xin** *2024年8月3日土曜日 02:30:10 GMT+0900 (日本標準時)* (-11 votes)
トレーニングデータセットからいくつかの特徴量を抽出し、その後、全データセットで1エポックのトレーニングを行ったところ、Gemmaモデル単体でリーダーボードで良い結果が得られると思いましたが、実際には評価値は0.867、リーダーボードは0.933でした。
これは、データの分布がトレーニングデータセットとはある程度異なることを意味しているのではないかと考えられます。その後、テストデータセットから特徴量を抽出したところ、スコアが低くなりました。
---
# 他のユーザーからのコメント
> ## CPMP
> 
> あなたが見ているのは、モデルが新しいデータよりもトレーニングデータでより良いパフォーマンスを発揮しているということです。これは予想されることです。
> 
> 驚かないようにするには、トレーニングデータを2つに分割します。1つはトレーニングに使用し、もう1つはトレーニング後にモデルの評価に使用します。2番目の部分は、しばしば検証データセットまたはテストデータセットと呼ばれます。
> 
> 
> 
---
> ## Valentin Werner
> 
> あなたは「初心者向けのミス」で多くの反発を受けています。たとえ1エポックしかトレーニングしていなくても、モデルを未知のデータで検証する必要があります。モデルはすでに「検証」データを見たことがあるので、それを知っています。これはデータリークの一種です。
> 
> このトレーニングだけでは、モデルがリーダーボード提出でどの程度のパフォーマンスを発揮するかを予測することはできません。多くの場合、ローカル検証とリーダーボードスコアを得るために、データの10〜20％を別に設定しておく方が良いでしょう。
> 
> リーダーボードデータセットのデータ分布を調べることは可能ですが、このアプローチではできません。
> 
> 
> 
> > ## XinTopic Author
> > 
> > はい、理解しました。1エポックでも、モデルはデータを見たことがない状態になる可能性があります。結果から、トレーニングデータセットと隠されたテストデータセットの分布が異なるか、トレーニングデータセット（トークン化されたデータ、おそらくテキストの最初の部分だけを抽出したため）に高い類似性があり、このような明らかな過剰適合を引き起こしているのではないかと直感的に考えています。
> > 
> > 
> > 
---
> ## JM
> 
> あなたのeval_datasetは、トレーニングデータセットのサブセットを使用しています…
> 
> 
> 
> > ## XinTopic Author
> > 
> > はい。しかし、1エポックでは、モデルはデータを見たことが1回だけです。
> > 
> > 
> > 
> > > ## David.Ricardo.H.X
> > > 
> > > 彼の言っていることが理解できていません…
> > > 
> > > あなたのeval_datasetは、トレーニングデータセットのサブセットを使用しています…
> > > 
> > > トレーニングセット、検証セット、テストセットの違いを理解していますか？
> > > 
> > > 
> > > 
---



</div>