# 要約 
このディスカッションは、KaggleのLMSYS - Chatbot Arena Human Preference Predictionsコンペティションにおける、Gemma2 9bモデルとLlama3 8bモデルの推論時間の違いについて議論しています。

**主なポイント:**

* Dylan Liuは、Gemma2 9bモデルの推論時間がLlama3 8bモデルの約2倍であることを報告し、その理由を尋ねています。
* Ashwaniは、Gemma2がLlama3よりも25%ほど時間がかかることは経験しているものの、Dylan Liuほど大きな差は見ていないとコメントしています。
* Sparsh Tewatiaは、Gemma2がパラメータ数を少なく見積もっており、実際には102億のパラメータを持つことを指摘しています。また、Llama3がグループ化されたクエリアテンションを使用しているのに対し、Gemma2はセルフアテンションを使用しているため、速度の違いを説明できると述べています。
* Yichuan Gaoは、重みとcompute_dtypeのデータ型を確認することを提案しています。T4がbfloat16をサポートしていない場合、他の方法でエミュレートする必要があるため、大幅に遅くなる可能性があると説明しています。
* Valentin Wernerは、トレーニング時間もLlama3-8bよりも50%遅く、アーキテクチャに依存すると述べています。
* Robert0921は、Gemma2がLlama3よりも正確であるものの、推論時間が長いため、コンペティションでより良い結果を得ることができなかったとコメントしています。

**結論:**

このディスカッションでは、Gemma2 9bモデルの推論時間がLlama3 8bモデルよりも長い理由について、いくつかの可能性が示されています。パラメータ数の違い、アーキテクチャの違い、データ型の違いなどが考えられます。しかし、明確な理由はまだ特定されていません。

**今後の課題:**

* Gemma2 9bモデルの推論時間を短縮するための具体的な方法を調査する。
* Gemma2 9bモデルとLlama3 8bモデルのパフォーマンスを比較し、速度と精度のトレードオフを分析する。


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

# Gemma2 9b's inference time is much longer that Llama3 8b?

**Dylan Liu** *Wed Jul 17 2024 15:55:30 GMT+0900 (日本標準時)* (2 votes)

With same submission code, my Llama3 8b model takes ~4h to finish the inference, but my Gemma2 9b takes ~8h. Are you experiencing the same?



---

 # Comments from other users

> ## Ashwani
> 
> I haven't seen such difference. For me its 25% more time in gemma than lamma. 
> 
> If you want to further reduce inference time, check dynamic padding for each batch. 😀
> 
> 
> 


---

> ## Sparsh Tewatia
> 
> 2 billion parameters more at work my friend.
> 
> 
> 
> > ## Dylan LiuTopic Author
> > 
> > 2 billion parameters? I thought it was 1b different. But even so, double inference time is still not much explainable.
> > 
> > 
> > 
> > > ## Sparsh Tewatia
> > > 
> > > gemma always claims less parameter if you count it shows 10.2 billion parameters , also LLAMA 3 uses grouped query attention , and has around 120 K tokens in tokenizer while Gemma uses self attention and has 250 K tokens in tokenizer which can explain the difference in speed.
> > > 
> > > 
> > > 


---

> ## Yichuan Gao
> 
> I would check the data type for both weights and compute_dtype. If you are using bfloat16 in compute, it will be MUCH slower since T4 does not support bfloat16, and need to emulate it by other methods. In my experience, Gemma2 9b and Mistral 7b inference time does not have much a difference (3~4h range), provides using 4bit weights and float16 dtype.
> 
> 
> 


---

> ## Valentin Werner
> 
> For me, also training time with same parameters is 50% slower than Llama3-8b which seems insane. But its all in the architecture, as Sparsh pointed out.
> 
> 
> 
> > ## Robert0921
> > 
> > For LoRa, even though Gemma2 is more accurate than Llama3, I was unable to achieve better results due to the 9-hour time limit.
> > 
> > 
> > 


---

> ## Robert0921
> 
> Not only inference, but also training takes longer, because 9b>8b？
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# Gemma2 9b の推論時間が Llama3 8b よりも大幅に長いのはなぜですか？

**Dylan Liu** *2024年7月17日 水曜日 15:55:30 GMT+0900 (日本標準時)* (2票)

同じ提出コードで、Llama3 8b モデルの推論に約4時間かかりますが、Gemma2 9b は約8時間かかります。同じような経験をしていますか？
---
# 他のユーザーからのコメント
> ## Ashwani
> 
> 私はそのような違いを見たことがありません。私の場合、Gemma は Llama よりも 25% ほど時間がかかります。
> 
> 推論時間をさらに短縮したい場合は、各バッチの動的パディングを確認してください。😀
> 
> 
> 
---
> ## Sparsh Tewatia
> 
> 20億のパラメータが追加されているのです。
> 
> 
> 
> > ## Dylan Liu トピック作成者
> > 
> > 20億のパラメータですか？10億のパラメータの違いだと思っていました。しかし、推論時間が2倍になるのは、まだ説明がつきません。
> > 
> > 
> > 
> > > ## Sparsh Tewatia
> > > 
> > > Gemma は常にパラメータ数を少なく見積もっており、102億のパラメータを示しています。また、LLAMA 3 はグループ化されたクエリアテンションを使用しており、トークナイザーに約12万トークンがありますが、Gemma はセルフアテンションを使用しており、トークナイザーに25万トークンがあるため、速度の違いを説明できます。
> > > 
> > > 
> > > 
---
> ## Yichuan Gao
> 
> 重みと compute_dtype のデータ型を確認することをお勧めします。compute で bfloat16 を使用している場合、T4 は bfloat16 をサポートしていないため、他の方法でエミュレートする必要があるため、大幅に遅くなります。私の経験では、Gemma2 9b と Mistral 7b の推論時間はほとんど変わりません (3～4時間程度)。4ビットの重みと float16 のデータ型を使用しています。
> 
> 
> 
---
> ## Valentin Werner
> 
> 私の場合、同じパラメータでのトレーニング時間も Llama3-8b よりも 50% 遅く、信じられないほどです。しかし、Sparsh が指摘したように、すべてアーキテクチャに依存します。
> 
> 
> 
> > ## Robert0921
> > 
> > LoRa の場合、Gemma2 は Llama3 よりも正確ですが、9時間の時間制限のため、より良い結果を得ることができませんでした。
> > 
> > 
> > 
---
> ## Robert0921
> 
> 推論だけでなく、トレーニング時間も長くなります。なぜなら、9b > 8b だからですか？
> 
> 
> 
---



</div>