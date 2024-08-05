# 要約 
このディスカッションは、KaggleのLMSYS - Chatbot Arena Human Preference Predictionsコンペティションにおける、Huggingfaceを使ったモデル構築に関するものです。

Heroseoさんは、Huggingfaceを使った新しいノートブックを共有しました。このノートブックは、トークナイザーにプロンプト、response_a、response_bの3つのテキストすべてを使用しています。V3バージョンでは、truncate_textを追加しましたが、スコアは少し悪化しました。

Nicholas Broadさんは、Heroseoさんのモデルがラベル1しか予測していないのではないかと指摘しました。Valentin Wernerさんは、その予測であれば推論時間を節約できるとコメントしました。Heroseoさんは、指摘に感謝し、後で確認して更新すると回答しました。しかし、現在KaggleのGPU時間が不足しているため、すぐに更新できないとのことです。 


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

# [New Starter] 3 texts + Huggingface

**Heroseo** *Sun May 05 2024 05:16:42 GMT+0900 (日本標準時)* (2 votes)

I shared a new notebook for Huggingface users.

This notebook uses huggingface and uses all three texts in the tokenizer.

- prompt, response_a, response_b

V3 - add truncate_text - but score got a little worse

- link: [[Train] LMSYS / Deberta-v3 meets Huggingface](https://www.kaggle.com/code/piantic/train-lmsys-deberta-v3-meets-huggingface/notebook)



---

 # Comments from other users

> ## Nicholas Broad
> 
> your model only predicts label 1?
> 
> 
> 
> > ## Valentin Werner
> > 
> > I guess you can save some inference time on those predictions 😉
> > 
> > 
> > 
> > ## HeroseoTopic Author
> > 
> > thank you for telling me. I will check again later and update.
> > 
> > p.s. But now I've run out of Kaggle GPU time. 🥲
> > 
> > 
> > 


---



</div>
<div class="column-right">

# 日本語訳

# 【初心者向け】3つのテキスト + Huggingface
**Heroseo** *2024年5月5日 日曜日 5:16:42 JST* (2票)

Huggingfaceユーザー向けの新しいノートブックを共有しました。
このノートブックはHuggingfaceを使用し、トークナイザーに3つのテキストすべてを使用しています。
- プロンプト、response_a、response_b
V3 - truncate_textを追加 - しかしスコアは少し悪化しました
- リンク: [[Train] LMSYS / Deberta-v3 meets Huggingface](https://www.kaggle.com/code/piantic/train-lmsys-deberta-v3-meets-huggingface/notebook)
---
# 他のユーザーからのコメント
> ## Nicholas Broad
> 
> あなたのモデルはラベル1しか予測していませんか？
> 
> 
> 
> > ## Valentin Werner
> > 
> > その予測では、推論時間を節約できると思います😉
> > 
> > 
> > 
> > ## HeroseoTopic Author
> > 
> > 教えてくれてありがとうございます。後で確認して更新します。
> > 
> > 追伸: しかし、今はKaggleのGPU時間がなくなってしまいました。🥲
> > 
> > 
> > 
--- 



</div>