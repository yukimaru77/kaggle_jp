# 要約 
このディスカッションは、Kaggle の LMSYS - Chatbot Arena 人間による好み予測チャレンジに参加しているユーザー、Marília Prata が、Gemma Keras 1.1_7b instruct_en モデルを使用する際にメモリ不足の問題に直面していることから始まります。

Marília は、バッチサイズを減らし、環境変数を調整し、コードの行数を減らすなど、いくつかの解決策を試しましたが、問題は解決しませんでした。彼女は、Google Cloud を使用せずに Gemma Keras 1.1_7b instruct_en を使用する方法を探しています。

他のユーザーからのコメントでは、バッチサイズをさらに減らすこと、混合精度を使用すること、メモリフラクションを下げること、より小さなモデルを使用すること、勾配累積を使用することなどが提案されています。

Marília は、バッチサイズがすでに 1 であること、そして最終的に Gemma Keras 1.1_2b_instruct_en に切り替えたことを明らかにしています。これは、コンテストのホストが 7b モデルを固定しているため、彼女は 7b モデルを使用する必要があるためです。

このディスカッションは、Kaggle コンテストで大きな言語モデルを使用する際に発生する可能性のあるメモリ不足の問題と、その問題を解決するためのさまざまなアプローチについて議論しています。


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

# How to work with Gemma Keras 1.1_7b instruct _en WITHOUT Google Cloud? On the 1.1_2b_instruct_en No Memory issue.

**Marília Prata** *Fri May 10 2024 10:43:46 GMT+0900 (日本標準時)* (17 votes)

I'm facing some memory issue with Gemma Keras 1.1 -7b- instruct-en.  It appeared that message "Your notebook tried to allocate more memory than is available. It has restarted".   Go to Google Cloud or dismiss it.

I even ran:

os.environ["XLA_PYTHON_CLIENT_PREALLOCATE"]="false"

  os.environ["XLA_PYTHON_CLIENT_MEM_FRACTION"]=".XX"

  os.environ["XLA_PYTHON_CLIENT_ALLOCATOR"]="platform"

Besides, I reduced the number of rows.

When I ran GemmaCausalLM the message that "The notebook tried to allocate more memory than is available" popped-up.

# Is there a way to work with Gemma Keras 1.1- 7b instruct -en WITHOUT  Google Cloud?

For the record, that doesn't occur on the other 7b models (7 billion parameters) that were pinned on this LMSYS competition.

Fortunately, I found Awsaf's code and published my 1st (Gemma 1.1-7b-instruct-en just 34 min. ago on May 10, 2024)

