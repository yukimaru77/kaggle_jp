# 要約 
このディスカッションは、LMSYS - Chatbot Arena Human Preference Predictionsコンペティションにおいて、ブースティングモデルでどの程度のスコアが期待できるのかについて議論しています。

投稿者は、GBDTのみを使用した現時点で最も性能の高い公開ノートブックを紹介し、llama3推論とのスコア差が大きいことから、ブースティングで0.98を下回ることにこだわる価値があるのか疑問を呈しています。

他のユーザーからのコメントでは、テキストの特徴量アプローチを採用した結果、約1.036のスコアを達成したことが報告されています。しかし、これは現在のトップスコアから大きく離れているため、予測のメインモデルにする価値はないとされています。

結論として、このディスカッションでは、ブースティングモデルはスコア向上に限界がある可能性が示唆され、優勝を目指すのであれば、他の手法も検討する必要があることが示されています。一方で、ブースティングと特徴量エンジニアリングについて学びたいのであれば、1.0を下回るように努力することは有意義であるとされています。 


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

# How far can a boosting get you?

**Ivan Vybornov** *Sat Jun 08 2024 05:37:05 GMT+0900 (日本標準時)* (1 votes)

I am curious what is a score upper bound on using solely a boosting?

The best performing public notebook that only utilizes a GBDTs so far is [https://www.kaggle.com/code/andreasbis/lmsys-chatbot-arena-tf-idf#Model-Training-%F0%9F%A7%A0](https://www.kaggle.com/code/andreasbis/lmsys-chatbot-arena-tf-idf#Model-Training-%F0%9F%A7%A0)

But the difference with llama3 inference is more than significant (1.011 vs 0.989) which makes me wonder if one should even bother trying to get below 0.98 with it.



---

 # Comments from other users

> ## Valentin Werner
> 
> I was wondering the same. Different than the notebook you mentioned above I went a pure Text characteristic based Feature approach (Length, Paragraph Count, …) and got to around 1.036
> 
> This is so far away from Raja's current score that I think it is not worth to be the main model for the prediction
> 
> If you are not going for the win and instead want to learn about boosting and feature engineering, I would suggest you try to get below 1.0 yourself
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# ブースティングでどこまでスコアを伸ばせるのか？
**Ivan Vybornov** *2024年6月8日 土曜日 5:37:05 JST* (1票)

ブースティングのみを使って、どのくらいのスコアの上限が期待できるのか興味があります。

GBDTのみを使用した、現時点で最も性能の高い公開ノートブックは [https://www.kaggle.com/code/andreasbis/lmsys-chatbot-arena-tf-idf#Model-Training-%F0%9F%A7%A0](https://www.kaggle.com/code/andreasbis/lmsys-chatbot-arena-tf-idf#Model-Training-%F0%9F%A7%A0) です。

しかし、llama3推論との差は非常に大きく（1.011 対 0.989）、ブースティングで0.98を下回ることにこだわる価値があるのか疑問に思います。
---
# 他のユーザーからのコメント
> ## Valentin Werner
> 
> 私も同じことを考えていました。上記で紹介したノートブックとは異なり、私は純粋にテキストの特徴に基づく特徴量アプローチ（長さ、段落数など）を採用し、約1.036に到達しました。
> 
> これはRajaの現在のスコアからかなり離れているため、予測のメインモデルにする価値はないと思います。
> 
> もし優勝を目指さず、ブースティングと特徴量エンジニアリングについて学びたいのであれば、1.0を下回るように努力することをお勧めします。
> 
> 
> 
--- 



</div>