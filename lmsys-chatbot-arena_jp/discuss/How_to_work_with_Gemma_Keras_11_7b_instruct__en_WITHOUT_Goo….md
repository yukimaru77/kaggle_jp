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

