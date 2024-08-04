# エージェントのパフォーマンスログ分析

**VijayaragavanRamasamy** *月 6 月 3 日 2024 00:33:46 GMT+0900 (日本標準時)* (1 票)

ログの解読方法を教えてください。4人のプレイヤーと複数の推測と回答がJSON形式で含まれています。自分のエージェントが尋ねた質問や推測を見つけるにはどうすればよいですか？

---
# 他のユーザーからのコメント

> ## waechter
> 
> JSONログをダウンロードして使いやすいデータセットにフォーマットするために、[https://www.kaggle.com/code/waechter/llm-20-questions-games-dataset](https://www.kaggle.com/code/waechter/llm-20-questions-games-dataset) を作成しました。
> 
> [https://www.kaggle.com/code/waechter/llm-20-questions-leaderbord-analyze-best-agents](https://www.kaggle.com/code/waechter/llm-20-questions-leaderbord-analyze-best-agents) では、このデータセットを使用して、現在のトップエージェントによるゲームを分析しています。これを使って自分のゲームを分析することもできます。
> 
> 例：
> 
> `df.loc[df.guesser='your_team_name']`
> 
> お役に立てれば幸いです！
> 
> 
> 
> > ## VijayaragavanRamasamy トピック作成者
> > 
> > ありがとうございます。この方法でJSONログを分析してみます。
> > 
> > 
> > 
---

