# 要約 
このディスカッションは、Kaggleコンペティション「LMSYS - Chatbot Arena 人間による好み予測チャレンジ」における、モデル実行に関する問題と解決策についてです。

ユーザーのKeShuang Liuは、CPUでモデルを実行した際に19GBのメモリを使用し、GPU p100では16GBしかなく、モデルが実行できない状況に直面していました。そこで、2つのt4ブロックを使用することで合計30GBのメモリが確保できることに気づき、モデルを2つのt4ブロックに展開する方法を質問しました。

ユーザーのMinato Ryanは、transformersライブラリを使用している場合は、`device_map="auto"`を使用することで、モデルが自動的に複数のGPUに分散されることを提案しました。KeShuang Liuは、この方法で問題を解決できたと報告しました。

このディスカッションは、Kaggleコンペティションにおける、GPUリソースの有効活用とモデルの分散実行に関する有益な情報提供となっています。


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

# How to run a model on two cards

**KeShuang Liu** *Mon Jun 17 2024 17:22:30 GMT+0900 (日本標準時)* (0 votes)

I loaded my model on the CPU and it took up 19g, while the GPU p100 only had 16g. However, I found that if I use two t4 blocks for a total of 30g, can I deploy my model to two t4 blocks? What should I do?



---

 # Comments from other users

> ## Minato Ryan
> 
> If you are using transformers library, use device_map="auto".
> 
> like this,
> 
> ```
> AutoModelForCausalLM.from_pretrained("google-bert/bert-base-cased", device_map="auto")
> 
> ```
> 
> 
> 
> > ## KeShuang LiuTopic Author
> > 
> > Thank you very much for your reply. I succeeded using your method
> > 
> > 
> > 


---



</div>
<div class="column-right">

# 日本語訳

# 2枚のGPUでモデルを実行する方法

**KeShuang Liu** *2024年6月17日 月曜日 17:22:30 JST* (0票)

CPUにモデルをロードしたところ、19GBのメモリを使用しました。一方、GPU p100は16GBしかありませんでした。しかし、2つのt4ブロックを使用すると合計30GBになることがわかりました。この場合、モデルを2つのt4ブロックに展開できますか？どうすればよいですか？

---
# 他のユーザーからのコメント

> ## Minato Ryan
> 
> transformersライブラリを使用している場合は、`device_map="auto"`を使用してください。
> 
> 例えば、
> 
> ```
> AutoModelForCausalLM.from_pretrained("google-bert/bert-base-cased", device_map="auto")
> 
> ```
> 
> 
> 
> > ## KeShuang Liuトピック作成者
> > 
> > ご回答ありがとうございます。この方法で成功しました。
> > 
> > 
> > 
---



</div>