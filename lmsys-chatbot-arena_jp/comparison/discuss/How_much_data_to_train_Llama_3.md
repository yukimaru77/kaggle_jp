# 要約 
このディスカッションは、KaggleコンペティションにおけるLlama 3のトレーニングデータ量に関するものです。

**ano**は、トレーニングデータの半分をトレーニングに、半分を検証に使用し、CVスコアが0.968、LBスコアが0.979であることを共有し、トレーニングデータ量と精度の関係について質問しています。

**James Day**は、トレーニングサンプルを増やすことで精度の向上を大幅に達成できる可能性があり、提供されたデータの50%でモデルが飽和しているとは考えられないと回答しています。彼は、データが十分に高品質であれば、より多くのデータを追加することはほとんど常に有益であると述べています。

**ano**は、James Dayの回答を受け、トレーニングデータを追加し、パラメータを変更することで最適化を試みることを表明しています。

**Cody_Null**は、James Dayがトレーニングデータから新しいデータを作成しているかどうかを質問しています。

**James Day**は、コンペティション終了までは追加データの入手元については詳しく説明したくないと回答しています。

**Sparsh Tewatia**は、James Dayの回答に同意し、賢い人ならそれで十分だとコメントしています。

**要約:**

このディスカッションは、KaggleコンペティションにおけるLlama 3のトレーニングデータ量と精度の関係について議論しています。参加者たちは、トレーニングデータ量を増やすことで精度の向上を大幅に達成できる可能性があることに同意しています。しかし、コンペティション終了までは、追加データの入手元については詳しく説明されていません。


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

# How much data to train Llama 3?

**ano** *Thu Jul 11 2024 08:00:45 GMT+0900 (日本標準時)* (3 votes)

How much data are you using for training Llama 3? I use half of all the given training data for training and the other half as validation data, with cv: 0.968, lb: 0.979.

I want to know about the relationship between the amount of training data and accuracy. I remember reading a discussion somewhere that said using all the data for training does not change the score, but I lost track of that discussion.



---

 # Comments from other users

> ## James Day
> 
> Hesitant to share details about my experiments until the end of the competition, but it is possible to achieve significant accuracy improvements by scaling from tens of thousands of training examples to hundreds of thousands, so I would not expect your models to be saturating at 50% of the data we received from the competition organizers. Using more than 200% is better than 80%. I never scaled down to only training on 50%.
> 
> Broadly speaking, my intuition is that adding more data is almost always beneficial (albeit with diminishing returns) so long as that data is sufficiently high quality (not too repetitive, mislabeled, or different from the test data) and your model has sufficiently high capacity to learn from that data (which shouldn't be a problem for Llama 3 8B with a decent LoRA config).
> 
> 
> 
> > ## anoTopic Author
> > 
> > Thank you for the valuable information! It seems I was mistaken in thinking that a small amount of training data would be sufficient. I'll try optimizing by adding training data (including external data) and changing the parameters.
> > 
> > 
> > 
> > ## Cody_Null
> > 
> > You have already shared a friendly amount of information so feel free to hold back, are you generating new data from the training data?
> > 
> > 
> > 
> > > ## James Day
> > > 
> > > I don't want to elaborate on where my extra data came from until the end of the competition. 🤐
> > > 
> > > 
> > > 
> > > ## Sparsh Tewatia
> > > 
> > > Thats enough for the smart one to know. 😀
> > > 
> > > 
> > > 


---



</div>
<div class="column-right">

# 日本語訳

## Llama 3のトレーニングデータ量について

**ano** *2024年7月11日 08:00:45 (日本標準時)* (3票)

Llama 3のトレーニングにどのくらいのデータを使用していますか？私は提供されたトレーニングデータの半分をトレーニングに、もう半分を検証データに使用しており、CVは0.968、LBは0.979です。

トレーニングデータ量と精度の関係について知りたいです。以前どこかで、すべてのデータを使ってトレーニングしてもスコアは変わらないという議論を読んだのですが、その議論を見失ってしまいました。

---

## 他のユーザーからのコメント

> ## James Day
> 
> コンペティション終了までは実験の詳細を共有することに躊躇していますが、トレーニングサンプルを数万から数十万に増やすことで、精度の向上を大幅に達成できる可能性があります。そのため、提供されたデータの50%でモデルが飽和しているとは考えられません。200%以上を使用する方が80%よりも優れています。私はトレーニングデータを50%に減らすことは一度もありませんでした。
> 
> 広く言えば、私の直感では、データが十分に高品質（あまり重複がなく、誤ってラベル付けされておらず、テストデータと大きく異ならない）であり、モデルがそのデータから学習するのに十分な能力を持っている限り（Llama 3 8Bで適切なLoRA設定があれば問題ないはずです）、より多くのデータを追加することはほとんど常に有益です（ただし、収穫逓減はあります）。
> 
> 
> 
> > ## anoTopic Author
> > 
> > 有益な情報ありがとうございます！少量のトレーニングデータで十分だと考えていたのは間違いだったようです。トレーニングデータ（外部データを含む）を追加し、パラメータを変更することで最適化を試みます。
> > 
> > 
> > 
> > ## Cody_Null
> > 
> > 既に十分な情報を共有してくれているので、遠慮なく教えてください。トレーニングデータから新しいデータを作成していますか？
> > 
> > 
> > 
> > > ## James Day
> > > 
> > > コンペティション終了までは、追加データの入手元については詳しく説明したくありません。🤐
> > > 
> > > 
> > > 
> > > ## Sparsh Tewatia
> > > 
> > > 賢い人ならそれで十分でしょう。😀
> > > 
> > > 
> > > 
--- 



</div>