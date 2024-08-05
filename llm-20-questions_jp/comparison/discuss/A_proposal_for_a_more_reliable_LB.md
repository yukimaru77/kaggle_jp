# 要約 
このディスカッションでは、Kaggleコンペティションのリーダーボードの信頼性についての提案と反応が交わされています。参加者のc-numberは、現在のリーダーボードが運に依存しすぎていると指摘し、特に有限の試合数では結果が不安定になりやすいことを述べています。彼は、運の影響を減らすために2つの新しいゲームタイプ（2人の推測者と1人の回答者、または2人の回答者と1人の推測者）を導入し、レーティングをEloシステムで更新することを提案しています。このアプローチは高レートのプレイヤーと低レートのプレイヤーがより頻繁にペアになることを促し、「愚かさの穴」の問題も回避します。

この提案に対し、他の参加者からは賛否が寄せられています。gguillardは公式な回答者ボットとの対戦を提案し、簡素な実装を提案していますが、loh-maaは新しい提案がゲームの面白さを損なうと反論しています。また、Kha Voは、ルール変更は混乱を招く可能性があるため、現状維持の方が良いと述べています。

全体として、このスレッドはリーダーボードの改善を目指す建設的な議論が展開されつつも、ゲームの楽しさや安定性を考慮した慎重な意見も存在することが示されています。

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

# A proposal for a more reliable LB

**c-number** *Wed Jul 31 2024 23:49:37 GMT+0900 (日本標準時)* (11 votes)

Many participants have pointed out that there's too much of a luck factor in the current LB because wins and losses are heavily dependent on teammates' abilities.

While ratings might converge given an infinite number of games, realistically, we're dealing with a finite number. Looking at [my submissions](https://www.kaggle.com/competitions/llm-20-questions/discussion/520928#2942026), it's unlikely to converge at all in two weeks, at least with the current number of matches.

Additionally, for players with similar abilities, the final result will be heavily influenced by luck (e.g., getting paired with a high- or low-ranked player) in the final few games.

To overcome this problem or at least reduce the dependence on luck, I propose introducing the following two types of games:

2 Guessers, 1 Answerer: Three players are in a game, with two guessers paired with the same answerer. The outcome will depend solely on the guessers' abilities. Only the guessers' ratings will be updated.

2 Answerers, 1 Guesser: Three players are in a game, with two answerers paired with the same guesser. The outcome will depend solely on the answerers' abilities. Only the answerers' ratings will be updated.

In both game types, ratings can be updated using the normal Elo rating system.

This approach not only reduces the luck factor but also addresses the "pit of dumbness" problem by allowing lower-ranked players to be paired with higher-ranked players more frequently (with no risk of losing rates for the high-ranked players).

I understand that changing the ranking system at this stage is technically challenging and may be unfavorable for some participants who rely on luck. However, I believe this change would benefit many others and make the competition's leaderboard more stable and reliable.

I hope the Kaggle staff will consider this proposal.

