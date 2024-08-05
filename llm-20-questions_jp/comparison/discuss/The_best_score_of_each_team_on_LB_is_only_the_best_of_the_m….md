# 要約 
このディスカッションでは、参加者がKaggleのコンペティションにおけるリーダーボード（LB）のスコア表示に関して意見を述べています。主なポイントは以下の通りです。

1. **LBのスコア表示方式**: ユーザーKha Voは、796のスコアを持つボットが2位になるべきだと考えているが、新しい提出物によりそのボットがリーダーボードから押し出される事例について疑問を呈しています。

2. **Bovard Doerschuk-Tiberiの説明**: 彼は、計算リソースとリーダーボードへの影響を考慮し、最新の3つの提出物のみがアクティブとされ、提出締切時点でこれらのエージェントのみが最終リーダーボードに考慮されると説明しています。

3. **Kha Voの異議**: Kha Voは、Kaggleがどのボットを運用するかを選ぶことを許可しないのは不自然であると述べ、実験や提出が多い中で異なるボットバージョンを選択することの重要性に言及しています。

4. **新しい機能の提案**: Bovardは、提出物を「エバーグリーン」としてマークできる機能を検討中で、その場合無効化されずに総数にはカウントされるとしています。参加者の意見を求めています。

5. **mhericksの意見**: この問題の原因はアクティブなエージェントが3つまでしか持てないことにあるとし、参加するエージェントを選ぶ方法が必要であると同意しています。

全体として、参加者たちは、プレイヤーがより柔軟にボットを管理できるようにする方法について議論しており、特にリーダーボードのスコア表示に関する改善を求めています。

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

# The best score of each team on LB is only the best of the most recent 3 submissions

**Kha Vo** *Wed Jun 05 2024 23:37:18 GMT+0900 (日本標準時)* (3 votes)

I have a bot with 796 score which should place 2nd. But when I submitted some new submissions, those pushed my 796-score bot out of the LB ranking.

Is this what we should expect? I guess an absolute best score should be displayed there on LB.

And how are the final bots selected for scoring at the end?

[@bovard](https://www.kaggle.com/bovard) 



---

 # Comments from other users

> ## Bovard Doerschuk-Tiberi
> 
> There were significant problems with keeping all submissions active (compute, leaderboard implications) so our current system only keeps the most recent three submissions. 
> 
> When the submission deadline hits, only your active agents will be considered for the final leaderboard
> 
> 
> 
> > ## Kha VoTopic Author
> > 
> > Thanks for clarifying. However it is still strange if Kaggle doesn’t allow us to choose which bots to operate. Day to day experiment and submission can be plentiful, and selecting different bot versions can spread a long period of time. 
> > 
> > 
> > 
> > > ## Bovard Doerschuk-Tiberi
> > > 
> > > Thanks for the feedback!
> > > 
> > > Arbitrary switching agents in and out causes a few different vectors to game the system so enabling that is unlikely.
> > > 
> > > We have considered the ability to mark a submission as "evergreen" so it doesn't get disabled (but still counts towards your total). How does that sound to you?
> > > 
> > > 
> > > 


---

> ## mhericks
> 
> I think that this is due to the fact, that one can only have three active agents. Since there is (currently) no way to select which agents are evaluated, only the 3 most recent submissions keep participating. Also, as the score of an agent (in some way) depends on all other agents on the leaderboard and the exact scoring mechanism used at the time, it would not be correct to take the maximum score of all agents ever submitted if the agent corresponding to the maximum is no longer re-evaluated constantly. 
> 
> Still, I totally agree that there should be a way to select which agents to participate in the leaderboard games. 
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# LBの各チームの最高スコアは、最近の3つの提出物の中での最高スコアのみです
**Kha Vo** *2024年6月5日水曜日 23:37:18 JST* (3票)
796のスコアを持つボットがあり、2位になるはずですが、新しい提出物をいくつか提出したところ、私の796スコアのボットがLBランキングから押し出されてしまいました。これは予想通りのことですか？絶対的な最高スコアがLBに表示されるべきだと思います。
最終的なボットはどのように選ばれてスコア付けされるのでしょうか？
[@bovard](https://www.kaggle.com/bovard)
---
# 他のユーザーからのコメント
> ## Bovard Doerschuk-Tiberi
> 
> すべての提出物をアクティブに保つことに関しては重大な問題があったため（計算リソースやリーダーボードへの影響）、現在のシステムでは最新の3つの提出物のみを維持しています。
> 
> 提出締切が来た時には、アクティブなエージェントのみが最終的なリーダーボードに考慮されます。
> 
> > ## Kha Vo（トピック作成者）
> > 
> > ご説明ありがとうございます。しかし、Kaggleがどのボットを運用するかを選ぶことを許可していないのは奇妙です。日々の実験や提出は数多くあり、異なるボットバージョンを選択するのは長期間にわたって広がることがあります。
> 
> > > ## Bovard Doerschuk-Tiberi
> > > > ご意見ありがとうございます！
> > > > 
> > > > 任意にエージェントを入れ替えると、いくつかの異なるルートでシステムをゲームすることができるため、それを可能にするのは難しいです。
> > > > 
> > > > 提出物を「エバーグリーン」としてマークできる機能を検討しています。この場合、その提出物は無効化されませんが、総数にはカウントされます。それについてはどう思いますか？
> > > > 
> > > > 
---
> ## mhericks
> 
> これは、アクティブなエージェントが3つしか持てないという事実が原因だと思います。現在のところ、どのエージェントが評価されるかを選択する方法がないため、最新の3つの提出物だけが参加し続けます。また、エージェントのスコアは（ある意味で）リーダーボード上の他のすべてのエージェントや、その時の正確なスコアリングメカニズムに依存しているため、最高スコアのエージェントが再評価されていなければ、すべてのエージェントの中での最大スコアを取ることは正しくありません。
> 
> それでも、リーダーボードのゲームに参加するエージェントを選択する方法があるべきだという意見には完全に賛成です。
> 
> ---


</div>