# 要約 
このディスカッションは、Kaggleコンペティション「LMSYS - Chatbot Arena 人間による好み予測チャレンジ」におけるモデルのトレーニングに関するものです。

投稿者は、複数のモデルを微調整したものの、損失がほとんど変化していないため、トレーニングを続けるべきかどうか悩んでいます。損失曲線は2000ステップごとに確認しており、現状では判断が難しい状況です。

コメントでは、S J Moudry氏が、検証セットでのパフォーマンスを重視し、ウォーミングアップステップを確認するようアドバイスしています。ウォーミングアップステップが少なすぎると、初期に大きな低下が発生し、その後はほとんど改善が見られない可能性があるとのことです。

このディスカッションは、モデルのトレーニングにおける重要なポイントである、適切なトレーニング時間とウォーミングアップステップの設定について議論しています。参加者は、このディスカッションを通じて、自身のモデルのトレーニング戦略を見直すヒントを得られるでしょう。


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

# Do I still need to continue training?

**KeShuang Liu** *Fri Jul 26 2024 14:05:04 GMT+0900 (日本標準時)* (0 votes)

I have fine tuned many models, but the losses have remained almost unchanged. Is it necessary for me to continue training because I haven't trained enough? I find it difficult to make a decision at this point.This is my current validation set loss curve, which I verify every 2000 steps



---

 # Comments from other users

> ## S J Moudry
> 
> Are you testing on a validation set? I'd be more worried about performance there.  I'd also check my warmup steps and set them around 5-20%, having too few can cause a big drop right away but then you never really improve.
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# 引き続きトレーニングを続ける必要があるか？
**KeShuang Liu** *金 7月 26 2024 14:05:04 GMT+0900 (日本標準時)* (0 票)

多くのモデルを微調整しましたが、損失はほとんど変化していません。十分にトレーニングしていないため、トレーニングを続ける必要があるのでしょうか？現時点で判断するのが難しいです。これは、2000ステップごとに確認する現在の検証セットの損失曲線です。
---
# 他のユーザーからのコメント
> ## S J Moudry
> 
> 検証セットでテストしていますか？検証セットでのパフォーマンスの方が心配です。また、ウォーミングアップステップを確認して、5〜20％程度に設定してください。ウォーミングアップステップが少なすぎると、すぐに大きな低下が発生しますが、その後はほとんど改善されません。
> 
> 
> 
---



</div>