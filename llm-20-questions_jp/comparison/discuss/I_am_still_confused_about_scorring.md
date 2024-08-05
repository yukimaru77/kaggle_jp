# 要約 
ディスカッションでは、コンペにおけるスコアリングシステムについての混乱が話題になっています。参加者のVolodymyrBilyachatは、質問者と回答者が協力してエピソードを進め、単語を当てることでポイントを得ると理解していましたが、連携がうまくいかないとマイナスの報酬を受けると考えていました。

その後、Chris Deotteがスコアの変動について詳細に説明しました。ポイントは、対戦相手やチームメイトのスコアに基づいて変動し、自分より低いスコアのチームと引き分ければ自分のスコアは減少し、高いスコアのチームと引き分ければ増加することが説明されました。勝つとスコアが増加し、負けると減少します。また、引き分けの場合はスコアが平均に近づくとされています。

VolodymyrBilyachatはChrisの説明を受けて理解が深まったと述べています。

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

# I am still confused about scorring

**VolodymyrBilyachat** *Thu May 30 2024 08:00:42 GMT+0900 (日本標準時)* (0 votes)

My understanding that questioner and answerer works together. If they guess the word they will get points so i would assume if they dont work nicely both gets negative reward.



---

 # Comments from other users

> ## Chris Deotte
> 
> Your change in points depends on the scores of your teammate and opponents.
> 
> Before game started, you had 659, Learning Curve had 599, Raki had 603, and Lathashree had 594. Afterward you all tied. So all scores move toward the average of the 4 teams. This means your score decreases while the other 3 increase.
> 
> Here is a approximate summary:
> 
> - If you tie with teams scored lower than yourself, your score decrease
> 
> - If you tie with teams scored higher than yourself, your score increase
> 
> - If you win, your score increase
> 
> - If you lose, your score decrease.
> 
> 
> 
> > ## Chris Deotte
> > 
> > Here is quote from evaluation page [here](https://www.kaggle.com/competitions/llm-20-questions/overview/evaluation)
> > 
> > Ranking System
> > 
> >   After an episode finishes, we'll update the rating estimate for all bots in the episode. If one bot pair won, we'll increase their μ and decrease the opponent's μ -- if the result was a tie, then we'll move the μ values closer towards their mean. The updates will have magnitude relative to the deviation from the expected result based on the previous μ values, and also relative to each bot’s uncertainty σ. We also reduce the σ terms relative to the amount of information gained by the result. The score by which your bot wins or loses an episode does not affect the skill rating updates.
> > 
> > 
> > 
> > ## VolodymyrBilyachatTopic Author
> > 
> > Okay now it make sense. Thanks for explanation
> > 
> > 
> > 


---



</div>
<div class="column-right">

# 日本語訳

# まだスコアリングについて混乱しています
**VolodymyrBilyachat** *2024年5月30日 08:00:42 (日本標準時)* (0票)
私の理解では、質問者と回答者は協力して作業します。もし彼らが単語を当てればポイントを得るでしょうから、うまく連携できなければ両方ともマイナスの報酬を受けると思います。
---
 # 他のユーザーからのコメント
> ## Chris Deotte
> 
> あなたのポイントの変化は、チームメイトと対戦相手のスコアによって決まります。
> 
> ゲームが始まる前、あなたは659、Learning Curveは599、Rakiは603、Lathashreeは594でした。その後、全員が引き分けになったので、全てのスコアは4つのチームの平均に近づきます。つまり、あなたのスコアは減少し、他の3つのスコアは増加します。
> 
> おおよその概要は以下の通りです:
> 
> - 自分より低いスコアのチームと引き分けた場合、あなたのスコアは減少します。
> 
> - 自分より高いスコアのチームと引き分けた場合、あなたのスコアは増加します。
> 
> - 勝った場合、あなたのスコアは増加します。
> 
> - 負けた場合、あなたのスコアは減少します。
> 
> > ## Chris Deotte
> > 
> > 評価ページからの引用です [こちら](https://www.kaggle.com/competitions/llm-20-questions/overview/evaluation)
> > 
> > ランキングシステム
> > 
> >   エピソードが終了すると、すべてのボットのレーティング推定値が更新されます。もしボットペアが勝った場合、そのペアのμは増加し、対戦相手のμは減少します。引き分けの場合は、μの値が平均に近づくように調整されます。更新の大きさは、以前のμ値に基づく予想結果からの偏差および各ボットの不確実性σに比例します。また、結果によって得られた情報量に応じて、σの項も減少させます。エピソードでボットが勝利または敗北したスコアは、スキルレーティングの更新には影響しません。
> > 
> > 
> > ## VolodymyrBilyachat トピック作成者
> > 
> > なるほど、理解できました。説明ありがとうございます。 
> > 
> > 
> > 
---


</div>