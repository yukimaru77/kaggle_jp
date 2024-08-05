# 要約 
このディスカッションは、Kaggleの計算リソースが、LMSYS - Chatbot Arena Human Preference PredictionsコンペティションでLlama 3 8Bのような大規模言語モデルをファインチューニングするのに十分かどうかについて議論しています。

参加者たちは、Kaggleの計算リソースではファインチューニングに時間がかかりすぎるため、RTX 4090のような高性能なGPUをレンタルする必要があると結論付けています。KaggleのTPUはファインチューニングに使用できますが、それでもRTX 4090よりも時間がかかります。

コンペティションで勝つことを目指す場合は、Kaggleの計算リソースでは難しいかもしれません。しかし、学ぶために参加している場合は、Kaggleの計算リソースで動作するソリューションを考案することができます。

要約すると、このディスカッションは、コンペティションで成功するためには、強力な計算リソースが必要であることを示しています。Kaggleの計算リソースは、学習には十分ですが、最先端のモデルをファインチューニングするには不十分です。


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

# Is the Kaggle provided compute enough to join this competition?

**Andreas Bisi** *Tue May 28 2024 13:29:59 GMT+0900 (日本標準時)* (5 votes)

After participating in the Home Credit competition, I am looking forward to joining a new one. The objective of this new competition seems interesting. From a quick look at public notebooks, it appears that two popular models are LightGBM and Llama 3 8B. For the latter, is it possible to do any fine-tuning on Kaggle, or will I need to rent A100 instances?



---

 # Comments from other users

> ## Ivan Vybornov
> 
> I would not recommend finetuning on kaggle, from my experience finetuning llama with QLoRA on TPU is extremely painful timewise therefore I had to rent a RTX 4090, which does the job roughly for 8 hours.
> 
> 
> 
> > ## Dr. Gopalashivabalasubramanium Chandrashekaran
> > 
> > Thank you for your input. In your experience, how much more time will fine tuning on kaggle take vs your RTX 4090's 8 hours? Will it take 2-3x longer? I don't want to rent a RTX 4090 lol
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > Agreed on paying for Experiments. I think 2-4x is realistic. If I remember correctly, peft llama3 for some epochs took about 20 hours on kaggle and ca 8 hours on 4090. Main reason is that you can only use 2x T4 for this, which are even slower.
> > > 
> > > 
> > > 


---

> ## Kishan Vavdara
> 
> You can use kaggle TPU's for finetuning. 
> 
> 
> 


---

> ## bogoconic1
> 
> I would not advise using Kaggle compute to fine tune, unless you don’t have another choice. Quick experiments with small turnaround is beneficial in a competition and using a faster GPU like A100 helps. Also, in Kaggle, you only have 30 GPU hours + 20 TPU hours (if you know how to use it) per week
> 
> 
> 


---

> ## Valentin Werner
> 
> If you are only playing to win, then it might not work on kaggle compute. If you are here to learn, embrace the challenge and try to come up with solutions that work with the kaggle compute.
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# Kaggleの計算リソースはこのコンペティションに参加するのに十分でしょうか？
**Andreas Bisi** *2024年5月28日 火曜日 13:29:59 日本標準時* (5票)

ホームクレジットコンペティションに参加した後、新しいコンペティションに参加したいと思っています。この新しいコンペティションの目標は興味深いようです。公開ノートブックをざっと見たところ、LightGBMとLlama 3 8Bの2つの一般的なモデルが使われているようです。後者については、Kaggleでファインチューニングを行うことは可能でしょうか、それともA100インスタンスをレンタルする必要がありますか？
---
# 他のユーザーからのコメント
> ## Ivan Vybornov
> 
> Kaggleでのファインチューニングはおすすめしません。私の経験では、TPUでQLORAを使ってLlamaをファインチューニングするのは時間的に非常に苦痛なので、RTX 4090をレンタルしました。RTX 4090なら約8時間で済みます。
> 
> 
> 
> > ## Dr. Gopalashivabalasubramanium Chandrashekaran
> > 
> > ご意見ありがとうございます。経験上、KaggleでのファインチューニングはRTX 4090の8時間と比べてどれくらい時間がかかるのでしょうか？2〜3倍くらい時間がかかるのでしょうか？RTX 4090をレンタルしたくありません笑
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > 実験にお金を払うことに同意します。2〜4倍は現実的だと思います。記憶が正しければ、peft llama3を数エポック実行するのに、Kaggleでは約20時間、4090では約8時間かかりました。主な理由は、2つのT4しか使用できないためで、T4はさらに遅いです。
> > > 
> > > 
> > > 
---
> ## Kishan Vavdara
> 
> ファインチューニングにはKaggleのTPUを使用できます。
> 
> 
> 
---
> ## bogoconic1
> 
> 別の選択肢がない場合を除き、Kaggleの計算リソースを使ってファインチューニングすることはお勧めしません。短い時間で実験を繰り返せることはコンペティションでは有利であり、A100のような高速なGPUを使用すると役立ちます。また、Kaggleでは、週に30 GPU時間 + 20 TPU時間（使い方を知っていれば）しか使用できません。
> 
> 
> 
---
> ## Valentin Werner
> 
> 勝つことだけを目的としているなら、Kaggleの計算リソースでは難しいかもしれません。学ぶために参加しているなら、この課題を受け入れて、Kaggleの計算リソースで動作するソリューションを考案してみてください。
> 
> 
> 
---



</div>