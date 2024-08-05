# 要約 
このディスカッションは、KaggleのLMSYS - Chatbot Arena Human Preference Predictionsコンペティションにおいて、unslothというライブラリを使用することについて議論しています。

Varun Jagannathは、unslothがトレーニングと推論を高速化すると聞いて、コンペティションでunslothを使ったことがあるかどうか尋ねています。

Ivan VybornovとCristóbal Mackenzieは、unslothは分類器をサポートしていないため、このコンペティションでは役に立たないと指摘しています。

Varun Jagannathは、プロンプトを与えてモデルにクラスを予測させる方法を試すことを提案しますが、Takamichi Todaは、CausalLMのヘッダーでトークンA、B、タイの生成確率を予測として使用できることを示唆しています。

Varun Jagannathは、この方法を試しましたが、常に1つのクラスに予測または重み付けされると指摘しています。Takamichi Todaは、分類ヘッドが生成ヘッドよりも良い結果を出していることを認め、ファインチューニングで改善できるかどうか試行錯誤していることを述べています。

このディスカッションは、unslothが現在のところこのコンペティションでは役に立たないことを示唆しており、参加者は代わりにCausalLMの生成確率を使用したり、分類ヘッドをファインチューニングしたりするなどの他の方法を試す必要があることを示しています。


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

# Usage of unsloth

**Varun Jagannath** *Mon Jul 08 2024 01:16:33 GMT+0900 (日本標準時)* (0 votes)

Has anyone used unsloth in the competition as it says that training and inferencing is much with it. Looking forward for suggestions.



---

 # Comments from other users

> ## Ivan Vybornov
> 
> They do not have kernels for classifier yet.
> 
> 
> 
> > ## Cristóbal Mackenzie
> > 
> > Exactly, and I think the "axolotl" library which is also being very widely used doesn't support classification models yet.
> > 
> > 
> > 
> > ## Varun JagannathTopic Author
> > 
> > ok, thanks for the input. But do you think it would be too much of a task if we give prompts and then ask model to predict the classes.
> > 
> > 
> > 
> > ## Takamichi Toda
> > 
> > In the CausalLM header can use the probabilities of generation of tokens A, B and tie as predictions.
> > 
> > ```
> > inputs = tokenizer(text)
> > out = model(inputs)
> > pred_token_id = tokenizer.encode("A") + tokenizer.encode("B") + tokenizer.encode("tie")
> > pred = out.logits[0, -1, pred_token_id].softmax(0)
> > 
> > ```
> > 
> > 
> > 
> > > ## Varun JagannathTopic Author
> > > 
> > > Tried this method as well, but it always predicts or weighs towards one class. Even I have checked your notebook. Model A is always having higher weight. I guess the classification head is working well in this competition.
> > > 
> > > 
> > > 
> > > ## Takamichi Toda
> > > 
> > > In my experiment as well, the classification head has been producing better results so far. I am currently in the process of trial and error to see if improvements can be made with fine-tuning (in [this discussion](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/520470#2925128), it seems they were able to achieve 0.902 with the generation head).
> > > 
> > > 
> > > 


---



</div>
<div class="column-right">

# 日本語訳

# unslothの使用について

**Varun Jagannath** *2024年7月8日 月曜日 01:16:33 GMT+0900 (日本標準時)* (0票)

このコンペティションでunslothを使った人はいますか？トレーニングと推論が非常に高速になるとのことですが、何か提案があれば教えてください。

---
# 他のユーザーからのコメント

> ## Ivan Vybornov
> 
> まだ分類器用のカーネルがありません。
> 
> 
> 
> > ## Cristóbal Mackenzie
> > 
> > その通りですね。また、広く使われている「axolotl」ライブラリも、まだ分類モデルをサポートしていません。
> > 
> > 
> > 
> > ## Varun Jagannathトピック作成者
> > 
> > 了解しました。ご意見ありがとうございます。しかし、プロンプトを与えてモデルにクラスを予測させると、あまりにも大変な作業になるでしょうか？
> > 
> > 
> > 
> > ## Takamichi Toda
> > 
> > CausalLMのヘッダーでは、トークンA、B、タイの生成確率を予測として使用できます。
> > 
> > ```
> > inputs = tokenizer(text)
> > out = model(inputs)
> > pred_token_id = tokenizer.encode("A") + tokenizer.encode("B") + tokenizer.encode("tie")
> > pred = out.logits[0, -1, pred_token_id].softmax(0)
> > 
> > ```
> > 
> > 
> > 
> > > ## Varun Jagannathトピック作成者
> > > 
> > > この方法も試しましたが、常に1つのクラスに予測または重み付けされます。あなたのノートブックも確認しましたが、モデルAは常に高い重みを持っています。このコンペティションでは、分類ヘッドがうまく機能していると思います。
> > > 
> > > 
> > > 
> > > ## Takamichi Toda
> > > 
> > > 私の実験でも、分類ヘッドはこれまでより良い結果を出しています。現在、ファインチューニングで改善できるかどうか試行錯誤しているところです（[このディスカッション](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/520470#2925128)では、生成ヘッドで0.902を達成できたようです）。
> > > 
> > > 
> > > 
---



</div>