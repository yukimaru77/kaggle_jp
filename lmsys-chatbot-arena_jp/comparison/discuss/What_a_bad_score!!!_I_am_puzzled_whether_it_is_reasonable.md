# 要約 
このディスカッションは、KaggleコンペティションにおけるローカルCVとLB（リーダーボード）のスコア間の大きな差について議論しています。

投稿者は、gemma-2とllama-3を用いたモデルで、ローカルCVでは高いスコア（0.9366と0.916）を達成したものの、LBでは大幅に低いスコア（0.968と0.934）しか得られず、その理由を疑問視しています。

他のユーザーからのコメントでは、同様の経験を持つ人が多く、ローカルCVとLBの差はよくあることであるという意見が多数見られます。

いくつかのコメントでは、この差はデータの過剰適合が原因である可能性が指摘されています。また、テストセットにローカルCVでは見られない有意なパターンが存在する可能性も示唆されています。

投稿者は、他のユーザーのコメントから、コードにバグがある可能性や、CVとLBの差はそれほど珍しいことではないという認識を得ています。

このディスカッションは、KaggleコンペティションにおけるローカルCVとLBのスコア間の差について、多くの参加者が共通して抱える問題であることを示しています。また、この差の原因を特定し、改善するためのヒントも提供しています。


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

# What a bad score!!! I am puzzled whether it is reasonable?

**Turbo** *Tue Jul 30 2024 13:28:30 GMT+0900 (日本標準時)* (4 votes)

I encountered inference score bad problem.

I used gemma-2 to classify and got local cv(20% data) = 0.9366, lb=0.968.

Also, I used llama-3 to regression and got local cv(20% data) = 0.916, lb=0.934.

What a bad result!!!.

Inspired by [@jsday96](https://www.kaggle.com/jsday96), so I tried to both inference on kaggle and local. The results are shown below. The results are train data head 10. The difference is very small. I am puzzled whether it is reasonable?



---

 # Comments from other users

> ## KeShuang Liu
> 
> After reading your discussion, I tested my model, which was very useful to me. I don't know why my local prediction is so different from the prediction on Kaggle, which leads to a big difference between cv and lb. I think this is the reason. This gave me new ideas. Thank you very much for your discussion.
> 
> 
> 
> > ## TurboTopic Author
> > 
> > Hey, the results have big difference. Maybe some bugs in the code which you need to check.
> > 
> > 
> > 


---

> ## Helmut12
> 
> I think that may be normal in kaggle competition. Is this related to overfitting of the data? Like there is a significant pattern in our test set. I heard that there is a huge discrepancy between LB and the final result in a previous competition because of overfitting.
> 
> 
> 


---

> ## justin1357
> 
> cv is lower than lb, that's normal.
> 
> 
> 
> > ## TurboTopic Author
> > 
> > low 0.02. Others said the results of cv and lb are very small.
> > 
> > 
> > 
> > > ## justin1357
> > > 
> > > In my exp, cv low 0.02 too
> > > 
> > > 
> > > 


---



</div>
<div class="column-right">

# 日本語訳

# これはひどいスコアだ！ 妥当なのか疑問です。
**Turbo** *2024年7月30日 火曜日 13:28:30 GMT+0900 (日本標準時)* (4 votes)
推論スコアが悪くて困っています。
gemma-2を使って分類したところ、ローカルCV（データの20%）は0.9366、LBは0.968でした。
また、llama-3を使って回帰を行ったところ、ローカルCV（データの20%）は0.916、LBは0.934でした。
ひどい結果です！
[@jsday96](https://www.kaggle.com/jsday96) に触発されて、Kaggleとローカルの両方で推論を試してみました。結果は以下に示されています。結果はトレーニングデータの先頭10行です。差は非常に小さいです。妥当なのか疑問です。
---
# 他のユーザーからのコメント
> ## KeShuang Liu
> 
> あなたのディスカッションを読んだ後、自分のモデルをテストしてみました。とても役に立ちました。なぜ私のローカル予測がKaggleでの予測と大きく異なるのか分かりません。これがCVとLBの大きな差につながっています。これが理由だと思います。新しいアイデアが得られました。ディスカッションを共有していただきありがとうございます。
> 
> 
> 
> > ## TurboTopic Author
> > 
> > 結果に大きな差がありますね。コードにバグがあるかもしれません。確認する必要があります。
> > 
> > 
> > 
---
> ## Helmut12
> 
> Kaggleコンペティションではよくあることだと思います。これはデータの過剰適合に関連しているのでしょうか？テストセットに有意なパターンがあるのかもしれません。以前のコンペティションでは、過剰適合のためにLBと最終結果に大きな食い違いがあったと聞いたことがあります。
> 
> 
> 
---
> ## justin1357
> 
> CVがLBより低いのは普通です。
> 
> 
> 
> > ## TurboTopic Author
> > 
> > 0.02低いですね。他のユーザーは、CVとLBの結果は非常に小さいと言っていました。
> > 
> > 
> > 
> > > ## justin1357
> > > 
> > > 私の経験では、CVも0.02低いですね。
> > > 
> > > 
> > > 
---



</div>