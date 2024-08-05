# 要約 
このディスカッションでは、参加者のフランチェスコ・フィアミンゴが、提出したエージェントをキャンセルして以前のエージェントを維持する方法について質問しています。彼は、異なる設定でエージェントを試しているが、特定のエージェントを生かしておきたい一方で、悪いエージェントを代替したいと考えています。しかし、現在のエージェントは提出された時間に基づいて選ばれるため、どのようにキャンセルできるか分からないと述べています。

それに対するクリス・デオッテのコメントでは、アクティブなエージェントは自動的に最近提出された3つのエージェントから選ばれるため、新しいエージェントを提出することでのみ置き換えられることが説明されています。また、ボットのオン・オフを難しくしているかもしれない理由として、高いスコアを達成したボットが無効化され、競技の終盤に再び有効化されるのを防ぐ可能性が指摘されています。最終的には、公開リーダーボードでの成績がプライベートリーダーボードへの影響を持つため、この仕組みが意図されているかもしれないと示唆されています。

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

# how to cancel an agent?

**francesco fiamingo** *Sat Jul 27 2024 03:55:41 GMT+0900 (日本標準時)* (3 votes)

dear friends, 

i m tring varius agents with varius setting…. but sometimes i have good agent that i want to keep and bad agent that i want to substitute….but seems not possibile becosue the substituaiotn (max 3 in same time and max 5 per day) is releted "when" the agent is submitted, do you knwo how to cancel a speficig agent keeping "alive" one that was submitted erlier? thanks a lot a win the best!



---

 # Comments from other users

> ## Chris Deotte
> 
> We cannot pick the 3 active agents. They are selected automatically as the most recent 3 submitted. (So to replace our current agents we need to submit new more recent agents).
> 
> 
> 
> > ## francesco fiamingoTopic Author
> > 
> > Thanks, but i dont understand the logic, at least in testing phase
> > 
> > 
> > 
> > > ## Chris Deotte
> > > 
> > > I don't understand the logic either. 
> > > 
> > > Perhaps Kaggle doesn't want us to be able to turn bots on and off. For example, when our bot achieves a high score, we can then disable our bot to prevent the score from decreasing. Then in the last 1 hour of the competition we can enable the bot and get 1st place public LB.
> > > 
> > > I think our final position in public LB is our seed going into private LB, so maybe what I say above could be an advantage. There are probably other ways to exploit the LB by turning bots on and off whenever we like.
> > > 
> > > 
> > > 


---



</div>
<div class="column-right">

# 日本語訳

# エージェントをキャンセルする方法は？
**フランチェスコ・フィアミンゴ** *2024年7月27日(土) 03:55:41 GMT+0900 (日本標準時)* (3票)
親愛なる友人たちへ、
私はさまざまな設定でいくつかのエージェントを試していますが、時々、良いエージェントをキープしたい一方で、悪いエージェントを代替したいことがあります。しかし、提出したエージェントが「いつ」提出されたかに基づいているため、特定のエージェントをキャンセルし、以前に提出したエージェントを「生かしておく」方法がわかりません。どうすればいいのか教えていただけますか？よろしくお願いします！成功を祈っています。

---
# 他のユーザーからのコメント
> ## クリス・デオッテ
> 
> 私たちは3つのアクティブなエージェントを選ぶことができません。それらは自動的に最近提出された3つのエージェントとして選ばれます。（したがって、現在のエージェントを置き換えるには、新しいエージェントを最近提出する必要があります）。
> 
> > ## フランチェスコ・フィアミンゴ トピック作成者
> > 
> > ありがとう、でもその論理が理解できません。少なくともテスト段階では。
> > 
> > > ## クリス・デオッテ
> > > 
> > > 私もその論理が理解できません。
> > > 
> > > おそらく、Kaggleは私たちがボットをオン・オフできないようにしたいのかもしれません。たとえば、ボットが高いスコアを達成したときに、そのボットを無効にすることでスコアの減少を防ぎ、競技の最後の1時間にボットを有効にして公開リーダーボードで1位を獲得することができます。
> > > 
> > > 最終的な公開リーダーボードでの位置が、プライベートリーダーボードへのシードになると思うので、私の言っていることは有利に働くかもしれません。ボットを好きなときにオン・オフできる他の方法もあるでしょう。


</div>