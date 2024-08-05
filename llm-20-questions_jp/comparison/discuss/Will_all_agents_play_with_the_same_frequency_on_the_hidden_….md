# 要約 
ディスカッションでは、コンペティション参加者のJK-Pieceが、隠れたテストセットにおけるエージェントのプレイ頻度やスキルレーティングの管理について質問しています。彼は、古いエージェントがプレイ機会が少ないため、得点の高いエージェントが有利になりやすい状況を懸念しています。

彼の質問は以下の2点です：
1. 隠れたテストセットで、すべてのエージェントは同じ頻度でプレイするのか？
2. ラン再実行の前に、すべてのエージェントのスキルレーティングが600にリセットされるのか？

これに対して、RS Turleyがコメントを寄せています。彼は、ホストが最終的なランキングの質に応じて試合の頻度を調整する自由があるため、質問1については柔軟に答えるのが難しい可能性があると指摘。また、質問2については、エージェントのスコアに対する確信が各試合後に強まることから、平均スコアはリセットされず、標準偏差がリセットされることが多いと考えられると述べています。

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

# Will all agents play with the same frequency on the hidden test set?

**JK-Piece** *Wed Jul 17 2024 00:01:09 GMT+0900 (日本標準時)* (3 votes)

Currently, old agents do not play much. In these settings, old agents with high scores have the chance to remain the leaders, and old ones with low scores have almost no chance to grow in skill. Therefore, I have questions regarding the evaluation on the hidden test set.

Will all agents play at the same frequency on the new vocabulary of keywords?

Will the skill rating be reset to 600 for all agents before the rerun?

[@Host](https://www.kaggle.com/Host) #Kaggle



---

 # Comments from other users

> ## RS Turley
> 
> The competition host has the freedom to adjust the frequency of matches based on their observations regarding the quality of the score convergence toward a stable set of final rankings, so (1) might be hard for them to answer without losing that flexibility.
> 
> Regarding (2), if you look at the internal scoring data, you’ll notice that an agent has a mean score that we observe on the leaderboard and also a standard deviation. The standard deviation decreases after each match, reflecting more certainty around that agent’s score. I believe in similar Kaggle environment competitions, the host reset each agent’s standard deviation but not the mean.
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# すべてのエージェントは隠れたテストセットで同じ頻度でプレイするのでしょうか？
**JK-Piece** *2024年7月17日（水）00:01:09 GMT+0900 (日本標準時)* (3票)
現在、古いエージェントはあまりプレイしていません。このような状況では、高得点の古いエージェントがリーダーの地位を維持するチャンスがあり、得点の低い古いエージェントはスキルを向上させるほとんどの機会がありません。そのため、隠れたテストセットの評価に関していくつか質問があります。
1. 新しいキーワードのボキャブラリーに対して、すべてのエージェントは同じ頻度でプレイするのでしょうか？
2. ラン再実行の前に、すべてのエージェントのスキルレーティングは600にリセットされるのでしょうか？
[@Host](https://www.kaggle.com/Host) #Kaggle
---
# 他のユーザーからのコメント
> ## RS Turley
> 
> コンペティションのホストは、最終的なランキングが安定したセットに収束する質に関する観察に基づいて試合の頻度を調整する自由がありますので、（1）については、その柔軟性を失わずに答えるのが難しいかもしれません。  
>  
> （2）については、内部スコアデータを見ると、エージェントにはリーダーボード上で観測される平均スコアと標準偏差があることがわかります。各試合の後、標準偏差は減少し、そのエージェントのスコアに対する確信が強まります。同様のKaggle環境のコンペティションでは、ホストが各エージェントの標準偏差はリセットするが、平均はリセットしないことが多いと考えています。  
>  
> ---


</div>