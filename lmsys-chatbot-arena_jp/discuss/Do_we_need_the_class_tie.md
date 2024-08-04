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