[Gemma 1.1 7B Int8 Load](https://www.kaggle.com/code/awsaf49/gemma-1-1-7b-int8-load) By Awsaf.

Thanks in advance,

Marília. 



---

 # Comments from other users

> ## Adnan Alaref
> 
> Hi [@mpwolke](https://www.kaggle.com/mpwolke) ,try to reduce batch size,restart the kernel
> 
> 
> 
> > ## Marília PrataTopic Author
> > 
> > My  batch_size = 1    Could it be lower? Zero or negative 😆
> > 
> > 
> > 


---

> ## Kaizhao Liang
> 
> I don't think we could load any pretrained model bigger than 1B, since the RAM runs out.
> 
> 
> 
> > ## Marília PrataTopic Author
> > 
> > I don't know how the model works on a submission due to its memory. However, I was facing issues even without submitting. Just at the beginning of the code.
> > 
> > Fortunately, I found Awsaf's code: [Gemma 1.1 7B Int8 Load](https://www.kaggle.com/code/awsaf49/gemma-1-1-7b-int8-load) and published my 1st (Gemma 1.1-7b-instruct-en just 34 min. ago)
> > 
> > Thank you Kaizhao.
> > 
> > 
> > 


---

> ## Matin Mahmoudi ✨
> 
> Try reducing the batch size, using mixed precision (float16), or lowering the memory fraction to handle Gemma Keras 1.1-7b. If that doesn't work, maybe go for a smaller model or use gradient accumulation [@mpwolke](https://www.kaggle.com/mpwolke).
> 
> 
> 
> > ## Marília PrataTopic Author
> > 
> > Hi Matin,
> > 
> > The batch size is only 1.
> > 
> > I changed to Gemma Keras 1.1_2b_instruct_en to reach at the end of the code (instead of the 7b).
> > 
> > Though the hosts pinned the 7b.
> > 
> > Thank you.
> > 
> > 
> > 


---



</div>
<div class="column-right">

# 日本語訳

## Gemma Keras 1.1_7b instruct_en を Google Cloud なしで使う方法について、1.1_2b_instruct_en のメモリ不足問題

**Marília Prata** *2024年5月10日 金曜日 10:43:46 GMT+0900 (日本標準時)* (17票)

Gemma Keras 1.1 -7b- instruct-en でメモリ不足の問題に直面しています。  「ノートブックが使用可能なメモリを超えるメモリを割り当てようとしています。ノートブックは再起動されます。」というメッセージが表示されました。  Google Cloud に移動するか、無視してください。

以下を実行しました。

```python
os.environ["XLA_PYTHON_CLIENT_PREALLOCATE"]="false"
os.environ["XLA_PYTHON_CLIENT_MEM_FRACTION"]=".XX"
os.environ["XLA_PYTHON_CLIENT_ALLOCATOR"]="platform"
```

さらに、行数を減らしました。

GemmaCausalLM を実行すると、「ノートブックが使用可能なメモリを超えるメモリを割り当てようとしています。」というメッセージが表示されました。

# Google Cloud なしで Gemma Keras 1.1- 7b instruct -en を使う方法はありますか？

記録として、この LMSYS コンテストで固定された他の 7b モデル（70億パラメータ）では、この問題は発生していません。

幸いなことに、Awsaf のコードを見つけて、私の最初の（Gemma 1.1-7b-instruct-en、2024年5月10日 34分前）を公開しました。
[Gemma 1.1 7B Int8 Load](https://www.kaggle.com/code/awsaf49/gemma-1-1-7b-int8-load) Awsaf によって。

事前に感謝します。
Marília. 

---
# 他のユーザーからのコメント

> ## Adnan Alaref
> 
> [@mpwolke](https://www.kaggle.com/mpwolke) さん、バッチサイズを減らして、カーネルを再起動してみてください。
> 
> 
> 
> > ## Marília Prataトピック作成者
> > 
> > 私の `batch_size = 1` です。もっと小さくできますか？ゼロか負の数ですか？😆
> > 
> > 
> > 
---
> ## Kaizhao Liang
> 
> RAM が不足するため、1B を超える事前学習済みモデルをロードすることはできないと思います。
> 
> 
> 
> > ## Marília Prataトピック作成者
> > 
> > モデルがメモリのためにどのように提出時に動作するのかわかりません。しかし、提出せずに問題に直面していました。コードの最初で。
> > 
> > 幸いなことに、Awsaf のコードを見つけました：[Gemma 1.1 7B Int8 Load](https://www.kaggle.com/code/awsaf49/gemma-1-1-7b-int8-load) そして私の最初の（Gemma 1.1-7b-instruct-en、34分前）を公開しました。
> > 
> > Kaizhao さん、ありがとうございます。
> > 
> > 
> > 
---
> ## Matin Mahmoudi ✨
> 
> バッチサイズを減らし、混合精度（float16）を使用するか、メモリフラクションを下げて Gemma Keras 1.1-7b を処理してみてください。それでもうまくいかない場合は、より小さなモデルを使用するか、勾配累積を使用してください [@mpwolke](https://www.kaggle.com/mpwolke)。
> 
> 
> 
> > ## Marília Prataトピック作成者
> > 
> > Matin さん、こんにちは。
> > 
> > バッチサイズは 1 です。
> > 
> > 7b ではなく、コードの最後まで到達するために Gemma Keras 1.1_2b_instruct_en に変更しました。
> > 
> > ホストは 7b を固定していますが。
> > 
> > ありがとうございます。
> > 
> > 
> > 
---



</div>