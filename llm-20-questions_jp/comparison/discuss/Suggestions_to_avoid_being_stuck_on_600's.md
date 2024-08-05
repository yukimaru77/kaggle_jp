# 要約 
ディスカッションでは、コンペティションに参加したMarcel0が、600点前後のエージェントが多く、これが新しいプレイヤーのランキング向上を妨げていると指摘しています。彼は、この問題を解決するための2つの提案をしています：1つ目は、新しいエージェントが自己対戦で勝利した場合、初期スコアを600点ではなく650点または700点にすること。2つ目は、過去100試合で一度も勝利していない650点未満のエージェントを排除することです。

他のユーザーからは、競技構造の難しさに同意を示すコメントがあり、良いエージェントを提出すると最初の日に数試合をこなしてスコアが上がるが、その後は試合数が減って進展が遅くなるという体験が共有されています。

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

# Suggestions to avoid being stuck on 600's.

**Marcel0.** *Thu Jul 04 2024 05:45:26 GMT+0900 (日本標準時)* (8 votes)

I just entered this competition and noticed a huge number of agents with around 600 points that were only made for testing purposes (answering only yes for example), which could be hindering new players from climbing the leaderboard. I've read about the 10% chance to play with higher-rated players, but it seems to take a lot of time to take effect. It would be interesting to see how long a copy of the top 1 on LB beginning with 600 points would take to return to have a high score again. Maybe two alternative possibilities to try to solve this problem:

1 - When entering a new agent, if you win the test episode against yourself, your agent begins with something like 650 or 700 points instead of 600.

2 - Remove agents without a single win in the last 100 games and less than 650 points.

What do you think about it?



---

 # Comments from other users

> ## RS Turley
> 
> I agree that this is a challenging aspect of the competition structure. In a different thread, [@lowmaa](https://www.kaggle.com/lowmaa) called this "escaping the pit of dumbness."
> 
> In my experience, when I submit a good agent, it plays around 10 matches on the first day, which usually allows it to get one win and rise to the 700 range. Unfortunately, it then only plays one or two matches each day, so further progress is slow.
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# 600点から抜け出すための提案
**Marcel0.** *2024年7月4日(木) 05:45:26 GMT+0900（日本標準時）* (8票)
このコンペティションに参加したばかりで、テスト目的で作成された600点前後のエージェントが非常に多いことに気付きました（たとえば、常に「はい」と答えるなど）。これが、新しいプレイヤーがリーダーボードで順位を上げるのを妨げている可能性があります。高評価のプレイヤーと対戦する10％の確率については聞いたことがありますが、効果が現れるまでにかなりの時間がかかるようです。600ポイントから始まるトップ1のコピーが高得点に戻るまでにどのくらいの時間がかかるのかを見てみるのも面白いでしょう。この問題を解決するために試すべき二つの代替案を提案します：
1 - 新しいエージェントを登録した際に、自己対戦でテストエピソードに勝利すれば、そのエージェントは600点の代わりに650点または700点でスタートする。
2 - 過去100試合で一度も勝利しておらず、650点未満のエージェントを排除する。
皆さんはどう思いますか？
---
 # 他のユーザーからのコメント
> ## RS Turley
> 
> 競技構造のこの難しさに同意します。別のスレッドで[@lowmaa](https://www.kaggle.com/lowmaa)はこれを「愚かさの穴からの脱出」と呼んでいました。
> 
> 私の経験では、良いエージェントを提出すると、初日のうちに約10試合をこなして、通常は1勝を得て700点台に上がります。残念ながら、その後は1日に1、2試合しか行わないため、さらなる進展は遅いです。
> 
> ---


</div>