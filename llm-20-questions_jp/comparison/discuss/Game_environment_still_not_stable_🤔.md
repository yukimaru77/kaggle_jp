# 要約 
ディスカッションでは、Kaggleコンペ「LLM 20 Questions」におけるゲームのポイント配分についての問題が議論されています。**Kuldeep Rathore**が、初回ラウンドでのポイント配分が不正確であると指摘し、特定のエピソードリンクを提供しています。彼は、エージェントがエラーを出した場合に他のチームメンバーがポイントを獲得するのはおかしいと述べ、理想的にはエラーを出したプレイヤーは負のスコアを得るべきで、残りのメンバーは0点であるべきだと主張しています。

他のユーザーである**waechter**も同様の意見を持ち、この問題についての以前の議論を引用しています。彼は、エージェントが失敗した場合の報酬が今後はゼロになると予想しつつも、現在の報酬計算が意図通りに機能していない可能性を指摘しています。**Bovard Doerschuk-Tiberi**は、各エージェントの不確実性が影響するため、値がゼロになることはないと補足しています。

全体として、エージェントのエラーによるポイントの扱いや報酬の算出方法に不満があり、改善が求められている様子が伺えます。

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

# Game environment still not stable? 🤔

**Kuldeep Rathore** *Mon Jun 24 2024 21:21:31 GMT+0900 (日本標準時)* (0 votes)

How come the below game ended in the round one and the points are allotted? 

Episode link: [https://www.kaggle.com/competitions/llm-20-questions/leaderboard?dialog=episodes-episode-55162391](https://www.kaggle.com/competitions/llm-20-questions/leaderboard?dialog=episodes-episode-55162391)

[@bovard](https://www.kaggle.com/bovard) 



---

 # Comments from other users

> ## waechter
> 
> The agent from Chris Deotte is in error, see Answer: none and [Err] 
> 
> Probably due to the keywords/category change.
> 
> 
> 
> > ## Kuldeep RathoreTopic Author
> > 
> > Got it but the point is other two opponents got +19 which is fine, but Giba got +5 which shouldn’t be there. Ideally if one of the player of a team is giving error then that person should get negative score but the second team member should get 0 instead of giving +5.
> > 
> > 
> > 
> > > ## waechter
> > > 
> > > I agree, this a been pointed out in the discussion [https://www.kaggle.com/competitions/llm-20-questions/discussion/508415](https://www.kaggle.com/competitions/llm-20-questions/discussion/508415) 
> > > 
> > > They made a change:
> > > 
> > > A fix for this should be rolling out tomorrow. The reward when an agent fails after this should be net zero. For example the failing agent might get -21 and the other three get an average of +7 each.
> > > 
> > > But i'm not sure it works as intented since here the reward is 19+19+5-13 != zero
> > > 
> > > 
> > > 
> > > ## Bovard Doerschuk-Tiberi
> > > 
> > > The values themselves won't equal zero, especially depending upon the uncertainty of each agent. 
> > > 
> > > 
> > > 


---



</div>
<div class="column-right">

# 日本語訳

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


</div>