# 要約 
このディスカッションは、コンペティションのテストデータの行数に関する質問と回答についてです。

Gabriel Mireaさんは、コンペティションの説明とリーダーボードの情報が矛盾しているように感じ、テストデータの行数が合計で75,000行あるのかどうかを質問しました。

RBさんは、テストデータは合計で25,000行あり、パブリックリーダーボードは26%のデータ（6,500行）で計算され、プライベートリーダーボードは残りの74%のデータ（18,500行）で計算されることを説明しました。

Gabriel Mireaさんは、RBさんの説明で疑問が解消され、提出物がリーダーボードでスコアを獲得した場合、すべてのサンプルを処理したことになることを理解しました。また、プライベートリーダーボードのスコアが隠されているのは、参加者が探りを入れないようにするためであることも理解しました。

このディスカッションは、コンペティションのデータに関する重要な情報を明らかにし、参加者が提出を行う際に必要な情報を理解するのに役立ちます。


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

# Clarification on the number of chats that need to be processed

**Gabriel Mirea** *Thu Jul 04 2024 21:04:10 GMT+0900 (日本標準時)* (0 votes)

Hi,

The dataset description says 

When your submission is scored, this example test data will be replaced with the full test set. There are 55K rows in the training data, and you can expect roughly 25,000 rows in the test set.

and the leaderboard says

This leaderboard is calculated with approximately 26% of the test data. The final results will be based on the other 74%,

So should we expect that the final submission on the private leaderboard will need to process ~75.000 rows?



---

 # Comments from other users

> ## RB
> 
> 
> So should we expect that the final submission on the private leaderboard will need to process ~75.000 rows?
> 
> No, total 25000 samples 
> 
> Public LB - 26% => 6500 Samples
> 
> Private LB - 74% => 18500 Samples
> 
> Total Test Set = 25000
> 
> When you make a submission, your code is doing inference for all 25000 samples, we only see public LB with 6500 samples, remaining after competition ends
> 
> 
> 
> > ## Gabriel MireaTopic Author
> > 
> > Thanks! That makes sense, so if the submission scores on the LB it got through all the samples. And the final score is hidden so that people don't probe, I guess?
> > 
> > My main concern was if the notebook will have to deal with more samples later. That's clear now, thank you again.
> > 
> > 
> > 


---



</div>
<div class="column-right">

# 日本語訳

# テストデータの行数に関する確認

**Gabriel Mirea** *木曜日 7月 4日 2024 21:04:10 GMT+0900 (日本標準時)* (0 票)

こんにちは。

データセットの説明には以下のように書かれています。

> 提出物が採点されるとき、このテストデータの例は完全なテストセットに置き換えられます。トレーニングデータには55,000行あり、テストセットには約25,000行あると予想されます。

そして、リーダーボードには以下のように書かれています。

> このリーダーボードは約26%のテストデータで計算されています。最終結果は残りの74%に基づいて算出されます。

つまり、プライベートリーダーボードでの最終提出では、約75,000行を処理する必要があるのでしょうか？

---

# 他のユーザーからのコメント

> ## RB
> 
> 
> つまり、プライベートリーダーボードでの最終提出では、約75,000行を処理する必要があるのでしょうか？
> 
> いいえ、合計25,000サンプルです。
> 
> パブリックLB - 26% => 6,500サンプル
> 
> プライベートLB - 74% => 18,500サンプル
> 
> テストセット合計 = 25,000
> 
> 提出を行うと、コードは25,000サンプルすべてに対して推論を実行します。私たちは6,500サンプルのパブリックLBしか見ることができません。残りはコンテスト終了後に公開されます。
> 
> 
> 
> > ## Gabriel Mireaトピック作成者
> > 
> > ありがとうございます！ 理解できました。つまり、提出物がLBでスコアを獲得した場合、すべてのサンプルを処理したということですね。そして、最終スコアは隠されているので、人々が探りを入れないようにしているのでしょうか？
> > 
> > 私の主な懸念は、ノートブックが後でより多くのサンプルを処理する必要があるかどうかでした。それが明確になりました。改めてありがとうございます。
> > 
> > 
> > 
---



</div>