# Kaggle外部でのトレーニングについて

**Ahmad Al-Husainy** *2024年6月16日日曜日 04:30:02 GMT+0900 (日本標準時)* (3票)

こんにちは。初めてのコンペティションに参加します。大きな事前学習済みモデルを外部環境でトレーニングし、その重みを提出するためにアップロードすることは可能でしょうか？

---
# 他のユーザーからのコメント

> ## Lorry Zou
> 
> 可能です。私もそうしています。ただし、このコンペティションではインターネット接続なしで提出する必要があるため、いくつか問題が発生すると思います…
> 
> 
> 
> > ## Valentin Werner
> > 
> > Kaggleのデータセットまたはモデルとしてロードしてください！
> > 
> > 使用するモデルがオープンソースであることを確認するだけです。
> > 
> > 
> > > ## Ivel afred
> > > 
> > > つまり、モデルをKaggleで公開する必要があるのでしょうか？それともHugging Faceで公開するだけで良いのでしょうか？
> > > 
> > > 
> > > 
> > > ## Valentin Werner
> > > 
> > > Kaggleで非公開にして、自分だけがアクセスできるようにしておけば問題ありません。Hugging Faceで公開する必要もありません。重要なのは、ファインチューニングするモデルが他の人にも利用可能であることです。（例えば、DeBERTaやLlamaはオープンソースです。GPT-4はオープンソースではありません。GPT-4をコンペティション用にファインチューニングした場合、それは不公平であり、GPT-4をファインチューニングしたモデルをコンペティションの参加者全員が利用できるようにする必要があります（たぶん））
> > > 
> > > 
> > > 
> > > ## Ivel afred
> > > 
> > > ありがとうございます。とても役に立ちました。
> > > 
> > > 
> > > 
> > ## Ahmad Al-Husainyトピック作成者
> > 
> > コメントありがとうございます。私のアプローチを明確にしたいと思います。現在、モデル開発にはGoogle Colabを使用しています。Kaggleでモデルをトレーニングしようとすると、GPUメモリの問題やKaggle環境自体の問題が発生します。同じコードがColabではスムーズに実行されるにもかかわらずです。Colabでモデルをトレーニングし、最適なモデルの重みを抽出することを検討しています。Kaggleでモデルを再構築し、重みをロードしてテストデータセットで予測を行い、結果を提出する予定です。さらに、Colabの環境はKaggleよりも広範であるため、Kaggleでのトレーニングは9時間の制限を超える可能性があります。
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > それが正しいアプローチです。
> > > 
> > > 
> > > 
---
> ## Marília Prata
> 
> 私は、それはコンペティションのルールによって異なると思います。確信はありません。Paul Mooney、Sohier Dane、またはAddison Howardが答えてくれるかもしれません。
> 
> ちなみに、初めてのコンペティションへようこそ。
> 
> 
> 
---
