# 要約 
## Kaggleコンペティションにおける外部モデル使用に関するディスカッション要約

このディスカッションは、Kaggleコンペティションにおいて、インターネットアクセスが制限されている状況下で、Hugging Faceの事前学習済みトランスフォーマーモデル（例：google-bert/bert-base-uncased）を使用する方法について議論しています。

**主なポイント:**

* **コンペティションの目的:** このコンペティションの目的は、提供されたGPUを用いて、LLMやNLP関連のモデルをトレーニングし、インターネットなしで推論モデルとして使用することです。
* **外部モデルの使用:**  コンペティションでは、自由に公開されている外部データの使用が許可されており、事前学習済みモデルも含まれます。
* **モデルの取得:** Hugging Faceからモデルをダウンロードし、Kaggleにアップロードすることで、コンペティションで使用することができます。
* **モデルの公開:** モデルを公開する必要はありません。Kaggleにアップロードし、プライベート設定にすることで、ノートブックで使用できます。

**結論:**

コンペティションでは、事前にHugging Faceからモデルをダウンロードし、Kaggleにアップロードすることで、インターネットアクセスなしで外部モデルを使用することができます。モデルを公開する必要はありません。

**追加情報:**

* コンペティションのコード要件には、外部データの使用が許可されていることが明記されています。
* モデルのライセンスが許可している場合、モデルをダウンロードして使用することができます。
* コンペティションの主なテーマは、LLMやNLP関連のモデルをトレーニングし、推論モデルとして使用することです。


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

# Can I use model which is not in kaggle ? 

**AlphaTT30** *Sat Jun 29 2024 08:42:50 GMT+0900 (日本標準時)* (1 votes)

In this competition, internet access is not allowed. So I can't use hugging face pre-trained transformer models like this one. The submission gets an error, I think for this one. This needs to be downloaded 

```
# Load model directly
from transformers import AutoTokenizer, AutoModelForMaskedLM

tokenizer = AutoTokenizer.from_pretrained("google-bert/bert-base-uncased")
model = AutoModelForMaskedLM.from_pretrained("google-bert/bert-base-uncased")

```

So what to do? 

Are all the hugging face models in kaggle? 

should I use a model that exists on Kaggle? 

or is there another way to use this one? 



---

 # Comments from other users

> ## tanaka
> 
> You can download these kind of Bert related things and llms before internet ristriction.
> 
> Major topic of these competition is
> 
> Training llm or nlp related model using some techniques and gpus (it is updated to you)
> 
> And then use these models as inference models without internet.
> 
> 
> 


---

> ## Yichuan Gao
> 
> If the model license permits, you can just download the model from huggingface and upload it to kaggle as a model, then add it to your notebook
> 
> 
> 
> > ## AlphaTT30Topic Author
> > 
> > Can I train a model outside kaggle and then upload here and use that model for this competition?  
> > 
> > 
> > 
> > > ## Ravi Ramakrishnan
> > > 
> > > Yes of course, this is a preferred way to handle these competitions [@alphatt30](https://www.kaggle.com/alphatt30) 
> > > 
> > > 
> > > 
> > ## Ivel afred
> > 
> > Does this mean that your model needs to be made public on Kaggle? Or is it okay to just make it public on Hugging Face.
> > 
> > 
> > 
> > > ## Yichuan Gao
> > > 
> > > You don't need to upload your model to huggingface, just upload it here on kaggle is ok. Also you can make it private (by default) and use it in your notebooks
> > > 
> > > 
> > > 
> > > ## Ivel afred
> > > 
> > > Code Requirements in LMSYS states: 'Freely&publicly available external data is allowed, including pre trained models.' Does this not require your models to be public? I'm a little confused
> > > 
> > > 
> > > 


---



</div>
<div class="column-right">

# 日本語訳

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



</div>