# 要約 
## ディスカッション要約: LlamaForSequenceClassification のランダムな分類層の重み

このディスカッションは、Llama3 を GPU で微調整する際に、分類層の重みがランダムに初期化される問題について議論しています。

**問題:**

* ユーザーは、LlamaForSequenceClassification モデルの分類層の重みが、トレーニングのたびに異なる値になることに気づきました。
* 保存したアダプターの重みをロードしても、重みが一致しません。

**原因:**

* 重みの初期化はランダムに行われるため、トレーニングのたびに異なる値になります。
* LoRA の保存方法によっては、間違った重みが保存される可能性があります。

**解決策:**

* **ランダムシードを設定:** トレーニングのたびに同じ初期値を得るために、ランダムシードを設定します。
* **LoRA のカスタム保存:** LoRA を適切に保存する必要があります。

**結論:**

このディスカッションは、Llama3 を微調整する際に、分類層の重みを安定させるための方法について議論しています。ランダムシードの設定と LoRA の適切な保存が、この問題を解決するのに役立ちます。


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

# [Question] Confused with random classification layer weight(score.weight) for LlamaForSequenceClassification

**Xuhang_CN** *Sat Jul 20 2024 19:07:52 GMT+0900 (日本標準時)* (0 votes)

Hi , I am a freshman for llm. I want to SFT llama3 in my GPU.

When I check for the same train environment, I find classification layer weight is initialized randomly(maybe?):

When I run below code first time and second time, I get different score.weight.

model_raw = LlamaForSequenceClassification.from_pretrained(
    model_name,
    quantization_config=quantization_config,
    num_labels=3,
    device_map='auto'
model = prepare_model_for_kbit_training(model)
config = PeftConfig.from_pretrained(finetune_model_name)
model = PeftModel.from_pretrained(model, finetune_model_name,is_trainable=False)
)

Even if I load saved adapter weight, weight is still not the same.

So I want to know how to make sure I train llama3 in my GPU and upload adapter in kaggle to make sure I get the same model.

Thanks!



---

 # Comments from other users

> ## Valentin Werner
> 
> You could set the seed for the run. That way you always get the same initial values. Make sure versions are similar / identical between kaggle notebook and local. There are plenty of "seed all" functions on kaggle and google that you can use
> 
> 
> 


---

> ## hn
> 
> You may need to do a custom save LoRA as some combinations may render the LoRA saving the wrong weights.
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

## [質問] LlamaForSequenceClassification のランダムな分類層の重み (score.weight) について

**Xuhang_CN** *2024年7月20日 土曜日 19:07:52 JST* (0票)

こんにちは、LLM初心者です。GPU で Llama3 を微調整したいと思っています。

同じトレーニング環境で確認したところ、分類層の重みがランダムに初期化されているようです (多分？):

以下のコードを初めて実行したときと2回目で、異なる score.weight を取得します。

```python
model_raw = LlamaForSequenceClassification.from_pretrained(
    model_name,
    quantization_config=quantization_config,
    num_labels=3,
    device_map='auto'
)
model = prepare_model_for_kbit_training(model)
config = PeftConfig.from_pretrained(finetune_model_name)
model = PeftModel.from_pretrained(model, finetune_model_name,is_trainable=False)
```

保存したアダプターの重みをロードしても、重みが同じになりません。

そこで、GPU で Llama3 をトレーニングして、アダプターを Kaggle にアップロードし、同じモデルを取得する方法を知りたいと思っています。

よろしくお願いします！

---

## 他のユーザーからのコメント

> ## Valentin Werner
> 
> ランのシードを設定することができます。そうすれば、常に同じ初期値が得られます。Kaggle のノートブックとローカルのバージョンが類似しているか、同一であることを確認してください。Kaggle や Google で使用できる「seed all」関数はたくさんあります。
> 
> 
> 
---
> ## hn
> 
> LoRA をカスタムで保存する必要があるかもしれません。組み合わせによっては、LoRA が間違った重みを保存してしまう場合があります。
> 
> 
> 
--- 



</div>