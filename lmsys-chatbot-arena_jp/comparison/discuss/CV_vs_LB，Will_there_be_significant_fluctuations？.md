# 要約 
このディスカッションは、Kaggleコンペティションにおける交差検証（CV）とリーダーボード（LB）のスコア間の相関関係について議論しています。

トピック作成者のsayoulalaは、このコンペティションでCVとLBの間に大きな変動があるかどうかを尋ねています。

Valentin Wernerは、過去のコンペティションではCVとLBの相関関係が良好であったことを指摘していますが、いくつかのコンペティションでは大きな変動があったことを認めています。彼は、特にTHE LEARNING AGENCY LABが主催したコンペティションでは、CVとLBの間に大きな差があったことを例に挙げています。

xiaotingtingは、トレーニングセットとテストセットの分布の違いが、CVとLBのスコア間の差に影響を与える可能性があると指摘しています。

Dlond Mikeは、ユーモラスなコメントで、トピック作成者を励ましています。

このディスカッションは、CVとLBのスコア間の相関関係がコンペティションによって異なる可能性があり、トレーニングセットとテストセットの分布の違いが重要な要因となる可能性があることを示しています。


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

# CV vs LB，Will there be significant fluctuations？

**sayoulala** *Sun Jul 14 2024 12:02:54 GMT+0900 (日本標準時)* (5 votes)

Hello everyone, what do you think about the trends of CV (Cross-Validation) and LB (Leaderboard) in this competition's challenge? Will there be significant fluctuations, similar to recent competitions?



---

 # Comments from other users

> ## Valentin Werner
> 
> The obligatory post towards the end of each competition. 
> 
> I cannot really answer your question, but I can say that we definetly managed to overfit models on CV before. However, in a lot of cases we have pretty good LB and CV correlation. This is something I often did not have in competitions with large shakeup.
> 
> 
> 
> > ## sayoulalaTopic Author
> > 
> > Then you probably haven't participated in the competitions hosted by THE LEARNING AGENCY LAB on Kaggle, haha."
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > DAIGT was wild, but I do not recall people feeling good about their CV - LB correlation in it. 
> > > 
> > > After a quick search, I found this, which agrees with what I remember [https://www.kaggle.com/competitions/llm-detect-ai-generated-text/discussion/458477](https://www.kaggle.com/competitions/llm-detect-ai-generated-text/discussion/458477)
> > > 
> > > But I also remember this gem which aged like fine milk: [https://www.kaggle.com/competitions/llm-detect-ai-generated-text/discussion/462235](https://www.kaggle.com/competitions/llm-detect-ai-generated-text/discussion/462235)
> > > 
> > > 
> > > 


---

> ## xiaotingting
> 
> It depends on the difference in the distribution of the training set and the test set. I can only say that there may be a big difference between the leaderboard score and the cross-validation score.
> 
> 
> 


---

> ## Dlond Mike
> 
> don't worry my friend,u are the first in LB:)
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# CV vs LB、大きな変動はあるのか？

**sayoulala** *2024年7月14日 12:02:54 (日本標準時)* (5 votes)
皆さん、このコンペティションのCV（交差検証）とLB（リーダーボード）の傾向についてどう思いますか？最近のコンペティションのように、大きな変動があると思いますか？
---
# 他のユーザーからのコメント
> ## Valentin Werner
> 
> これは、コンペティションの終わり頃に必ず出てくる話題ですね。
> 
> あなたの質問に直接答えることはできませんが、私たちは確かに以前、CVでモデルを過剰適合させていました。しかし、多くの場合、LBとCVの相関関係は非常に良好です。これは、大きな変動があったコンペティションではあまり見られなかったことです。
> 
> 
> 
> > ## sayoulalaトピック作成者
> > 
> > じゃあ、あなたはKaggleのTHE LEARNING AGENCY LABが主催したコンペティションには参加していないんですね、笑。"
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > DAIGTは大変でしたが、CVとLBの相関関係について、みんなが満足していたとは思いません。
> > > 
> > > 少し調べてみたところ、私の記憶と一致する内容を見つけました。[https://www.kaggle.com/competitions/llm-detect-ai-generated-text/discussion/458477](https://www.kaggle.com/competitions/llm-detect-ai-generated-text/discussion/458477)
> > > 
> > > でも、この素晴らしい記事も覚えています。これは、まるで腐った牛乳のように時代遅れになりましたね。[https://www.kaggle.com/competitions/llm-detect-ai-generated-text/discussion/462235](https://www.kaggle.com/competitions/llm-detect-ai-generated-text/discussion/462235)
> > > 
> > > 
> > > 
---
> ## xiaotingting
> 
> それは、トレーニングセットとテストセットの分布の違いによって異なります。リーダーボードのスコアと交差検証のスコアの間には大きな差がある可能性があるとしか言えません。
> 
> 
> 
---
> ## Dlond Mike
> 
> 心配しないでください、あなたはLBで1位です:)
> 
> 
> 
--- 



</div>