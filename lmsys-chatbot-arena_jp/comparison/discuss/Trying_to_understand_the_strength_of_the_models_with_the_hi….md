# 要約 
##  コンペティションディスカッション要約

このディスカッションは、KaggleのLMSYS - Chatbot Arena Human Preference Predictionsコンペティションにおける、モデルの強さをタイの数からどのように評価するかについて議論しています。

**投稿者Dr. Gopalashivabalasubramanium Chandrashekaran**は、タイ率の高いモデルをリストアップし、特に性能が低いモデル同士がタイになることに疑問を呈しています。勝利数に基づいた評価は容易ですが、タイの数からモデルの強さを判断するのは難しいと指摘しています。

**ユーザーtanaka**は、LMSYSのELOレーティングがタイを考慮した計算方法を採用していることを説明しています。タイになった場合、上位のプレイヤーのスコアはわずかに減少し、下位のプレイヤーのスコアはわずかに増加する可能性があるとのことです。

**ユーザーValentin Werner**は、プロンプトの重要性を強調し、簡単な質問に対しては、性能の低いモデルでも上位モデルとタイになる可能性があることを指摘しています。また、同じカテゴリのモデルは、より頻繁にタイになることを期待していると述べています。さらに、LMSYSのウェブサイトでは、タイも予測対象としており、モデルが頻繁にタイになることは、多くの勝利と同じくらい良いことであると説明しています。

**要約:**

* このディスカッションは、モデルの強さを評価する際に、タイの数も考慮すべきかどうかという問題を提起しています。
* タイは、モデルの性能が低い場合だけでなく、プロンプトの難易度やモデルのカテゴリによって発生する可能性があることが指摘されています。
* LMSYSのELOレーティングは、タイを考慮した計算方法を採用しており、タイはモデルの強さを評価する上で重要な要素であることが示唆されています。


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

# Trying to understand the strength of the models with the highest ties

**Dr. Gopalashivabalasubramanium Chandrashekaran** *Sat Jun 08 2024 09:37:46 GMT+0900 (日本標準時)* (-1 votes)

Good evening everyone,

I had a go at this data and made myself a list of the models with the highest tie rate. It made sense that the non-winner models will be the ones tie-ing. It was interesting to see the models that were subpar tie-ing with each other. 

My question here is: How do I assess the strength of the model based on the count of its ties? It is easy to judge it based on its number of wins. 

Anyone have any findings on this?

Also, if you have time, see my notebook. Would appreciate any feedback.



---

 # Comments from other users

