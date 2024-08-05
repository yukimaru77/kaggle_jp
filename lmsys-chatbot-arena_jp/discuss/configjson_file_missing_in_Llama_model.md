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
