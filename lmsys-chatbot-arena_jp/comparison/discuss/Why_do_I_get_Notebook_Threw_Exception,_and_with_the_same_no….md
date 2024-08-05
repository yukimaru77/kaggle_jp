# 要約 
このディスカッションは、Kaggleコンペティションで「Notebook Threw Exception」というエラーが発生する原因について議論しています。投稿者は、同じノートブックを提出した際に、時々正常に提出できる場合があることに困惑しています。

コメントでは、OminousDude氏が、ランダムシードを設定していない場合、ゼロ除算などのエラーが発生する可能性があると指摘しています。これは、コードがランダムな要素を含んでいる場合、実行ごとに異なる結果が得られる可能性があり、エラーが発生する原因となる可能性があることを示唆しています。 


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

# Why do I get "Notebook Threw Exception", and with the same notebook, sometimes, I get a successful submission?

**Kilaru Vasudeva** *Sat Jun 15 2024 21:32:39 GMT+0900 (日本標準時)* (1 votes)

I find it wierd. Is it any wrong code specification on myside or it is something on the kaggle backend?



---

 # Comments from other users

> ## OminousDude
> 
> Can I get some more info about this problem? It could be if you don't set a random seed something like a division by zero could occur.
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# なぜ「Notebook Threw Exception」が発生するのですか？同じノートブックで、時々正常に提出できるのはなぜですか？
**Kilaru Vasudeva** *2024年6月15日 土曜日 21:32:39 日本標準時* (1票)

奇妙ですね。私のコードに問題があるのでしょうか、それともKaggleのバックエンドの問題でしょうか？
---
# 他のユーザーからのコメント
> ## OminousDude
> 
> この問題についてもう少し情報をもらえますか？ランダムシードを設定していない場合、ゼロ除算のようなエラーが発生する可能性があります。
> 
> 
> 
--- 



</div>