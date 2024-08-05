# 要約 
コンペのディスカッションでは、ユーザーのOminousDudeが自分のモデルをテストするための場所を探していることが述べられています。それに対してChris Deotteが、「メトリクス」という用語について説明し、リーダーボードがどのように機能するかについて触れています。具体的には、これまでにプレイしたゲームの数に基づいて成績が算出されることを説明し、バリデーション中にはそのメトリクスが使用できない点を指摘しています。バリデーションの目的は、モデルができるだけ少ない質問で正確に単語を推測できるかを評価することです。OminousDudeは、このやり取りに感謝しつつ、圧縮されたモデルの対戦を確認できる場所を知りたいと求めています。

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

# Where can I find the llm 20 Q metric?

**OminousDude** *Sat Jun 29 2024 07:03:28 GMT+0900 (日本標準時)* (0 votes)

Basically, the title wanted to be able to test my models. 😁



---

 # Comments from other users

> ## Chris Deotte
> 
> The "metric" is how our overall LB increases which uses a formula based on number of games we have previously played. However during validation I do not think we can use this.
> 
> For validation, I think we just want accuracy and speed of win. In other words optimize our models to correctly guess word in 20 questions and guess in the fewest number of guesses (i.e << 20)
> 
> 
> 
> > ## OminousDudeTopic Author
> > 
> > Ok, Thank you!
> > 
> > 
> > 
> > > ## OminousDudeTopic Author
> > > 
> > > Sorry but this is not what I meant I wanted to know if I could find how the zipped models are played against eachother
> > > 
> > > 
> > > 


---



</div>
<div class="column-right">

# 日本語訳

# LLM 20 Qのメトリクスはどこで見つけられますか？
**OminousDude** *2024年6月29日 土曜日 07:03:28 JST* (0票)
基本的に、タイトルとしては自分のモデルをテストできる場所を探しています。😁
---
 # 他のユーザーからのコメント
> ## Chris Deotte
> 
> 「メトリクス」とは、これまでにプレイしたゲームの数に基づく計算式を用いて、私たちのリーダーボード全体がどのように増加するかを指します。しかし、バリデーション中にはこれを使用できないと思います。
> 
> バリデーションでは、正確性と勝利までのスピードを把握したいです。つまり、20の質問で正しく単語を推測し、できるだけ少ない質問（つまり20より少ない）で推測できるようモデルを最適化することが目標です。
> 
> > ## OminousDude トピック作成者
> > 
> > ありがとうございます！
> > 
> > > ## OminousDude トピック作成者
> > > 
> > > すみませんが、私が知りたかったのは、圧縮されたモデルがどのように対戦するかを確認できる場所です。


</div>