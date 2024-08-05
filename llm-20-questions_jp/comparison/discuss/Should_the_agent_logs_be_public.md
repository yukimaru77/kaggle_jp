# 要約 
ディスカッションでは、ボットのログを公開すべきかについて意見が交わされています。特に、1位のチーム「Rigging」が二分探索法を用いて勝利した戦略が明らかになったことについて指摘されています。参加者の一人は、他のチームがトップチームの戦略を分析して自分のボットを構築することができ、公平性が損なわれる可能性があると懸念しています。

他のコメントでは、過去のコンペティションと比較して、戦略やロジックの理解は難しいが、現状のリーダーボードは公開されている情報に基づいているため最終的には役に立たない可能性が示唆されています。また、チーム名が表示されていない問題についても指摘があり、視覚的なバグであることが確認されています。

全体として、ボットログの公開に関する議論や、リーダーボードの透明性とその影響に関する意見が中心となっています。

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

# Should the agent logs be public?

**Khoi Nguyen** *Sun May 19 2024 18:39:15 GMT+0900 (日本標準時)* (11 votes)

This is the log of the latest game of (at the time of writing) 1st place Team Rigging vs 33rd place Pavel Pavlov:

I think the team names are wrong (!?) but anyway that's not the point, what happened here is that Team Rigging (I think) used the binary search method to deduce the final guess, they started with asking if the keyword is in one of the categories, then if first character is in the fist half of alphabet, and when the pool is small enough they started asking if the answer is in a sublist until they have the correct guess. 

There it goes, I knew the winning asker's strategy for that game. 

In previous bot arena competitions I guess the bot behavior was much harder to reverse engineer just from the game log, but for 20 Questions the method above is a proven strategy. At the worst case I can just download all the questions from the top teams and analyze them to build my own, is that fair?



---

 # Comments from other users

> ## Rob Mulla
> 
> I think it's intended by the competition designers. Similar to past agent based competitions: [halite](https://www.kaggle.com/competitions/halite), [connect-x](https://www.kaggle.com/competitions/connectx), you can openly see the strategy of each team as the game plays out. We don't know the exact logic and code used to produce the questions, but that can be easily inferred when the solutions are very simple.
> 
> For what it's worth this our current solution is only works because we know the subset of categories and words used in the public/(pre-deadline) leaderboard. Because of this, I don't think ultimately the public leaderboard is going to be a good indication of agents what will perform well on the private/post-deadline leaderboard.
> 
> Top teams might choose to not submit their best agents until right before the deadline so that their strategy isn't revealed. But in the end the public leaderboard is pretty useless anyways so 🤷‍♂️
> 
> 
> 


---

> ## Bovard Doerschuk-Tiberi
> 
> [@suicaokhoailang](https://www.kaggle.com/suicaokhoailang) We will be changing out the list of words after the submission deadline and then we'll wait for the scores to stabilize. Any agent assuming a fixed word list will perform quite poorly.
> 
> Final Evaluation
> 
>   At the submission deadline on August 13, 2024, submissions will be locked. From August 13, 2024 to August 27th, 2024 we will continue to run episodes against a new set of unpublished, secret words. At the conclusion of this period, the leaderboard is final.
> 
> 
> 


---

> ## Nicholas Broad
> 
> Why aren't there 4 team names shown? Shouldn't there be two for each team? One questioner and one answerer for each
> 
> edit: maybe the other two teams are at the bottom? It is a bit confusing who is on what team and what role, though
> 
> 
> 
> > ## Bovard Doerschuk-Tiberi
> > 
> > Yes, two teams are at the bottom. The team names at the top are a visual bug, I'll fix that.
> > 
> > 
> > 


---



</div>
<div class="column-right">

# 日本語訳

# エージェントのログは公開すべきか？
**Khoi Nguyen** *2024年5月19日 日曜日 18:39:15 GMT+0900 (日本標準時)* (11票)
これは、（執筆時点での）1位のチーム「Rigging」と33位のチーム「Pavel Pavlov」の最新のゲームログです。
チーム名が間違っているかもしれませんが、そこは問題ではありません。ここで起まったことは、チーム「Rigging」が（二分探索法を使って）最終的な推測を導き出したことだと思います。まずキーワードがいずれかのカテゴリに含まれているかを尋ね、次に最初の文字がアルファベットの前半にあるかどうかを問います。そして、プールが十分に小さくなると、答えがサブリストにあるかどうかを次々に尋ねて、正解にたどり着きます。
というわけで、私はそのゲームで勝った質問者の戦略を知ってしまいました。
以前のボットアリーナのコンペティションでは、ゲームのログからボットの行動を解析するのがずっと難しかったと思いますが、「20の質問」に関しては上記の手法が実証済みの戦略です。最悪の場合、私はトップチームの質問をすべてダウンロードして分析し、自分のボットを構築することもできるので、これは公正でしょうか？

---
# 他のユーザーからのコメント
> ## Rob Mulla
> 
> これはコンペティションの設計者による意図的なものだと思います。過去のエージェントベースのコンペティション、例えば[halite](https://www.kaggle.com/competitions/halite)や[connect-x](https://www.kaggle.com/competitions/connectx)でも、ゲームが進行する中で各チームの戦略を見ることができます。私たちは質問を生成するための具体的なロジックやコードを知らないのですが、それは解法が非常に単純な場合には容易に推測できます。
> 
> 私たちの現在の解法が機能しているのは、公にされている（締切前の）リーダーボードで使用されているカテゴリや単語のサブセットを知っているからです。このため、最終的には公のリーダーボードがプライベート/締切後のリーダーボードでうまく機能するエージェントの指標にはならないでしょう。
> 
> トップチームは、戦略が明らかになるのを避けるために、締切直前まで自分たちの最高のエージェントを提出しないかもしれません。しかし、結局のところ、公のリーダーボードはほとんど役に立たないですけど🤷‍♂️

---
> ## Bovard Doerschuk-Tiberi
> 
> [@suicaokhoailang](https://www.kaggle.com/suicaokhoailang) 提出締切後に単語のリストを変更し、その後スコアが安定するのを待ちます。固定された単語リストを前提としたエージェントは、非常に悪い成績を残すでしょう。
> 
> 最終評価
> 
>   2024年8月13日の提出締切で、提出物はロックされます。2024年8月13日から8月27日までの間、新しい公開されていない秘密の単語セットに対してエピソードを実行し続けます。この期間中、リーダーボードの対象となるのはアクティブな3つの提出物のみです。この期間が終了した時点で、リーダーボードは確定します。
> 
> ---

> ## Nicholas Broad
> 
> どうして4つのチーム名が表示されていないのでしょうか？各チームにはそれぞれ質問者と回答者がいるべきではないですか？
> 
> 編集: もしかしたら他の2つのチームが底の方にいるのかもしれません。しかし、誰がどのチームに属し、どの役割を果たしているのかは少し分かりにくいです。

> > ## Bovard Doerschuk-Tiberi
> > 
> > はい、2つのチームが下にいます。上部に表示されているチーム名は視覚的なバグですので、修正します。
> > 
> > ---


</div>