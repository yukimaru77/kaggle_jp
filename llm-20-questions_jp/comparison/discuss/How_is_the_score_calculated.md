# 要約 
ディスカッションでは、スコアの算出方法についての質問がされました。ユーザーの「OminousDude」が、エピソードごとにスコアの変動が大きい場合と小さい場合があることに疑問を持っています。これに対し、「Chris Deotte」は、スコアがガウス分布N(μ,σ²)に基づいており、μが推定スキル、σが不確実性であることを説明しました。提出物は自己対戦のバリデーションを経て、成功すれば初期スキルμ0=600として評価プールに加わります。また、勝利や敗北がスコアに与える影響は、引き分けより大きいとのことです。「OminousDude」はこの説明に感謝の意を示しています。

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

# How is the score calculated?

**OminousDude** *Mon May 27 2024 11:12:07 GMT+0900 (日本標準時)* (0 votes)

I was looking through some episodes and in some, I see massive changes in the score up to +64 and -64 but in some, I see stuff like +0 +1 +4 etc. I was wondering how this is calculated. Thank you for the help!



---

 # Comments from other users

> ## Chris Deotte
> 
> The evaluation page says:
> 
> Each submission has an estimated skill rating which is modeled by a Gaussian N(μ,σ2) where μ is the estimated skill and σ represents the uncertainty of that estimate which will decrease over time.
> 
> When you upload a submission, we first play a validation episode where that submission plays against copies of itself to make sure it works properly. If the episode fails, the submission is marked as error and you can download the agent logs to help figure out why. Otherwise, we initialize the submission with μ0=600 and it joins the pool of for ongoing evaluation.
> 
> I have noticed that a true win or loss changes score more than a tie (i.e. no team gets a correct answer).
> 
> 
> 
> > ## OminousDudeTopic Author
> > 
> > Thanks very much!
> > 
> > 
> > 


---



</div>
<div class="column-right">

# 日本語訳

# スコアはどのように算出されるのですか？
**OminousDude** *2024年5月27日 11:12:07 日本標準時* (0票)
いくつかのエピソードを見ていたのですが、あるエピソードではスコアが+64や-64の大きな変動が見られるのに対し、他のエピソードでは+0、+1、+4などの小さな変動が見られます。このスコアがどのように計算されるのか気になっています。助けていただけると嬉しいです！

---
 # 他のユーザーからのコメント
> ## Chris Deotte
> 
> 評価ページには以下のように記載されています：
> 
> 各提出物には、ガウス分布N(μ,σ2)でモデル化された推定スキルレーティングがあります。ここでμは推定スキル、σはその推定の不確実性を表し、時間とともに減少します。
> 
> 提出物をアップロードすると、まずその提出物が自己のコピーと対戦するバリデーションエピソードが実行され、正しく機能することが確認されます。エピソードが失敗した場合、その提出物はエラーとしてマークされ、原因を特定するためにエージェントログをダウンロードできます。そうでない場合は、μ0=600で提出物を初期化し、継続的な評価のためにプールに追加します。
> 
> 私が気づいたのは、実際の勝利や敗北がスコアに与える影響は、引き分け（つまり、どちらのチームも正解を出さなかった場合）よりも大きいということです。
> 
> > ## OminousDudeトピックの作成者
> > 
> > ご丁寧にありがとうございます！
> > 
> > >


</div>