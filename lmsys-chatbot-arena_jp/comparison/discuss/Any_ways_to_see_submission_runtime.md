# 要約 
このディスカッションは、Kaggleコンペティションにおける提出物の実行時間の確認方法についてです。

投稿者は、提出物の実行時間を知る方法を探しており、特にノートブックの実行時間を測定する方法について質問しています。

コメントでは、Valentin Wernerが提出物のタイムスタンプを確認する方法を説明し、提出ログが存在しない理由を説明しています。

RBは、提出物の実行時間を測定するための2つの方法を紹介しています。1つは、別のコンペティションのディスカッションへのリンクで、実行時間を測定するためのコードが提供されています。もう1つは、Kaggleのコード共有サイトへのリンクで、実行時間を測定するための別のコードが提供されています。

要約すると、このディスカッションは、Kaggleコンペティションにおける提出物の実行時間の確認方法について、具体的な方法やツールを紹介しています。


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

# Any ways to see submission runtime?

**gmin5y** *Thu Jul 25 2024 03:34:25 GMT+0900 (日本標準時)* (0 votes)

Hi, I am new to Kaggle and I am wondering if we can have access to the outputs of the notebooks we submitted for scoring (probably not?) If we couldn't access the submission logs, then how can we know how long our notebooks run? I have seen people discussing about the runtime of the notebook and I would really appreciate someone can explain how you measure the runtime of your solution on test set.

Thank you all! Best of luck for everyone in the coming 2 weeks!



---

 # Comments from other users

> ## Valentin Werner
> 
> You can hover over the "3h ago" to get an exact timestamp of submission. You cannot see exactly how long it runs, so you have to check in regularly, which is quite annoying.
> 
> Submission logs do not exist, as you could just print all the testdata etc.
> 
> 
> 
> > ## gmin5yTopic Author
> > 
> > 
> > You can hover over the "3h ago" to get an exact timestamp of submission. You cannot see exactly how long it runs, so you have to check in regularly, which is quite annoying.
> > 
> > Submission logs do not exist, as you could just print all the testdata etc.
> > 
> > Thank you so much!
> > 
> > 
> > 
> > ## RB
> > 
> > I have used  [this](https://www.kaggle.com/c/riiid-test-answer-prediction/discussion/201047) , its easy and works , you don't have to keep checking forever to measure runtime.
> > 
> > [This](https://www.kaggle.com/code/cpmpml/submission-timing) is another option.
> > 
> > 
> > 


---



</div>
<div class="column-right">

# 日本語訳

# 提出のランタイムを確認する方法について

**gmin5y** *2024年7月25日 木曜日 03:34:25 日本標準時* (0票)
Kaggle初心者です。提出したノートブックのスコア計算に使われた出力にアクセスすることは可能でしょうか？ (おそらく無理ですよね？) 提出ログにアクセスできない場合、ノートブックの実行時間を知るにはどうすればいいのでしょうか？ 他のユーザーがノートブックの実行時間について議論しているのを見かけました。自分のソリューションのテストセットでの実行時間を測定する方法を説明していただけると嬉しいです。
皆さん、ありがとうございます！ 残りの2週間、頑張ってください！
---
# 他のユーザーからのコメント
> ## Valentin Werner
> 
> 「3時間前」にカーソルを合わせると、提出の正確なタイムスタンプが表示されます。実行時間そのものは確認できないため、定期的に確認する必要があります。これはかなり面倒です。
> 
> 提出ログは存在しません。テストデータなどをすべて出力できてしまうからです。
> 
> 
> 
> > ## gmin5yトピック作成者
> > 
> > 
> > 「3時間前」にカーソルを合わせると、提出の正確なタイムスタンプが表示されます。実行時間そのものは確認できないため、定期的に確認する必要があります。これはかなり面倒です。
> > 
> > 提出ログは存在しません。テストデータなどをすべて出力できてしまうからです。
> > 
> > ありがとうございます！
> > 
> > 
> > 
> > ## RB
> > 
> > [こちら](https://www.kaggle.com/c/riiid-test-answer-prediction/discussion/201047) を使いました。簡単で動作します。実行時間を測定するために、ずっと確認し続ける必要はありません。
> > 
> > [こちら](https://www.kaggle.com/code/cpmpml/submission-timing) も別の選択肢です。
> > 
> > 
> > 
---



</div>