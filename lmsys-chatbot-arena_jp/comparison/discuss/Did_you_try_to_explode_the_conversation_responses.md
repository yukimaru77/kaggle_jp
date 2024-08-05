# 要約 
このディスカッションは、KaggleのLMSYS - Chatbot Arena Human Preference Predictionsコンペティションにおける会話応答の分割に関するものです。

**Mattia Vanzetto**は、トレーニングデータの約14%が複数回の会話で構成されているため、モデルに組み込まれるプロンプトと応答の長さが制限される可能性があることを指摘しています。彼は、会話応答を分割してモデルをファインチューニングし、個々の会話部分に対する予測を集計することで、この問題を解決できるのではないかと提案しています。彼は、このアプローチが単純なxgboostモデルでリーダーボードのスコアをわずかに改善したことを報告しています。

**JM**は、このアプローチを試しましたが、推論時間が増え、パブリックLBのスコアは改善されなかったとコメントしています。

**Yi-Fu Chen**は、プロンプトと応答のみを考慮し、ターゲットを相対的なwinner_model_Xとするバイナリ分類器を作成するという別のアイデアを提案しています。彼は、このアプローチは直感的に理にかなっていないと考えています。

**Mattia Vanzetto**は、Yi-Fu Chenのコメントに返信し、負けと引き分けは「比較」されるため、このアプローチは有効であると主張しています。

このディスカッションは、コンペティション参加者が、会話応答の分割やバイナリ分類器の使用など、さまざまなアプローチを試していることを示しています。これらのアプローチは、モデルの性能を向上させる可能性がありますが、推論時間や計算リソースなどの課題も伴う可能性があります。


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

# Did you try to explode the conversation responses?

**Mattia Vanzetto** *Thu Aug 01 2024 04:42:15 GMT+0900 (日本標準時)* (0 votes)

Hello guys,

I saw that the ~86% of the training conversations is composed by just a single prompt + response, but 14% is not. I saw also that, at least in the public notebooks, the fine-tuned models usually have a maximum sequence lenght of 2000/2400 characters, and often the prompt assembled for the models are just prompt_list + response_a_list + response_b_list, which surely lead to cases where the response_b is completely truncated, or anyway to a loss of information.

Did you try to explode the responses, fine-tune a model and then aggregate the predictions on the single piece of the conversation?

The mean/median length of the single piece of conversation "prompt_i + response_a_i + response_b_i" is between 2000 and 2400 characters, which seems perfect for this expirement.

I would like to try myself, but I have no fine-tuning experience, no computing power, and no time 😂

For what it's worth, I tried with a simple xgboost, same features preparation, same optimization procedure, the exploding+aggregating approach got 1.03 on the leaderboard vs 1.04 of the standard approach.

Another expirement I would have liked to do is to build a binary classifier considering just prompt + response_X, with target the relative winner_model_X, basically duplicating the number of rows, without considering the "opponent's response", and then aggregate all back.

I am really looking forward to see the solutions after the competitions ends. 

Good luck for the last days of the competition 🍀



---

 # Comments from other users

> ## JM
> 
> I tried, it increase the inference time and did not see any improvement to public LB myself
> 
> 
> 


---

> ## Yi-Fu Chen
> 
> 
> Another expirement I would have liked to do is to build a binary classifier considering just prompt + response_X, with target the relative winner_model_X, basically duplicating the number of rows, without considering the "opponent's response", and then aggregate all back.
> 
> I have thought about a similar concept, but the intuition seems unreasonable because winning and losing are compared.
> 
> 
> 
> > ## Mattia VanzettoTopic Author
> > 
> > Do you mean loosing and tie? These two would be "compared" doing so.
> > 
> > 
> > 


---



</div>
<div class="column-right">

# 日本語訳

# 会話応答を分割して試しましたか？
**Mattia Vanzetto** *2024年8月1日木曜日 04:42:15 GMT+0900 (日本標準時)* (0票)
皆さん、こんにちは。

トレーニングデータの約86%は、単一のプロンプトと応答で構成されていることがわかりました。しかし、14%はそうではありません。また、少なくとも公開されているノートブックでは、ファインチューニングされたモデルは通常、最大シーケンス長が2000/2400文字で、モデルに組み込まれるプロンプトは、prompt_list + response_a_list + response_b_listのみです。これは、response_bが完全に切り捨てられるか、情報が失われる可能性があることを意味します。

会話応答を分割し、モデルをファインチューニングしてから、個々の会話部分に対する予測を集計することを試しましたか？

単一の会話部分「prompt_i + response_a_i + response_b_i」の平均/中央値の長さは2000〜2400文字で、この実験に最適なようです。

私も試してみたいのですが、ファインチューニングの経験も、計算能力も、時間もないので😂

参考までに、単純なxgboostで、同じ特徴量の前処理、同じ最適化手順で試したところ、分割して集計するアプローチではリーダーボードで1.03、標準的なアプローチでは1.04でした。

もう1つやってみたかった実験は、プロンプト + response_Xのみを考慮し、ターゲットを相対的なwinner_model_Xとするバイナリ分類器を作成することです。これにより、行数を2倍にすることができます。「相手の応答」は考慮しません。その後、すべてを再び集計します。

コンペティション終了後にソリューションを見るのが楽しみです。

コンペティションの残りの数日間、頑張ってください🍀

---
# 他のユーザーからのコメント
> ## JM
> 
> 試しましたが、推論時間が増え、パブリックLBの改善は見られませんでした。
> 
> 
> 
---
> ## Yi-Fu Chen
> 
> 
> もう1つやってみたかった実験は、プロンプト + response_Xのみを考慮し、ターゲットを相対的なwinner_model_Xとするバイナリ分類器を作成することです。これにより、行数を2倍にすることができます。「相手の応答」は考慮しません。その後、すべてを再び集計します。
> 
> 似たような概念を考えたのですが、勝ち負けは比較されるので、直感的に理にかなっていないように思えます。
> 
> 
> 
> > ## Mattia Vanzettoトピック作成者
> > 
> > 負けと引き分けのことですか？そうすると、この2つは「比較」されることになります。
> > 
> > 
> > 
---



</div>