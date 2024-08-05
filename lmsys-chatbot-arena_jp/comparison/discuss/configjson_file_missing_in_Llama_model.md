# 要約 
このディスカッションは、KaggleのLMSYS - Chatbot Arena Human Preference PredictionsコンペティションにおけるLlamaモデルの利用に関するものです。

ユーザーAlphaTT30は、自分のノートブックでLlamaモデルを使用しようとした際に、`config.json`ファイルが見つからないというエラーに遭遇しました。他のユーザーのノートブックでは問題なく動作しているため、原因を特定しようと質問しています。

コメント欄では、Artyom Lyanがtransformersバージョンを使用するようアドバイスしています。Saiyan Warriorは、Llamaへのアクセス許可を取得する必要があるか、パスが間違っている可能性を指摘し、エラーメッセージの詳細を要求しています。

AlphaTT30は、アクセス許可は取得済みでパスも正しいことを確認し、他のユーザーのノートブックから同じモデルをコピーしても`config.json`ファイルが見つからないと報告しています。

このディスカッションは、Llamaモデルの利用に関する問題を解決するための情報共有とトラブルシューティングの場となっています。しかし、具体的な解決策は得られていません。 


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

# config.json file missing in Llama model

**AlphaTT30** *Thu Jul 04 2024 16:18:38 GMT+0900 (日本標準時)* (0 votes)

I copied other notebooks where the config.json file exists. But when I add the model as input in my notebooks the config.json file is missing so the model does not load. 

Why is that and what to do? 



---

 # Comments from other users

> ## Artyom Lyan
> 
> You should use transformers version, not pytorch
> 
> 
> 


---

> ## Saiyan Warrior
> 
> HI [@alphatt30](https://www.kaggle.com/alphatt30) there might be 2 reasons that I can think of:
> 
> You might need to get the llama permission [here](https://www.kaggle.com/models/metaresearch/llama-3)
> You might have given the wrong path.
> 
> can you share the exact error?
> 
> 
> 
> > ## AlphaTT30Topic Author
> > 
> > I have permission and the path was correct, I even tried other's notebooks where they used the same model. so I removed their model and then loaded the same model in input and config.json was still missing there 
> > 
> > 
> > 


---



</div>
<div class="column-right">

# 日本語訳

# config.json ファイルがLlamaモデルで見つかりません

**AlphaTT30** *2024年7月4日 16:18:38 (日本標準時)* (0票)

他のノートブックでは config.json ファイルが存在するのですが、自分のノートブックでモデルを入力として追加すると、config.json ファイルが見つからず、モデルがロードされません。

なぜでしょうか？どうすればいいですか？

---

# 他のユーザーからのコメント

> ## Artyom Lyan
> 
> transformers バージョンを使用する必要があります。pytorch は使用しないでください。
> 
> 
> 
---
> ## Saiyan Warrior
> 
> こんにちは [@alphatt30](https://www.kaggle.com/alphatt30) さん。考えられる原因は2つあります。
> 
> Llama のアクセス許可を取得する必要があるかもしれません。[こちら](https://www.kaggle.com/models/metaresearch/llama-3) を参照してください。
> パスが間違っている可能性があります。
> 
> エラーメッセージを具体的に教えていただけますか？
> 
> 
> 
> > ## AlphaTT30 トピック作成者
> > 
> > アクセス許可は取得済みで、パスも正しいです。他のユーザーが同じモデルを使用したノートブックを試してみましたが、そのモデルを削除して同じモデルを自分のノートブックに入力しても、config.json ファイルは依然として見つかりませんでした。
> > 
> > 
> > 
--- 



</div>