[@bovard](https://www.kaggle.com/bovard)



---

 # Comments from other users

> ## gguillard
> 
> The simplest solution regarding teams pairing would be to pair all guessers against the same official answerer bot.
> 
> Although it was very fun to randomly pair teams, it's now clear that it only leads to a large scoring injustice because of dummy bots.
> 
> On the other hand, the answerer bot is straightforward to implement, and there's no challenge here.  We could even develop an open source official answerer in a collaborative way.
> 
> Finally, if the hosts still want to assess that each team has a valid answerer bot, it is also straightforward to test, as a single game with yes/no questions is needed.
> 
> 
> 
> > ## loh-maa
> > 
> > This would be a different game rather than a solution. All the effort would focus on the single answering reference bot. Less fun I think.
> > 
> > 
> > 
> > > ## gguillard
> > > 
> > > 
> > > All the effort would focus on the single answering reference bot.
> > > 
> > > What do you mean ?  AFAIK there is only a single right answer to each question between yes or no, no strategy to counter a yesbot or a nobot besides throwing random guesses, and no strategy to recover from several wrong answers…
> > > 
> > > 
> > > 


---

> ## Kha Vo
> 
> Your ideas are great indeed!
> 
> However, I prefer no other competition rule change. It's nearly the end and many of us don't want to deal with some major disruption via this critical time, including moving the submission deadline. (but extending post final evaluation period is a good idea)
> 
> 
> 


---

> ## loh-maa
> 
> In my opinion, if I may, we may assume the current ranking algorithm is temporarily modified and in the final stage it's going to keep evaluating all agents regardless of their score, so this will largely improve the convergence. I think the suggestions are very interesting, but it is already late, indeed. Stability is important, too. Personally I definitely would not appreciate such last minute changes in any competition, even if they were considered good ideas.
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# より信頼性の高いリーダーボードに関する提案
**c-number** *2024年7月31日 水曜日 23:49:37 (日本標準時)* (11票)
多くの参加者が指摘しているように、現在のリーダーボードには運の要素が強すぎます。勝敗はチームメンバーの能力に大きく依存しています。 
無限の試合数があればレーティングが収束するかもしれませんが、実際には有限の試合数で取り組んでいます。私の[提出物](https://www.kaggle.com/competitions/llm-20-questions/discussion/520928#2942026)を見ていると、今の試合数では2週間内に収束するのは難しいでしょう。 
また、能力が似ているプレイヤー同士では、最後の数試合で運の要素（例えば、強いあるいは弱いプレイヤーとペアになること）が結果に大きく影響します。 
この問題を克服するため、あるいは少なくとも運への依存を減らすために、以下の2つのゲームタイプを導入することを提案します：
1. 2人の推測者、1人の回答者：3人のプレイヤーが参加し、2人の推測者が同じ回答者とペアになります。結果は推測者の能力にのみ依存します。レーティングは推測者のものだけが更新されます。
2. 2人の回答者、1人の推測者：3人のプレイヤーが参加し、2人の回答者が同じ推測者とペアになります。結果は回答者の能力にのみ依存します。レーティングは回答者のものだけが更新されます。
どちらのゲームタイプでも、レーティングは通常のEloレーティングシステムを使用して更新できます。 
このアプローチは運の要素を減少させるだけでなく、低レートのプレイヤーが高レートのプレイヤーとより頻繁にペアになることで「愚かさの穴」の問題にも対処します（高レートのプレイヤーがレートを失うリスクがないため）。 
この段階でレーティングシステムを変更することは技術的に難しいことを理解していますし、運に依存している参加者にとっては好ましくないかもしれません。しかし、この変更は多くの他の参加者に利益をもたらし、コンペティションのリーダーボードをより安定させ、信頼性を高めると信じています。 
Kaggleのスタッフがこの提案を検討してくれることを期待しています。
[@bovard](https://www.kaggle.com/bovard)
---
# 他のユーザーからのコメント
> ## gguillard
> 
> チームのペアリングに関して最も簡単な解決策は、すべての推測者を同じ公式回答者ボットと対戦させることです。 
> 
> チームをランダムにペアにするのは非常に楽しいことでしたが、今はそれが愚かなボットのためにスコアの不公平を引き起こすことが明らかです。 
> 
> 一方、回答者ボットは実装が簡単で、挑戦はありません。私たちは、オープンソースの公式回答者を協力的に開発することもできます。 
> 
> 最後に、ホストが各チームに有効な回答者ボットがあるかを評価したい場合でも、yes/noの質問を使った単一のゲームでテストするのは簡単です。

> ## loh-maa
> 
> これは解決策ではあまりにも異なるゲームになると思います。すべての努力が単一の回答参考ボットに集中します。あまり面白くないと思います。

> > ## gguillard
> > 
> > > すべての努力が単一の回答参考ボットに集中します。 
> > > 何を意味していますか？私の知る限り、yesかnoの間に正しい答えは一つしかなく、yesボットやnoボットに対抗する戦略はなく、ランダムな推測を投げること以外にありません。そして、いくつかの誤った答えから回復する戦略もありません…
> > 
> > 
---
> ## Kha Vo
> 
> あなたのアイデアは本当に素晴らしいです！ 
> 
> しかし、私は他の競技ルールの変更を希望しません。ほぼ終了の時期であり、多くの人はこの重要な時期に大きな混乱に直面したくありません。それには提出期限を延ばすことも含まれます（ただし、最終評価期間を延長するのは良い考えです）。

---
> ## loh-maa
> 
> 私の意見では、現在のレーティングアルゴリズムが一時的に修正され、最終段階でスコアに関係なくすべてのエージェントを評価し続けると仮定すれば、収束が大幅に改善されるでしょう。この提案は非常に興味深いですが、確かに遅すぎます。安定性も重要です。個人的には、こうした最後の瞬間に変更があるのは、たとえ良いアイデアであっても、あまり嬉しく思いません。 
> 
---


</div>