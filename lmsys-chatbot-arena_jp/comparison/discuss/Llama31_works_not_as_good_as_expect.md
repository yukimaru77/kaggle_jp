# 要約 
このディスカッションは、KaggleのLMSYS - Chatbot Arena Human Preference PredictionsコンペティションにおけるLlama3.1モデルのパフォーマンスに関するものです。

多くの参加者が、Llama3.1モデルが期待通りのパフォーマンスを発揮せず、gemma-2モデルよりも劣る結果が出ていると報告しています。

具体的には、QLoRA+SFTのftメソッドを使用した場合、Llama3.1モデルのクロスバリデーションスコアが0.914と非常に低く、gemma-2モデルよりも劣る結果が出ています。

この問題の原因として、トークナイザーが正しいbosトークンを使用していない可能性が指摘されています。しかし、トークナイザーを修正してもパフォーマンスが改善しないという報告もあります。

また、他の参加者も同様の結果を得ており、Llama3.1モデルのパフォーマンスがgemma-2モデルよりも劣ることは事実のようです。

このディスカッションは、Llama3.1モデルのパフォーマンスに関する懸念を共有し、解決策を探るためのものです。参加者たちは、互いに情報交換を行い、より良い結果を得るための方法を探しています。


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

# Llama3.1 works not as good as expect

**justin1357** *Wed Jul 24 2024 13:44:46 GMT+0900 (日本標準時)* (10 votes)

After first 1000 steps, i found its performence is worse than gemma-2 slightly.



---

 # Comments from other users

> ## Rise_Hand
> 
> I got a very bad result according to llama3.1 while using the ft method of QLoRA+SFT. CV = 0.914
> 
> 
> 


---

> ## Nicholas Broad
> 
> Make sure your tokenizer uses the [correct bos token](https://huggingface.co/meta-llama/Meta-Llama-3.1-8B-Instruct/discussions/29)
> 
> 
> 
> > ## justin1357Topic Author
> > 
> > still bad performance
> > 
> > 
> > 


---

> ## Xinyuan Qiao
> 
> I tested it in [@emiz6413](https://www.kaggle.com/emiz6413) notebook with exact same parameter, the evaluation log loss is 0.958, the gemma2 version was 0.927.
> 
> 
> 


---

> ## sayoulala
> 
> Thanks for share it. That's great, it looks like I'll be able to save a lot on my electricity bill, hahaha!
> 
> 
> 
> > ## william.wu
> > 
> > You're safe for the 1st place. It's tough to make improvements😭
> > 
> > 
> > 


---

> ## justin1357Topic Author
> 
> After 4000 steps, its significantly worse than gemma-2 haha
> 
> 
> 


---

> ## Lorry Zou
> 
> Thank you for saving our time and TPU quota😁
> 
> 
> 


---

> ## Yixiao Yuan
> 
> Same here.
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# Llama3.1 のパフォーマンスが期待通りに良くない

**justin1357** *2024年7月24日 13:44:46 (日本標準時)* (10票)

最初の1000ステップの後、Llama3.1のパフォーマンスはgemma-2よりもわずかに劣ることがわかりました。

---
# 他のユーザーからのコメント

> ## Rise_Hand
> 
> QLoRA+SFTのftメソッドを使用しているのですが、Llama3.1では非常に悪い結果が出ています。CVは0.914です。
> 
> 
> 
---
> ## Nicholas Broad
> 
> トークナイザーが[正しいbosトークン](https://huggingface.co/meta-llama/Meta-Llama-3.1-8B-Instruct/discussions/29)を使用していることを確認してください。
> 
> 
> 
> > ## justin1357トピック作成者
> > 
> > まだパフォーマンスが悪いですね。
> > 
> > 
> > 
---
> ## Xinyuan Qiao
> 
> [@emiz6413](https://www.kaggle.com/emiz6413)のノートブックで、まったく同じパラメータでテストしたところ、評価ログ損失は0.958でした。gemma2バージョンは0.927でした。
> 
> 
> 
---
> ## sayoulala
> 
> 共有してくれてありがとうございます。素晴らしいですね！これで電気代を大幅に節約できそうです。笑
> 
> 
> 
> > ## william.wu
> > 
> > 1位は安泰ですね。改善するのは難しいです😭
> > 
> > 
> > 
---
> ## justin1357トピック作成者
> 
> 4000ステップ後、gemma-2よりも大幅に悪くなりました。笑
> 
> 
> 
---
> ## Lorry Zou
> 
> 時間とTPUクォータを節約してくれてありがとうございます😁
> 
> 
> 
---
> ## Yixiao Yuan
> 
> 私も同じです。
> 
> 
> 
---



</div>