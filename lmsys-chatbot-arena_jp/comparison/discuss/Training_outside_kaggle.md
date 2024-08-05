# 要約 
このディスカッションは、Kaggleコンペティションで外部環境でトレーニングされたモデルを使用できるかどうかについてです。

Ahmad Al-Husainyは、コンペティションで大きな事前学習済みモデルを外部環境でトレーニングし、その重みを提出するためにアップロードできるかどうかを尋ねています。

Lorry Zouは、それが可能であると答えますが、コンペティションではインターネット接続なしで提出する必要があるため、いくつかの問題が発生する可能性があると指摘しています。

Valentin Wernerは、モデルをKaggleのデータセットまたはモデルとしてロードすることを提案し、使用されるモデルがオープンソースであることを確認する必要があると述べています。

Ivel afredは、モデルをKaggleで公開する必要があるのか、それともHugging Faceで公開するだけで良いのかを尋ねます。

Valentin Wernerは、Kaggleで非公開にして自分だけがアクセスできるようにしておけば問題ないと答えます。Hugging Faceで公開する必要はありません。重要なのは、ファインチューニングするモデルが他の人にも利用可能であることです。

Ahmad Al-Husainyは、Google Colabでモデルをトレーニングし、最適なモデルの重みを抽出し、Kaggleでモデルを再構築して重みをロードしてテストデータセットで予測を行い、結果を提出することを検討していると説明します。

Valentin Wernerは、それが正しいアプローチであると述べています。

Marília Prataは、それがコンペティションのルールによって異なる可能性があると指摘し、Paul Mooney、Sohier Dane、またはAddison Howardが答えてくれるかもしれないと述べています。

このディスカッションは、コンペティションのルールが明確でないため、外部環境でトレーニングされたモデルを使用できるかどうかについて、参加者間で混乱があることを示しています。


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

# Training outside kaggle

**Ahmad Al-Husainy** *Sun Jun 16 2024 04:30:02 GMT+0900 (日本標準時)* (3 votes)

Hello, this is my first competition, and I'm curious to know if it's possible to train large pre-trained models in an external environment and then simply upload the weights for submission. 



---

 # Comments from other users

> ## Lorry Zou
> 
> You definitely can do that. It's also what I'm doing. However, since this competition requires internet-off submission, I'm sure I will run into some issues…
> 
> 
> 
> > ## Valentin Werner
> > 
> > Just load it as a kaggle dataset or kaggle model!
> > 
> > You only have to make sure the models you are using are open source. 
> > 
> > 
> > 
> > > ## Ivel afred
> > > 
> > > Does this mean that your model needs to be public on Kaggle? Or it's okay to just make it public on Hugging Face.
> > > 
> > > 
> > > 
> > > ## Valentin Werner
> > > 
> > > It can be private on kaggle, just available for you. You dont have to make it public on huggingface either. Its just important that the model that you finetune is also available for others. (e.g., DeBERTa or Llama are open source; GPT-4 is not - if you finetune GPT-4 for the competition, that would be not fair and you would have to make your GPT-4 tuned model available for everybody in the competition instead (I think))
> > > 
> > > 
> > > 
> > > ## Ivel afred
> > > 
> > > thanks, that helps me a lot
> > > 
> > > 
> > > 
> > ## Ahmad Al-HusainyTopic Author
> > 
> > Thank you for your comment. I want to clarify my approach: I'm currently using Google Colab for model development. When I attempt to train the models on Kaggle, I encounter GPU memory issues and other problems related to the Kaggle environment it self, even though the same code runs smoothly on Colab. I'm considering training the model in Colab and then extracting the best model weights. My plan is to rebuild the model on Kaggle, load the weights, predict on the test dataset, and submit my results. Additionally, the environment on Colab is more extensive than on Kaggle, so training on Kaggle could potentially exceed the 9-hour limit.
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > That is the correct approach
> > > 
> > > 
> > > 


---

> ## Marília Prata
> 
> I think it depends on each competition rules. Though I'm not certain. Maybe Paul Mooney, Sohier Dane or Addison Howard could answer that.
> 
> By the way, welcome to your 1st competition.
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

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



</div>