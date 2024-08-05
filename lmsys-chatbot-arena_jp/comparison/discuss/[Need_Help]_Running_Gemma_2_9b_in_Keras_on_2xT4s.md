# 要約 
このディスカッションは、KaggleのLMSYS - Chatbot Arena Human Preference Predictionsコンペティションにおいて、参加者Pranshu BahadurがGemma 2 9bモデルをTPUでトレーニングし、推論を実行する際に直面した問題について、他の参加者からの助けを求めているものです。

Pranshu Bahadurは、TPUでトレーニングするためのノートブックを作成しましたが、コンペティションでは提出にTPUの使用が許可されていないため、推論を実行する際に問題が発生しました。

他の参加者からのコメントでは、Pranshu Bahadurは推論を実行するために、デバイスの割り当て、カスタム予測ループ、set_floatx('float16')を使用し、量子化は必要なかったことを明らかにしています。

このディスカッションは、コンペティション参加者が直面する技術的な課題を共有し、互いに助け合うための場として機能していることを示しています。


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

# [Need Help] Running Gemma 2 9b in Keras on 2xT4s

**Pranshu Bahadur** *Mon Jul 22 2024 12:28:59 GMT+0900 (日本標準時)* (3 votes)

Hey guys!

I made this notebook to train Gemma 2 9b on TPUs.

But the competition doesn't allow TPUs for submission….which is a bit awkward haha

So I'm enlisting your help to figure this out!

Would really appreciate any feedback, I am looking to learn!

Training nb (~3 hrs for 1 epoch):

[https://www.kaggle.com/code/pranshubahadur/tf-gemma-2-9b-lmsys-training-tpu](https://www.kaggle.com/code/pranshubahadur/tf-gemma-2-9b-lmsys-training-tpu)

Unsolved inference nb:

[https://www.kaggle.com/code/pranshubahadur/unsolved-inference-tf-gemma-2-9b-lmsys](https://www.kaggle.com/code/pranshubahadur/unsolved-inference-tf-gemma-2-9b-lmsys)



---

 # Comments from other users

> ## Pranshu BahadurTopic Author
> 
> Update: Inference works now, out of tpu quota will update on saturday
> 
> 
> 
> > ## Somesh88
> > 
> > what did you do to make inference run?
> > 
> > 
> > 
> > > ## Pranshu BahadurTopic Author
> > > 
> > > mainly device allocation followed by a custom prediction loop and set_floatx('float16')
> > > 
> > > no quantization was needed 
> > > 
> > > you can check out my inference nb linked above
> > > 
> > > 
> > > 


---



</div>
<div class="column-right">

# 日本語訳

# [助けが必要] Keras で 2xT4 上で Gemma 2 9b を実行する
**Pranshu Bahadur** *2024年7月22日 月曜日 12:28:59 GMT+0900 (日本標準時)* (3票)

皆さん、こんにちは！

Gemma 2 9b を TPU でトレーニングするためのノートブックを作成しました。
しかし、このコンペティションでは提出に TPU を使用することが許可されていません…ちょっと奇妙ですね、笑
そこで、皆さんのお力をお借りして解決策を見つけたいと思います！

フィードバックをいただけたら幸いです。学習したいと思っています！

トレーニングノートブック（1エポックあたり約3時間）：
[https://www.kaggle.com/code/pranshubahadur/tf-gemma-2-9b-lmsys-training-tpu](https://www.kaggle.com/code/pranshubahadur/tf-gemma-2-9b-lmsys-training-tpu)

未解決の推論ノートブック：
[https://www.kaggle.com/code/pranshubahadur/unsolved-inference-tf-gemma-2-9b-lmsys](https://www.kaggle.com/code/pranshubahadur/unsolved-inference-tf-gemma-2-9b-lmsys)

---
# 他のユーザーからのコメント
> ## Pranshu Bahadur トピック作成者
> 
> 更新：推論が動作するようになりました。TPU クォータを使い果たしたので、土曜日に更新します。
> 
> 
> 
> > ## Somesh88
> > 
> > 推論を実行するために何を行いましたか？
> > 
> > 
> > 
> > > ## Pranshu Bahadur トピック作成者
> > > 
> > > 主にデバイスの割り当て、それに続くカスタム予測ループと set_floatx('float16') です。
> > > 
> > > 量子化は必要ありませんでした。
> > > 
> > > 上記にリンクされている推論ノートブックを確認できます。
> > > 
> > > 
> > > 
---



</div>