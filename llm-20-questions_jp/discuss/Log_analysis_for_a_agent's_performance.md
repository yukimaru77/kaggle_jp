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