> ## tanaka
> 
> lmsys's elo rating is calculated something like following.
> 
> It means, when ties, higher rank player's score may decrease slightly, while lower-ranked player's score may increase slightly.
> 
> ```
> def compute_online_elo(battles, K=4, SCALE=400, BASE=10, INIT_RATING=1000):
>     rating = defaultdict(lambda: INIT_RATING)
> 
>     for rd, model_a, model_b, winner in battles[['model_a', 'model_b', 'winner']].itertuples():
>         ra = rating[model_a]
>         rb = rating[model_b]
>         ea = 1 / (1 + BASE ** ((rb - ra) / SCALE))
>         eb = 1 / (1 + BASE ** ((ra - rb) / SCALE))
>         if winner == "model_a":
>             sa = 1
>         elif winner == "model_b":
>             sa = 0
>         elif winner == "tie" or winner == "tie (bothbad)":
>             sa = 0.5
>         else:
>             raise Exception(f"unexpected vote {winner}")
>         rating[model_a] += K * (sa - ea)
>         rating[model_b] += K * (1 - sa - eb)
> 
>     # calibrate llama-13b to 800
>     delta = (800-rating["llama-13b"])
>     for model in battles["model_a"].unique():
>         rating[model] += delta
> 
>     return rating
> 
> ```
> 
> Refs
> 
> - [https://colab.research.google.com/drive/1KdwokPjirkTmpO_P1WByFNFiqxWQquwH#scrollTo=hytEb0aXfcwm](https://colab.research.google.com/drive/1KdwokPjirkTmpO_P1WByFNFiqxWQquwH#scrollTo=hytEb0aXfcwm)
> 
> 
> 


---

> ## Valentin Werner
> 
> 
> It was interesting to see the models that were subpar tie-ing with each other.
> 
> It is important to acknowledge that the prompt matters a lot. When presenting prompting in my company, I show a tool a bit like the lmsys arena to raise understanding for when you need the "big guns". On a simple questions, llama2-7B can easily tie gpt4-turbo, such as "what is 2+2?" - you will not need that many parameters to answer this. Now, one model may say "4" and the other one says "Adding 2+2 results in 4." and you may prefer one of the answers. Oops, suddenly Llama2-7B "outperformed" GPT-4?
> 
> Further, we always expect models of the same category to tie more often - not sure if I fully understood your point.
> 
> How do I assess the strength of the model based on the count of its ties? It is easy to judge it based on its number of wins.
> 
> This is what LMSYS is doing on the website. For this competition, we are also predicting ties - so knowing that a model ties a lot should be as good as winning a lot.
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# モデルの強さをタイの数から理解しようとする試み

**Dr. Gopalashivabalasubramanium Chandrashekaran** *2024年6月8日 土曜日 09:37:46 JST* (-1 votes)

皆さん、こんばんは。

このデータを使って色々試してみたのですが、タイ率の高いモデルをリストアップしてみました。勝っていないモデルがタイになるのは当然ですが、性能が低いモデル同士がタイになるのは興味深いですね。

ここで疑問なのは、タイの数からモデルの強さをどのように評価すればいいのかということです。勝利数に基づいて判断するのは簡単ですが、タイの数から判断するのは難しいです。

この点について何か発見した方はいらっしゃいますか？

また、もしよろしければ私のノートブックを見てください。フィードバックがあれば幸いです。

---
# 他のユーザーからのコメント

> ## tanaka
> 
> lmsysのELOレーティングは、以下の様な計算方法で算出されます。
> 
> つまり、タイになった場合、上位のプレイヤーのスコアはわずかに減少し、下位のプレイヤーのスコアはわずかに増加する可能性があります。
> 
> ```
> def compute_online_elo(battles, K=4, SCALE=400, BASE=10, INIT_RATING=1000):
>     rating = defaultdict(lambda: INIT_RATING)
> 
>     for rd, model_a, model_b, winner in battles[['model_a', 'model_b', 'winner']].itertuples():
>         ra = rating[model_a]
>         rb = rating[model_b]
>         ea = 1 / (1 + BASE ** ((rb - ra) / SCALE))
>         eb = 1 / (1 + BASE ** ((ra - rb) / SCALE))
>         if winner == "model_a":
>             sa = 1
>         elif winner == "model_b":
>             sa = 0
>         elif winner == "tie" or winner == "tie (bothbad)":
>             sa = 0.5
>         else:
>             raise Exception(f"unexpected vote {winner}")
>         rating[model_a] += K * (sa - ea)
>         rating[model_b] += K * (1 - sa - eb)
> 
>     # calibrate llama-13b to 800
>     delta = (800-rating["llama-13b"])
>     for model in battles["model_a"].unique():
>         rating[model] += delta
> 
>     return rating
> 
> ```
> 
> 参考文献
> 
> - [https://colab.research.google.com/drive/1KdwokPjirkTmpO_P1WByFNFiqxWQquwH#scrollTo=hytEb0aXfcwm](https://colab.research.google.com/drive/1KdwokPjirkTmpO_P1WByFNFiqxWQquwH#scrollTo=hytEb0aXfcwm)
> 
> 
> 
---
> ## Valentin Werner
> 
> 
> 性能が低いモデル同士がタイになるのは興味深いですね。
> 
> プロンプトが非常に重要であることを認識することが重要です。私の会社でプロンプティングについて説明する際には、lmsysアリーナのようなツールを使って、いつ「大砲」が必要になるのかを理解してもらうようにしています。簡単な質問の場合、llama2-7Bは簡単にgpt4-turboとタイになります。例えば、「2+2は？」という質問に対しては、これだけの数のパラメータは必要ありません。一方、あるモデルは「4」と答え、もう一方のモデルは「2+2を足すと4になります」と答えるかもしれません。そして、どちらかの答えを好むかもしれません。おっと、突然Llama2-7BがGPT-4を「凌駕」したのでしょうか？
> 
> さらに、同じカテゴリのモデルは、より頻繁にタイになることを期待しています。私の理解が間違っていなければですが。
> 
> タイの数からモデルの強さをどのように評価すればいいのかということです。勝利数に基づいて判断するのは簡単ですが、タイの数から判断するのは難しいです。
> 
> これは、LMSYSがウェブサイトで行っていることです。このコンペティションでは、タイも予測しています。つまり、モデルが頻繁にタイになることは、多くの勝利と同じくらい良いことです。
> 
> 
> 
---




</div>