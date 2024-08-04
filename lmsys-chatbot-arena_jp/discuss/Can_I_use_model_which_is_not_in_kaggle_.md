# Kaggleで外部モデルを使用できますか？

**AlphaTT30** *2024年6月29日 08:42:50 (日本標準時)* (1票)

このコンペティションでは、インターネットアクセスが許可されていません。そのため、Hugging Faceの事前学習済みトランスフォーマーモデル（例：google-bert/bert-base-uncased）を使用できません。このモデルを使用しようとすると、エラーが発生します。このモデルはダウンロードする必要があります。

```python
# モデルを直接ロード
from transformers import AutoTokenizer, AutoModelForMaskedLM
tokenizer = AutoTokenizer.from_pretrained("google-bert/bert-base-uncased")
model = AutoModelForMaskedLM.from_pretrained("google-bert/bert-base-uncased")
```

どうすればいいのでしょうか？

Hugging FaceのすべてのモデルがKaggleにあるのでしょうか？

Kaggleにあるモデルを使用するべきでしょうか？

それとも、このモデルを使用する別の方法があるのでしょうか？

---

# 他のユーザーからのコメント

> ## tanaka
> 
> このようなBert関連のモデルやLLMは、インターネット制限が適用される前にダウンロードできます。
> 
> このコンペティションの主なテーマは、
> 
> いくつかのテクニックとGPU（これはあなたに提供されます）を使用して、LLMまたはNLP関連のモデルをトレーニングすることです。
> 
> そして、これらのモデルをインターネットなしで推論モデルとして使用することです。
> 
> 
> 
---
> ## Yichuan Gao
> 
> モデルのライセンスが許可している場合、Hugging FaceからモデルをダウンロードしてKaggleにモデルとしてアップロードし、ノートブックに追加することができます。
> 
> 
> 
> > ## AlphaTT30Topic Author
> > 
> > Kaggle以外でモデルをトレーニングして、ここにアップロードし、このコンペティションでそのモデルを使用できますか？
> > 
> > 
> > 
> > > ## Ravi Ramakrishnan
> > > 
> > > はい、もちろんです。これは、これらのコンペティションを扱うための推奨される方法です [@alphatt30](https://www.kaggle.com/alphatt30) 
> > > 
> > > 
> > > 
> > ## Ivel afred
> > 
> > これは、モデルをKaggleで公開する必要があるという意味ですか？それとも、Hugging Faceで公開するだけで大丈夫ですか？
> > 
> > 
> > 
> > > ## Yichuan Gao
> > > 
> > > Hugging Faceにモデルをアップロードする必要はありません。Kaggleにアップロードするだけで大丈夫です。また、プライベート（デフォルト）にすることもでき、ノートブックで使用できます。
> > > 
> > > 
> > > 
> > > ## Ivel afred
> > > 
> > > LMSYSのコード要件には、「自由に公開されている外部データの使用が許可されています。事前学習済みモデルを含む。」と記載されています。これは、モデルを公開する必要があるという意味ではないでしょうか？少し混乱しています。
> > > 
> > > 
> > > 
--- 

