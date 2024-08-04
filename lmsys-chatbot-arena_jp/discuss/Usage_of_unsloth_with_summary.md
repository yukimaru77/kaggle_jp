# 要約 
このディスカッションは、KaggleのLMSYS - Chatbot Arena Human Preference Predictionsコンペティションにおいて、unslothというライブラリを使用することについて議論しています。

Varun Jagannathは、unslothがトレーニングと推論を高速化すると聞いて、コンペティションでunslothを使ったことがあるかどうか尋ねています。

Ivan VybornovとCristóbal Mackenzieは、unslothは分類器をサポートしていないため、このコンペティションでは役に立たないと指摘しています。

Varun Jagannathは、プロンプトを与えてモデルにクラスを予測させる方法を試すことを提案しますが、Takamichi Todaは、CausalLMのヘッダーでトークンA、B、タイの生成確率を予測として使用できることを示唆しています。

Varun Jagannathは、この方法を試しましたが、常に1つのクラスに予測または重み付けされると指摘しています。Takamichi Todaは、分類ヘッドが生成ヘッドよりも良い結果を出していることを認め、ファインチューニングで改善できるかどうか試行錯誤していることを述べています。

このディスカッションは、unslothが現在のところこのコンペティションでは役に立たないことを示唆しており、参加者は代わりにCausalLMの生成確率を使用したり、分類ヘッドをファインチューニングしたりするなどの他の方法を試す必要があることを示しています。


---
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

