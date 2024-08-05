# 要約 
このディスカッションは、KaggleのLMSYS - Chatbot Arena Human Preference Predictionsコンペティションのテストデータセットに関するものです。参加者は、テストデータセットの性質、特にトレーニングデータセットとの違いについて質問しています。

主なポイントは以下の通りです。

* **テストデータセットのサイズ:** テストデータセットは約25,000行あり、そのうち約26%（約6,500行）がパブリックリーダーボードに使用されます。
* **トレーニングデータセットとの違い:** トレーニングデータセットには、最近リリースされたモデル（例：Llama 3）が含まれていません。そのため、テストデータセットには異なるLLMからのメッセージが含まれている可能性があります。
* **データ分割:** テストデータセットは、各比較が行われた日付に基づいて分割されている可能性があります。
* **パブリックリーダーボードの信頼性:** パブリックリーダーボードは、テストデータセット全体の約26%のみを使用しているため、信頼性に欠ける可能性があります。
* **過剰適合:** パブリックリーダーボードに過剰適合すると、プライベートリーダーボードでのスコアが低くなる可能性があります。

このディスカッションは、参加者がテストデータセットの性質を理解し、過剰適合を避けるための戦略を立てるのに役立ちます。


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

# More information on test dataset

**Matous Famera** *Thu Jun 13 2024 02:12:49 GMT+0900 (日本標準時)* (1 votes)

Hello, I have a few questions regarding the nature of test dataset.

I already know that 26% of the entire test dataset is used for public leaderboard and 74% is used for private leaderboard.

What is the difference between the train dataset and test dataset? Are the same LLMs used? Was the same dataset used for train dataset and test dataset?
How long is the test dataset? Or atleast how long compared to the train dataset is the test dataset?

Thanks if any of these questions can be answered



---

 # Comments from other users

> ## James Day
> 
> 
> What is the difference between the train dataset and test dataset? Are the same LLMs used? Was the same dataset used for train dataset and test dataset?
> 
> I've noticed there aren't any recently released models (e.g. Llama 3) in the training dataset, so I have a suspicion they split their data based on the date on which each comparison occurred and I would expect to receive messages from different LLMs during testing.
> 
> How long is the test dataset? Or atleast how long compared to the train dataset is the test dataset?
> 
> The data tab says "you can expect roughly 25,000 rows in the test set"
> 
> 
> 
> > ## Matous FameraTopic Author
> > 
> > 
> > There are 55K rows in the training data, and you can expect roughly 25,000 rows in the test set.
> > 
> > Does it mean that the entire test dataset has 25k rows or just the public leaderboard part?
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > The entire data has 25k rows, ~26% of them is public leaderboard (so about 6.5k rows).
> > > 
> > > As you probably guess, this makes trusting the public leaderboard score similar to trusting a single validation fold in a 4-fold cv setup. Thats why it is often recommended to build a good CV strategy and try to create a correlation between the CV score (which should be reliable) and the public LB score.
> > > 
> > > Also note, that the final score is ONLY the private LB, so the other 74% of the data. Meaning the fold, you may overfit on (the public LB) is NOT part of your winning score. This can lead to what we call "Leaderboard shakeup". These concepts apply to basically all kaggle competitions.
> > > 
> > > 
> > > 
> > > ## Matous FameraTopic Author
> > > 
> > > Thanks for clarification. I was asking that questions, because the length of the test dataset is related to variance and reliability of the score.
> > > 
> > > I'm aware of the concept of overfitting for public leaderboard.
> > > 
> > > 
> > > 


---



</div>
<div class="column-right">

# 日本語訳

# テストデータセットに関する詳細情報

**Matous Famera** *2024年6月13日 木曜日 02:12:49 GMT+0900 (日本標準時)* (1票)
こんにちは。テストデータセットの性質についていくつか質問があります。

テストデータセット全体の26%がパブリックリーダーボードに使用され、74%がプライベートリーダーボードに使用されることはすでに知っています。

トレーニングデータセットとテストデータセットの違いは何ですか？同じLLMが使用されていますか？トレーニングデータセットとテストデータセットには同じデータセットが使用されましたか？

テストデータセットの長さはどのくらいですか？あるいは、少なくともトレーニングデータセットと比較してテストデータセットの長さはどのくらいですか？

これらの質問のいずれかに回答していただければ幸いです。

---
# 他のユーザーからのコメント

> ## James Day
> 
> 
> トレーニングデータセットとテストデータセットの違いは何ですか？同じLLMが使用されていますか？トレーニングデータセットとテストデータセットには同じデータセットが使用されましたか？
> 
> トレーニングデータセットには、最近リリースされたモデル（例：Llama 3）が含まれていないことに気づきました。そのため、私は彼らが各比較が行われた日付に基づいてデータを分割したのではないかと疑っています。そして、テスト中は異なるLLMからのメッセージを受け取ると予想しています。
> 
> テストデータセットの長さはどのくらいですか？あるいは、少なくともトレーニングデータセットと比較してテストデータセットの長さはどのくらいですか？
> 
> データタブには、「テストセットには約25,000行が含まれると予想されます」と記載されています。
> 
> 
> 
> > ## Matous Fameraトピック作成者
> > 
> > 
> > トレーニングデータには55,000行あり、テストセットには約25,000行が含まれると予想されます。
> > 
> > これは、テストデータセット全体に25,000行あるのか、それともパブリックリーダーボード部分のみを指すのでしょうか？
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > データ全体には25,000行あり、その約26%がパブリックリーダーボードです（つまり約6,500行）。
> > > 
> > > おそらくお気づきでしょうが、これはパブリックリーダーボードのスコアを信頼することは、4分割交差検証設定における単一の検証フォールドを信頼することと似ています。そのため、多くの場合、優れた交差検証戦略を構築し、交差検証スコア（信頼できるはずです）とパブリックLBスコアとの相関関係を作成することをお勧めします。
> > > 
> > > また、最終スコアはプライベートLBのみであることに注意してください。つまり、データの残りの74%です。つまり、過剰適合する可能性のあるフォールド（パブリックLB）は、あなたの勝利スコアには含まれません。これは、「リーダーボードのシャッフル」と呼ばれる現象につながる可能性があります。これらの概念は、基本的にすべてのKaggleコンペティションに適用されます。
> > > 
> > > 
> > > 
> > > ## Matous Fameraトピック作成者
> > > 
> > > 説明ありがとうございます。テストデータセットの長さは、スコアの分散と信頼性に関連しているため、これらの質問をしました。
> > > 
> > > パブリックリーダーボードに対する過剰適合の概念は理解しています。
> > > 
> > > 
> > > 
---



</div>