# ゲームの環境はまだ安定していないのか？ 🤔
**Kuldeep Rathore** *2024年6月24日 月曜日 21:21:31 GMT+0900 (日本標準時)* (0票)
どうして以下のゲームが初回ラウンドで終了し、ポイントが配分されたのでしょうか？ 
エピソードリンク: [https://www.kaggle.com/competitions/llm-20-questions/leaderboard?dialog=episodes-episode-55162391](https://www.kaggle.com/competitions/llm-20-questions/leaderboard?dialog=episodes-episode-55162391)
[@bovard](https://www.kaggle.com/bovard) 
---
# 他のユーザーからのコメント
> ## waechter
> 
> Chris Deotteのエージェントにエラーがあります。「Answer: none」と「[Err]」が表示されています。 
> 
> おそらく、キーワードやカテゴリーの変更によるものです。
> 
> > ## Kuldeep Rathore（トピック作成者）
> > 
> > なるほど。しかし、問題は他の2人の対戦相手が+19を獲得しているのは理解できますが、Gibaが+5を獲得したのはおかしいことです。理想的には、チームの一人がエラーを出した場合、そのプレイヤーは負のスコアを得るべきですが、残りのチームメンバーは0点になるべきではなく+5を得るのはおかしいです。
> 
> > > ## waechter
> > > > 同意します。これは以前の議論でも指摘されていますね。[https://www.kaggle.com/competitions/llm-20-questions/discussion/508415](https://www.kaggle.com/competitions/llm-20-questions/discussion/508415) 
> > > > 
> > > > この修正は明日適用されるはずです。今後、エージェントが失敗した場合の報酬は実質的にゼロになるでしょう。例えば、失敗したエージェントが-21を得ると、他の3人が各々+7の平均を得ることになります。
> > > > 
> > > > しかし、この場合の報酬が19+19+5-13 != ゼロになるため、意図通りに機能しているかはわかりません。
> > > > 
> > > > > ## Bovard Doerschuk-Tiberi
> > > > > 値自体がゼロになることはありません。特に各エージェントの不確実性によって影響されます。
> > > > 
