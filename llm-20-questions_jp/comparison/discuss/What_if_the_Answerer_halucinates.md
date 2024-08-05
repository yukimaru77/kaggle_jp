# 要約 
このディスカッションでは、コンペでの回答者LLMが間違った答えを返した場合の影響について話し合われています。**FelipeDamasceno**が、間違った回答が評価にどのようなペナルティを与えるかを懸念し、間違いを知る方法について質問しました。**Nicholas Broad**は、間違った回答をしたLLMは評価が下がり、能力の低いモデルとペアにされると説明しました。**Bovard Doerschuk-Tiberi**は、頻繁に間違った回答をするエージェントは試合に勝てず評価が低下するが、他の試合では別のパートナーと高評価を得ることができる可能性があると述べました。**Aatif Fraz**も、協力型の形式では良いチームメイトに恵まれることが重要であると同意しました。全体として、回答者LLMのパフォーマンスがチームの成功に大きく影響するという見解が示されています。

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

# What if the Answerer halucinates

**FelipeDamasceno** *Sat May 18 2024 22:33:15 GMT+0900 (日本標準時)* (3 votes)

Hello everyone, I am not sure if I understood everything about the evaluation, but it seems to me that the one who will be answering the questions is also a LLM, so I was wandering, what if the LLM that answers the questions give the wrong answer? In that case the other LLM will not be able to get the right secret word. Is there something in the evaluation that penalize the LLM in this case? Is there a way to know if the LLM answered the question wrong?



---

 # Comments from other users

> ## Nicholas Broad
> 
> The penalty is that you are less likely to win the game. You will drop in the rankings and get paired with bad models
> 
> 
> 
> > ## FelipeDamascenoTopic Author
> > 
> > but, is it the penalty for the bad answerer or the model playing against it? Because you can have a model that is good at making questions and finding the secret word, but the answer to questions is not really good as the idea is to have two different models, one for questions and finding the model and other to answer to questions, correct? 
> > 
> > 
> > 
> > > ## Bovard Doerschuk-Tiberi
> > > 
> > > Each submission has a ranking that changes after each match. An agent that often responds incorrectly will most likely never win a match (and thus consistently drop in rating).
> > > 
> > > Yes, for that match the model paired with the bad answerer will also lose rating for that game, but can go on to gain rating with other partners in other matches.
> > > 
> > > Note that since you are matched with agents around your skill level, this becomes less of a problem the higher in the leaderboard you go.
> > > 
> > > 
> > > 


---

> ## Aatif Fraz
> 
> Yes, then that team is doomed, the answerer LLM as well. It is a cooperative 2v2, you have to get lucky with teammates I guess. 
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# 回答者が幻覚を起こした場合
**FelipeDamasceno** *2024年5月18日 22:33:15 JST* (3票)
皆さん、評価についてすべて理解しているか不安ですが、質問に答えるのもLLMであるようなので、気になったのですが、もし質問に答えるLLMが間違った答えを返したらどうなるのでしょうか？その場合、もう一方のLLMは正しい秘密の単語を見つけることができなくなります。評価方法には、そういった場合にLLMにペナルティを与えるような仕組みはありますか？回答が間違っているかどうかを知る方法はあるのでしょうか？

---
## 他のユーザーからのコメント
> ## Nicholas Broad
> 
> ペナルティは、ゲームに勝つ可能性が低くなることです。ランキングが下がり、能力の低いモデルとペアにされることになります。

> > ## FelipeDamasceno（トピック作成者）
> > 
> それは悪い答えを出すLLMへのペナルティなのか、それとも対戦相手のモデルへのペナルティなのか？質問を上手に作成し秘密の単語を見つけることが得意なモデルがある一方で、答えはあまり良くない場合もあり得ますよね。基本的には、質問への回答を担当するLLMと質問を担当するLLMの2つが必要という理解で合っていますか？

> > > ## Bovard Doerschuk-Tiberi
> > > 
> > 各提出物は、試合ごとにランキングが変わります。頻繁に間違った回答をするエージェントは、ほぼ確実に試合に勝てず（その結果、評価が下がることになります）。  
> >  
> > はい、その試合では悪い回答者とペアを組んだモデルもその試合のために評価が下がりますが、他の試合で別のパートナーと一緒に高評価を得ることも可能です。  
> >  
> > スキルレベルが同じエージェントとマッチングされるため、リーダーボードで上位に行くほど、この問題は軽減されます。

> > > > 
---
> ## Aatif Fraz
> 
> そうですね、そのチームは厳しい状況になります。回答者のLLMも同様です。協力型の2対2の形式なので、運良く良いチームメイトに恵まれないといけませんね。


</div>