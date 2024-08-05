# 要約 
ディスカッションの要約：

ユーザー **mhericks** が、言葉当てゲーム「20の質問」において、エージェントがキーワードを正しく推測した成功したエピソードが見つからないと述べ、そうしたエピソードを求めている。これに対し、**Chris Deotte** は成功したエピソードは存在するものの、90%以上のエピソードが成功していないことに同意し、リーダーボードの上位チームが得点したゲームを探すことを勧めている。彼は自身のボットの成功例をリンクで共有し、他のユーザー **OminousDude** も異なる成功例を示している。さらに、成功したエピソードを集めて分析するためのKaggleノートブックの作成を提案し、他のユーザー **Waee** がすでにその作業を始めていることを言及している。

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

# Example of successful round

**mhericks** *Thu May 30 2024 23:49:44 GMT+0900 (日本標準時)* (0 votes)

I am new to the challenge and just skimmed through the submissions and some episodes. I am yet to find a successful episode, i.e. an episode in which an agent correctly guessed the keyword. It would be even more interesting to see an episode that also contains some questions vaguely narrowing down on the keyword.

Do such episodes exist (yet)? In this case, it'd be very helpful if someone could point me to such an episode. 



---

 # Comments from other users

> ## Chris Deotte
> 
> Hi. There are successful episodes (but I agree that 90%+ episodes are unsuccessful). View the top teams on the LB and search for a game where one team scored >25 points. Here is a recent example from my bot which occurred 3 hours ago:
> 
> - [[1st] Chris Deotte 604 (+40)[1st] Kaustubh 603 (+57) vs [3rd] Briaha 625 (-15)[3rd] huiqin 600 (-32)](https://www.kaggle.com/competitions/llm-20-questions/leaderboard?dialog=episodes-episode-54912547)
> 
> 
> 
> > ## OminousDude
> > 
> > This is another example: [https://www.kaggle.com/competitions/llm-20-questions/leaderboard?dialog=episodes-episode-54913201](https://www.kaggle.com/competitions/llm-20-questions/leaderboard?dialog=episodes-episode-54913201)
> > 
> > 
> > 
> > > ## Chris Deotte
> > > 
> > > Yes. It may be helpful to make a Kaggle notebook that finds all the successful episodes from all played games. So we can view and analyze them. Also we can compute the success rate.
> > > 
> > > UPDATE: it looks like Waee [@waechter](https://www.kaggle.com/waechter) is beginning to do this [here](https://www.kaggle.com/code/waechter/llm-20-questions-games-dataset) and [here](https://www.kaggle.com/code/waechter/llm-20-questions-leaderbord-analyze-best-agents)
> > > 
> > > 
> > > 


---



</div>
<div class="column-right">

# 日本語訳

# 成功したラウンドの例
**mhericks** *2024年5月30日 23:49:44 GMT+0900 (日本標準時)* (0票)
私はこのチャレンジに新しく参加し、提出物やいくつかのエピソードをざっと見ましたが、エージェントがキーワードを正しく推測した成功したエピソードをまだ見つけていません。キーワードをぼんやりと絞り込む質問が含まれるエピソードも見ることができれば、さらに興味深いです。
そのようなエピソードは（まだ）存在していますか？ もしあれば、どなたかそのエピソードを教えていただけると助かります。

---
# 他のユーザーのコメント
> ## Chris Deotte
> 
> こんにちは。成功したエピソードはありますが、90%以上のエピソードが成功していないというのには同意します。リーダーボードの上位チームを見て、どちらかのチームが25点以上を獲得したゲームを検索してみてください。ここに、私のボットが3時間前に行った最近の例があります：
> 
> - [[1位] Chris Deotte 604 (+40)[1位] Kaustubh 603 (+57) vs [3位] Briaha 625 (-15)[3位] huiqin 600 (-32)](https://www.kaggle.com/competitions/llm-20-questions/leaderboard?dialog=episodes-episode-54912547)
> 
> > ## OminousDude
> > 
> > こちらも別の例です：[https://www.kaggle.com/competitions/llm-20-questions/leaderboard?dialog=episodes-episode-54913201](https://www.kaggle.com/competitions/llm-20-questions/leaderboard?dialog=episodes-episode-54913201)
> > 
> > 
> > > ## Chris Deotte
> > > 
> > > はい。それらのすべての成功したエピソードを見つけるKaggleノートブックを作成すると便利かもしれません。そうすれば、私たちもそれらを見て分析することができます。また、成功率を計算することもできます。
> > > 
> > > 更新：Waee [@waechter](https://www.kaggle.com/waechter) がこれを始めているようです、ここで [こちら](https://www.kaggle.com/code/waechter/llm-20-questions-games-dataset) と [こちら](https://www.kaggle.com/code/waechter/llm-20-questions-leaderbord-analyze-best-agents) をご覧ください。
> > > 
> > > 
> > > 


</div>