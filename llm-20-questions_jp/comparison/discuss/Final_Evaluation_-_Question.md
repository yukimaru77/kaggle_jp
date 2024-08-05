# 要約 
ディスカッションの要約は以下の通りです。

参加者「vj4science」がコンペの最終評価に関する疑問を提起しました。具体的には、8月13日の提出締め切り時点でロックされる3つの提出物のスコアが606からスタートするのか、またはそれまでの実行から得られたスコアを引き継ぐのかについて質問しています。

「Mahmoud Elshahed」は、評価期間中に隠れたテストセットでゼロからスタートすべきだと主張し、そうしないと現在の公開単語リストを用いた反復的なスクリプトが高スコアを得やすくなるという懸念を表明しました。

「Chris Deotte」は、Kaggleの管理者がすでにコメントを投稿しており、現在のリーダーボードが最終評価時にエージェントの基礎となることを確認しました。また、新しい単語セットでの十分なゲームが行われるよう調整がなされるとのことです。

「vj4science」はChrisに感謝し、管理者のアプローチが理想的かどうか分からないものの、その情報が役立つことを認識しました。

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

# Final Evaluation - Question

**vj4science** *Sat Jul 27 2024 11:18:16 GMT+0900 (日本標準時)* (6 votes)

Need clarification on the below paragraph please? Does the locked 3 submissions start with a score of 600? or do they carry over previously accumulated scores from runs prior to August 13th? 

"Final Evaluation

At the submission deadline on August 13, 2024, submissions will be locked. From August 13, 2024 to August 27th, 2024 we will continue to run episodes against a new set of unpublished, secret words. During this period only your three active submissions will be eligible for the leaderboard. At the conclusion of this period, the leaderboard is final."



---

 # Comments from other users

> ## Mahmoud Elshahed
> 
> Logically, it shall start from scratch on hidden test set, 
> 
> because if not 
> 
> with the current public wordlist, you can write script for iteration instead of model building, this lead to high score, 
> 
> and low decremental score in the evaluation period will keep the user up and won easily.
> 
> "Just My Opinion" 
> 
> 
> 
> > ## sayoulala
> > 
> > Totally agree with you.
> > 
> > 
> > 


---

> ## Chris Deotte
> 
> Kaggle admin commented [here](https://www.kaggle.com/competitions/llm-20-questions/discussion/512358#2872495)
> 
> Yes, the current leaderboard will be the seed of your agent going into the final evaluation period. We will ensure that agents receive enough games for the leaderboard to stabilize under the new set of words, so even if your agent is severly under ranked it should not be an issue.
> 
> 
> 
> > ## gguillard
> > 
> > That's crazy.
> > 
> > 
> > 
> > ## vj4scienceTopic Author
> > 
> > Thank You Chris for pointing out to this. I'm not sure if the admins approach is ideal but helps to be aware. Also explains why some of the top agents are not being updated
> > 
> > 
> > 


---



</div>
<div class="column-right">

# 日本語訳

# 最終評価 - 質問
**vj4science** *2024年7月27日（土）11:18:16 GMT+0900（日本標準時）* (投票数: 6)
以下の段落について、明確にしていただけますか？ ロックされた3つの提出物は606から開始されるのですか？それとも、8月13日以前の実行から蓄積されたスコアを引き継ぐのですか？
「最終評価
2024年8月13日の提出締め切り時点で、提出物はロックされます。2024年8月13日から2024年8月27日まで、新しい未公開の秘密の単語セットに対してエピソードを実行し続けます。この期間中、あなたの3つのアクティブな提出物だけがリーダーボードの対象となります。この期間の終わりに、リーダーボードは確定します。」

---
# 他のユーザーからのコメント
> ## Mahmoud Elshahed
> 
> 論理的に考えると、隠れたテストセットではゼロからスタートすべきでしょう。
> 
> そうでない場合、現在の公開単語リストを使って、モデル構築ではなくスクリプトでの反復を行うことができ、高スコアを得やすくなります。また、評価期間中にスコアがあまり減少しないことで、ユーザーは有利になってしまいます。
> 
> 「私の意見ですが」

> ## sayoulala
> 
> おっしゃる通りだと思います。
> 
> > 

---
> ## Chris Deotte
> 
> Kaggleの管理者が[こちら](https://www.kaggle.com/competitions/llm-20-questions/discussion/512358#2872495)でコメントしています。
> 
> はい、現在のリーダーボードが最終評価期間におけるエージェントの基本となります。新しい単語セットのもとで十分なゲームが行われるように調整し、たとえエージェントが大きく過小評価されていても問題にならないようにします。

> ## gguillard
> 
> それは驚くべきことだ。
> 
> > 

> ## vj4scienceトピック著者
> 
> Chris、これを指摘してくれてありがとう。管理者のアプローチが理想的かわからないけれど、知っておくのは大事だね。また、なぜいくつかのトップエージェントの更新が行われないのかも説明がつく。


</div>