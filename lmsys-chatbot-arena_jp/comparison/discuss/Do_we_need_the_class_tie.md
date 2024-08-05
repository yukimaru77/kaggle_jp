# 要約 
このディスカッションは、Kaggleコンペティション「LMSYS - Chatbot Arena 人間による好み予測チャレンジ」における「tie」クラスの必要性について議論しています。

**問題点:**

* ユーザーが2つのモデルの回答を同じように良いと評価した場合、確率が(0.5, 0.5)になるのに、なぜ「tie」クラスが必要なのか疑問視されています。

**回答:**

* Marília Prataは、元のデータセットでは「winner_tie」ではなく「winner」列があり、行は「model_a」、「model_b」、「tie」、そして「tie (bothbad)」となっていることを説明しています。
* 「tie」は、ユーザーが両方のモデルを同じように良いと評価した場合だけでなく、両方のモデルを同じように悪いと評価した場合（どちらも幻覚や質問への回答を避けているなど）にも使用されます。
* bogoconic1は、後者の場合、確率が(0.5, 0.5)にならない可能性があると指摘しています。
* Rich Olsonは、最初の提出で「winner_tie」をすべて0にした結果、スコアが非常に低くなったことを報告しています。これは、「winner_tie」が0であることが要因である可能性を示唆しています。

**結論:**

* 「tie」クラスは、ユーザーが両方のモデルを同じように良いと評価した場合だけでなく、両方のモデルを同じように悪いと評価した場合も考慮するために必要です。
* 「winner_tie」を0にすることは、スコアに悪影響を与える可能性があります。
* 「winner_tie」を適切に予測することは、コンペティションで良いスコアを得るために重要です。

**追加情報:**

* Marília Prataは、コンペティションの主催者が書いたノートブックや論文で、タイについて詳しく説明していることを示唆しています。
* トレーニングデータでは、タイは非常に一般的です（約3分の1）。

このディスカッションは、コンペティション参加者にとって重要な情報を提供しており、「tie」クラスをどのように扱うかについて考えるための良い出発点となります。


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

# Do we need the class "tie"?

**Anh Bui** *Fri May 03 2024 15:50:05 GMT+0900 (日本標準時)* (4 votes)

I have a question about why there is a class 'tie', when based on the probabilities (winner_model_a/winner_model_b) = (0.5, 0.5), it can be determined whether the two models have a 'tie'.



---

 # Comments from other users

> ## Marília Prata
> 
> Hi Anh Bui (bibanh),
> 
> On the original dataset instead of "winner_tie"  they have "winner" column (where the Rows are: model_a, model_b, tie AND tie (bothbad)
> 
> Battles No ties
> 
> battles_no_ties = battles[~battles["winner"].str.contains("tie")]
> 
> Battles without ties
> 
> visualize_battle_count(battles_no_ties, "Battle Count for Each Combination of Models (without Ties)")
> 
> Counting ties
> 
> visualize_battle_count(battles[battles['winner'].str.contains("tie")], "Tie Count for Each Combination of Models")
> 
> [https://colab.research.google.com/drive/1KdwokPjirkTmpO_P1WByFNFiqxWQquwH#scrollTo=PbTdhkLQp113](https://colab.research.google.com/drive/1KdwokPjirkTmpO_P1WByFNFiqxWQquwH#scrollTo=PbTdhkLQp113)
> 
> That's what the authors wrote:
> 
> "Statistics
> 
> "The authors allowed the user to declare a tie between the pairs of models. To collect additional data, later in the tournament they also allowed the user to declare a tie in which both models were bad. There were a significant portion of tied outcomes."
> 
> I hope it could help to clarify. I didn't read anything else about the ties on that Notebook or in their paper too.
> 
> 
> 


---

> ## bogoconic1
> 
> I would think it is necessary for reason (B)
> 
> A tie could mean
> 
> (A) The user rates both responses as equally good
> 
> (B) The user rates both responses as equally bad. The 2 models can answer in different ways, of which both responses are hallucinated (by making up completely different facts etc) or not answering the question
> 
> For (B) I’m pretty sure the 2 classes will not be predicted as (0.5, 0.5) 🧐
> 
> 
> 


---

> ## Rich Olson
> 
> For my first submission - I tried filling in "winner_tie" with all 0's.
> 
> That got me a score of 11.73 (almost last-place).  At least - I'm assuming "winner_tie" being 0's was a factor.
> 
> For my next entry - I'm going to try to fill in winner_tie based on the confidence of A or B winning.  Hopefully this improves things…
> 
> In the train data - it seems ties are very common (about 1 out of 3).
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# 「tie」クラスは必要ですか？
**Anh Bui** *2024年5月3日 金曜日 15:50:05 JST* (4票)

確率（winner_model_a/winner_model_b）が（0.5, 0.5）の場合、2つのモデルが「tie」であるかどうかを判断できるのに、なぜ「tie」クラスがあるのか疑問に思います。

---
# 他のユーザーからのコメント
> ## Marília Prata
> 
> Anh Bui (bibanh) さん、こんにちは。
> 
> 元のデータセットでは、「winner_tie」の代わりに「winner」列があり、行は「model_a」、「model_b」、「tie」、そして「tie (bothbad)」となっています。
> 
> タイがないバトル
> 
> battles_no_ties = battles[~battles["winner"].str.contains("tie")]
> 
> タイがないバトル
> 
> visualize_battle_count(battles_no_ties, "Battle Count for Each Combination of Models (without Ties)")
> 
> タイの数を数える
> 
> visualize_battle_count(battles[battles['winner'].str.contains("tie")], "Tie Count for Each Combination of Models")
> 
> [https://colab.research.google.com/drive/1KdwokPjirkTmpO_P1WByFNFiqxWQquwH#scrollTo=PbTdhkLQp113](https://colab.research.google.com/drive/1KdwokPjirkTmpO_P1WByFNFiqxWQquwH#scrollTo=PbTdhkLQp113)
> 
> これは、著者が書いたものです。
> 
> 「統計
> 
> 「著者は、ユーザーがモデルのペア間のタイを宣言できるようにしました。追加のデータ収集のために、トーナメントの後半では、ユーザーが両方のモデルが悪い場合にタイを宣言できるようにしました。タイの結果はかなりの割合を占めていました。」
> 
> 明確になることを願っています。そのノートブックや論文でも、タイについて他に何も読んでいません。
> 
> 
> 
---
> ## bogoconic1
> 
> 理由 (B) のために必要だと思います。
> 
> タイは、次のような意味を持つ可能性があります。
> 
> (A) ユーザーは両方の回答を同じように良いと評価する。
> 
> (B) ユーザーは両方の回答を同じように悪いと評価する。2つのモデルは異なる方法で回答することができ、その両方の回答が幻覚（完全に異なる事実などを作り出すなど）または質問に答えない。
> 
> (B) の場合、2つのクラスは（0.5, 0.5）として予測されないと思います🧐
> 
> 
> 
---
> ## Rich Olson
> 
> 最初の提出では、「winner_tie」をすべて 0 で埋めてみました。
> 
> その結果、スコアは 11.73（ほぼ最下位）でした。少なくとも、「winner_tie」が 0 であることが要因だったと思います。
> 
> 次の提出では、「winner_tie」を A または B が勝つ確率に基づいて埋めてみます。うまくいけば、これで改善されるでしょう…
> 
> トレーニングデータでは、タイは非常に一般的です（約 3 分の 1）。
> 
> 
> 
---


</div>