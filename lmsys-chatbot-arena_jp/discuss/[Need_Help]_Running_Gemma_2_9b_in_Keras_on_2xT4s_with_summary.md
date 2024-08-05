# 要約 
このディスカッションは、KaggleのLMSYS - Chatbot Arena Human Preference Predictionsコンペティションにおいて、参加者Pranshu BahadurがGemma 2 9bモデルをTPUでトレーニングし、推論を実行する際に直面した問題について、他の参加者からの助けを求めているものです。

Pranshu Bahadurは、TPUでトレーニングするためのノートブックを作成しましたが、コンペティションでは提出にTPUの使用が許可されていないため、推論を実行する際に問題が発生しました。

他の参加者からのコメントでは、Pranshu Bahadurは推論を実行するために、デバイスの割り当て、カスタム予測ループ、set_floatx('float16')を使用し、量子化は必要なかったことを明らかにしています。

このディスカッションは、コンペティション参加者が直面する技術的な課題を共有し、互いに助け合うための場として機能していることを示しています。


---
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
