# 要約 
このディスカッションでは、コンペティション内で古いエージェントが削除される理由についての議論が行われています。ユーザー**d1v1s10n_by_zer0**は、新しい仮説を試すためには、最も評価の高いエージェントを削除する必要があると示唆していますが、古い提出物と入れ替える可能性について提起しています。

その後、ユーザー**Jasper Butcher**は、ランキングがあまり意味を持たないと述べ、ボットのスコアが日によって大きく変動することを経験として語っています。彼は安定した評価が得られず、オフラインでのボットのテストを検討していることも明かしています。

ユーザー**Hadeka**も同様に、同一のエージェントから提出したボットのスコアが大きく変動した体験を共有し、LLMの生成の安定性が難しいことを指摘しています。彼もオフラインでのテストを考えているが実行していないことを軽く述べています。

全体的に、エージェントの評価が不安定であることに対する不満と、効果的なテスト方法についての探索が中心の議論として展開されています。また、ログイン時のエージェントの提出数の制限に対する解決策も提案されています。

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

# Why is the oldest agent being deleted and not the agent with the worst results?

**d1v1s10n_by_zer0** *Thu Jul 11 2024 08:23:29 GMT+0900 (日本標準時)* (4 votes)

I would like to try new hypotheses, but for that I have to remove the agent with the highest rating. Is it possible to replace new agents with the worst of my attempts rather than the best (in my case, it coincides with the oldest shipment)?



---

 # Comments from other users

> ## Jasper Butcher
> 
> Doesn't seem so. Just lose the ego & document the old code, rankings don't matter.
> 
> 
> 
> > ## Hadeka
> > 
> > What do u mean by “ranking don’t matter”?
> > 
> > Isn’t an evidence that this code can overcome others, and can somehow defend itself from other codes to overcome it?
> > 
> > Or am I missing something?
> > 
> > 
> > 
> > > ## Jasper Butcher
> > > 
> > > You're right, perhaps it's a bit of a blanket statement but I mean in the long-term they won't provide you much information because I've found the rankings are super volatile.
> > > 
> > > I submitted 3 identical bots, and after 3 days they had scores ranging from 800, 700 and 500. You win once by chance, you shoot up, you lose once, you're stuck with lobotomized bots which give you no information whatsoever. I simply don't have time to wait a week for the rankings to stabilize - even then though, this is very slow signal.
> > > 
> > > It's really really hard to submit one decent bot, make some changes, and submit an improved one and use the difference in ranking to see if that truly improved it.
> > > 
> > > I'm leaning towards trying to test bots offline? Not sure if people have tried doing this?
> > > 
> > > 
> > > 
> > > ## Hadeka
> > > 
> > > Well I totally agree with you.
> > > 
> > > I’ve did the same actually, submitted 3 identical agents, their score ranged from 470 to 890. My rank was 360, then after few hours, I’m the 20th! All with the same agent, same submission.
> > > 
> > > My 3 identical agents, one kept around 400, the second is around 600, and the third between 800 and 900!
> > > 
> > > It’s not really weird, but stabilizing LLM generations  is actually too hard, almost impossible to do it 100%. We tried a lot in the past AIMO here on Kaggle, but you can only relatively reduce its instability, but you cannot eliminate it. That’s anyway one of the key factors that define LLMs, but for that kind of research (and competitions), it’s really annoying.
> > > 
> > > I was thinking about testing it offline, but haven’t done so, yet.
> > > 
> > > 
> > > 
> > > ## Jasper Butcher
> > > 
> > > My guess is that testing offline wouldn't be needed as much if we could just select one bot to put all of our games quota to. Best work-around is just to submit all of your daily allowance. I sympathise with the hosts though, not an easy competition to run!
> > > 
> > > 
> > > 


---



</div>
<div class="column-right">

# 日本語訳

# なぜ古いエージェントが削除され、結果が最も悪いエージェントが削除されないのか？
**d1v1s10n_by_zer0** *2024年7月11日 08:23:29 JST* (4票)
新しい仮説を試してみたいのですが、そのためには最高評価のエージェントを削除する必要があります。最良の結果を出せなかったエージェントを削除するのではなく、最も古い提出物と入れ替えられるようにしたりできますか？

---
# ユーザーからのコメント
> ## Jasper Butcher
> 
> そう見えませんよ。プライドを捨てて古いコードを文書化するだけです。ランキングなんてあまり関係ありません。

> ## Hadeka
> 
> 「ランキングは関係ない」とはどういう意味ですか？
> > 他のコードを上回ることができる証拠ではないですか？また、他のコードに打ち勝つために、何らかの形で自分を守ることができるのではないでしょうか？
> > 
> > それとも私が何かを見逃しているのでしょうか？

> > > ## Jasper Butcher
> > > おっしゃる通りです。少し漠然とした言い方でしたが、長期的には多くの情報を提供してくれないと思います。私の経験では、ランキングは非常に変動しやすいです。
> > > 
> > > 同一のボットを3つ提出したところ、3日間でスコアが800、700、500と様々でした。一度運良く勝つと急上昇し、負けると意味のないボットに固まってしまう。それに、私はランキングが安定するまで待つ時間がありません - それでも非常に鈍い信号です。
> > > 
> > > 一つのまともなボットを提出し、少し修正して改良版を提出し、ランキングの差を見て本当に改善されたかを評価するのは非常に難しいです。
> > > 
> > > 私はオフラインでボットをテストしてみようかと考えていますが、みんなが試したのかどうかは分かりません。

> > > ## Hadeka
> > > まったく同意します。
> > > 同様に、私も同一のエージェントを3つ提出しましたが、スコアは470から890まででした。私のランキングは360だったのが、数時間後には20位に！すべて同じエージェント、同じ提出物で。
> > > 
> > > 私の3つの同一エージェントは、一つが約400、二つ目が約600、三つ目が800から900の間を維持していました！
> > > 
> > > これは本当に不思議ではありませんが、LLMの生成を安定させるのは非常に難しく、完全に行うことはほぼ不可能です。過去のAIMOで多くの試みがありましたが、安定性を相対的に減少させることしかできず、完全に排除することはできません。それはLLMを定義する重要な要素の一つですが、こういった研究やコンペティションには本当に厄介です。
> > > 
> > > オフラインでのテストについて考えていましたが、まだ実行していません。

> > > ## Jasper Butcher
> > > 私の考えですが、オフラインでのテストが必要なくなるのは、もし可能なら、すべてのゲーム計画を一つのボットに集約できればということです。一番の解決策は、日々の提出上限をすべて出すことです。ホストの方々には同情しますが、簡単なコンペティションではありません！


</div>