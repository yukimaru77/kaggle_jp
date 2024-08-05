# 要約 
このディスカッションは、Llama-8bとLlama-8b-instructモデルの性能向上におけるテンプレートの効果について議論しています。

投稿者は、インストラクトモデルはテンプレートを使用することで性能が向上すると聞いていましたが、自身の試みではテンプレートなしでも同じLBスコアだったと報告しています。さらに、テンプレートを使用するとスコアが悪化し、loglossがスタックする傾向があるとも述べています。

コメント欄では、別のユーザーもLlama3のインストラクトモデルでテンプレートを使用してみたものの、テンプレートなしよりも性能が悪化したと報告しています。

このディスカッションは、インストラクトモデルにおけるテンプレートの効果はモデルや設定によって異なる可能性を示唆しています。投稿者は、テンプレートの使用に関するさらなる洞察や意見を求めています。


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

# Using template for instruct model?

**Weiren** *Thu Jul 11 2024 15:42:49 GMT+0900 (日本標準時)* (0 votes)

I heard that using instruct model would perform slightly better. But when I was using Llama-8b and Llama-8b-instruct without template,  they got the same LB score.

Does the template matters? I had tried using template but the score was even worse. Also, I found that using a template causes the logloss stuck…

Some details:

1 epoch

4 batch size * 2 accumulation_steps

and just trying different lora params 🤡

Any thoughts or insights on this?



---

 # Comments from other users

> ## hn
> 
> Actually anecdotally I use the Llama3 template as well for instruct and I think it’s worse off than no template for some reason. 
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# テンプレートを使ったインストラクトモデルについて

**Weiren** *木曜日 7月 11日 2024 15:42:49 GMT+0900 (日本標準時)* (0 票)

インストラクトモデルを使うと少し性能が向上するって聞いたんだけど、テンプレートなしでLlama-8bとLlama-8b-instructを使ってみたら、どちらも同じLBスコアだったんだ。
テンプレートって重要なのかな？ テンプレートを使ってみたらスコアが悪化したんだけど。それに、テンプレートを使うとloglossがスタックするみたいなんだよね…
詳細:
1エポック
4バッチサイズ * 2アキュムレーションステップ
あとは、いろんなloraパラメータを試してるだけだよ🤡
何か考えや洞察があれば教えてください！
---
# 他のユーザーからのコメント
> ## hn
> 
> 実は、インストラクト用にLlama3のテンプレートも使ってるんだけど、なぜかテンプレートなしよりも悪くなってるんだ。
> 
> 
> 
--- 



</div>