# 要約 
このディスカッションは、KaggleのLMSYS - Chatbot Arena Human Preference PredictionsコンペティションにおけるLlama3の使用に関するものです。

ユーザーのzywは、Metaの公式ウェブサイトからLlama3のフォームを送信したところ、モデルの作者から使用を拒否されたと報告しています。Llama2は正常に使用できるものの、Llama3は使用できません。

Valentin Wernerは、Hugging Faceでアカウントを作成し、モデルページでLlama3を申請することで、Llama3を使用できる回避策を提案しています。この方法は、ローカルでのトレーニングに適していますが、ノートブックでインターネットアクセスを無効にすることはできません。

zywは、Valentin Wernerの提案に感謝し、有益な情報だとコメントしています。


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

# How can i use llama3?

**zyw** *Tue May 28 2024 03:11:29 GMT+0900 (日本標準時)* (1 votes)

I submitted the llama3 form without applying from the meta official website, and the model author refused me to use llama3. 

After I clicked "here" and filled out the form on the meta official website, I can now use llama2 normally, but cannot use llama3. I want to resubmit the form but I don't find the submit button. Can anyone help me solve this problem?



---

 # Comments from other users

> ## Valentin Werner
> 
> Not directly answering your problem, but giving you a workaround:
> 
> You can also go to huggingface, create an Account, apply for llama3 on the model Page, wait 12 hours, put an access token into your Notebook (dont share it!!) and then use it that way by specifying "token=…" in all the from_pretrained calls (model, tokenizer).
> 
> this is rather recommended for local Training. You will not be able to turn off Internet access for that notebook.
> 
> 
> 
> > ## zywTopic Author
> > 
> > This is indeed a great idea, thank you for sharing!
> > 
> > 
> > 


---



</div>
<div class="column-right">

# 日本語訳

# Llama3の使用方法について

**zyw** *2024年5月28日 火曜日 03:11:29 日本標準時* (1票)

Metaの公式ウェブサイトから申請せずにLlama3のフォームを送信したところ、モデルの作者からLlama3の使用を拒否されました。
Metaの公式ウェブサイトで「こちら」をクリックしてフォームを送信したところ、Llama2は正常に使用できるようになりましたが、Llama3は使用できません。フォームを再提出したいのですが、送信ボタンが見つかりません。この問題を解決する方法はありますか？

---
# 他のユーザーからのコメント

> ## Valentin Werner
> 
> あなたの問題に直接答えるものではありませんが、回避策を提案します。
> 
> Hugging Faceにアカウントを作成し、モデルページでLlama3を申請することができます。12時間待機した後、アクセス・トークンをノートブックに入力し（共有しないでください！）、`token=...`をすべての`from_pretrained`呼び出し（モデル、トークナイザー）に指定することで、Llama3を使用できます。
> 
> この方法は、ローカルでのトレーニングに適しています。ノートブックでインターネットアクセスを無効にすることはできません。
> 
> 
> > ## zywTopic Author
> > 
> > 素晴らしいアイデアですね！共有していただきありがとうございます！
> > 
> > 
> > 
---



</div>