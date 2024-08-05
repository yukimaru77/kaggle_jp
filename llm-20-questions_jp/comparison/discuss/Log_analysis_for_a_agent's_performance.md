# 要約 
このコンペのディスカッションでは、ユーザーのVijayaragavanRamasamyが自分のエージェントのパフォーマンスを確認するために、ログデータから特定の推測や質問を見つける方法について質問しています。彼は、プレイヤーの動きが複数の推測や回答としてJSON形式で記録されていることに触れています。

それに対して、他の参加者waechterが、JSONログをダウンロードして使いやすいデータセットにフォーマットするためのコードを提供しており、現在の優秀なエージェントのゲームを分析できるリソースも共有しています。彼は、具体的なデータフレーム操作の例を示し、VijayaragavanRamasamyが自分のエージェントのデータを効率的に分析する手助けをしています。

最終的に、VijayaragavanRamasamyはwaechterのアプローチを試す意向を示しています。

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

# Log analysis for a agent's performance 

**VijayaragavanRamasamy** *Mon Jun 03 2024 00:33:46 GMT+0900 (日本標準時)* (1 votes)

How to decipher logs? There are 4 players and multiple guesses as well as answers in json. How do I find the guesses or questions asked by my agent?



---

 # Comments from other users

> ## waechter
> 
> I made [https://www.kaggle.com/code/waechter/llm-20-questions-games-dataset](https://www.kaggle.com/code/waechter/llm-20-questions-games-dataset) to download json logs, and format them into an easy to use dataset
> 
> In [https://www.kaggle.com/code/waechter/llm-20-questions-leaderbord-analyze-best-agents](https://www.kaggle.com/code/waechter/llm-20-questions-leaderbord-analyze-best-agents) i use the dataset to analyse games from the current best agents. You can use it to analyze your own games 
> 
> Example:
> 
> df.loc[df.guesser='your_team_name']
> 
> Hope this help!
> 
> 
> 
> > ## VijayaragavanRamasamyTopic Author
> > 
> > Thanks. I will try analysing json logs using this approach 
> > 
> > 
> > 


---



</div>
<div class="column-right">

# 日本語訳

# エージェントのパフォーマンスに関するログ分析
**VijayaragavanRamasamy** *2024年6月3日 月曜日 00:33:46 GMT+0900 (日本標準時)* (1票)
ログを解読するにはどうしたらいいですか？プレイヤーは4人いて、複数の推測や回答がjson形式で記録されています。その中から自分のエージェントが行った推測や質問を見つけるにはどうすれば良いでしょうか？
---
 # 他のユーザーからのコメント
> ## waechter
> 
> [こちら](https://www.kaggle.com/code/waechter/llm-20-questions-games-dataset)でjsonログをダウンロードし、使いやすいデータセットにフォーマットするためのコードを作成しました。
> 
> また、[こちら](https://www.kaggle.com/code/waechter/llm-20-questions-leaderbord-analyze-best-agents)で、そのデータセットを使用して現在の優秀なエージェントのゲームを分析しています。自身のゲームを分析するのにも役立つと思います。
> 
> 例:
> 
> df.loc[df.guesser='your_team_name']
> 
> 参考になれば幸いです！
>
> > ## VijayaragavanRamasamyトピック作成者
> > 
> > ありがとうございます。このアプローチでjsonログを分析してみます。
> > 
> > 
> > 


</div>