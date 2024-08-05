# 要約 
### ディスカッション要約

**タイトル：コンペティションのスコアリングシステムに関する懸念とその改善案**

参加者のKha Voは「20の質問ゲーム」のスコアリングシステムに対する懸念を表明しました。主な問題点は以下の通りです：

1. **競争性の欠如**:
   現在の競技形式では、質問者と回答者のパフォーマンスが他のチームに影響を与えないため、真の対戦要素が不足しています。Kha Voは、単独の「テスト」チームを形成する方が、有効な指標になると主張しました。

2. **引き分けによる影響**:
   引き分けが多いため、高ランクボットは減点され、低ランクボットは得をする不公平が生じています。Kha Voは、勝利や引き分けに対するポイントの配分を再考する必要があると提案しました。

Kha Voは、スコアリングの調整案を示し、具体的には、質問者と回答者の能力を均等に評価する新たなメトリックの導入を提案しました。

**他のユーザーの意見**:
- Bovard Doerschuk-Tiberiは、スコアリングアルゴリズムの改善を検討しており、引き分け時のポイント減少の見直しを進めています。
- その他の参加者も、エージェントのペアリング方法やその切り替えによる公平性の必要性を指摘し、サンプルキーワードの頻繁な更新を求めています。

全体的に、参加者たちは競技性の向上と公正なスコアリングシステムを求めており、ホスト側の改善を期待しています。

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

# Some real concerns over the competition' scoring system (and proposals how to fix it)

**Kha Vo** *Tue Jun 04 2024 11:42:45 GMT+0900 (日本標準時)* (8 votes)

Hi Kaggle Team,

I am truly interested in competing in this competition, but the concerns raised below also truly made me lose most interest in it. I hope you can review and make comments or adjustment to the game design, to attract more people into the contest.

1. There are no true competitiveness in the match-up

Unlike all of the previous Kaggle simulation competitions (Halite, Rock/Paper/Scissors, Snake, ….) where there are real "versus" match, this "20 Questions Game" actually does NOT have any aspects for the "versus" at all. In specific, how a team (composed of a questioner and an answerer) performs in a match does NOT have any impact to the opponent's team. As a result, pairing to form a match-up makes no sense. Indeed, just forming 1 team for a single "testing" and count the number of questions needed to guess the correct keyword should be a much better metric on the LB.

2. Tied games (games resulting a draw) are so populous, devastating to the higher ranked bots, and inexplicably rewarding to the lower ranked bots

Since the match-up is not truly competitive at all (explain in point 1), it is converged to the notion that each bot just needs to care for its own sake, not caring anything else, not even the opponent's team. However, this is still so far to guess the correct keyword. The perfect questioner still depends heavily on the answerer to be able to correctly guess the keyword.

In short, to actually "WIN" a game is so difficult. It needs to have 3 following aspects to form a win: a) The questioner must be very good in playing "20 questions". b) The answerer must be at least a valid (and good) LLM. and c) No error formed by any of the 4 bots

I saw one of my bots amazingly guessed out the keyword in 4 steps, got 45 points on the LB, jumped to 1st place. Then, in 3 next consecutive games it acts as the answerer and at least draws all games, but still got heavily deducted until it cancels out that amazing win.

The ratio between a good win and the tied games is extremely low. Hence, the mechanism of point deduction in tied games for higher ranked bots (and also increasing points for lower bots) need to be rectified, otherwise good bots can never surface on the top of the LB.

However, making rectifying on the scoring like that still poses some other weaknesses that we still can't foresee. I still prefer changing the match-up format to the "testing" metric, that is: single question-answerer pairing only with no matchup, and LB is based on the average metric such as:

0.8* (average number of questions needed to guess correctly as the questioner) + 0.2 * (average number of questions needed to guess correctly as the answerer)

Please have a look and my points.

[@bovard](https://www.kaggle.com/bovard) [@addisonhoward](https://www.kaggle.com/addisonhoward) [@mylesoneill](https://www.kaggle.com/mylesoneill) 



---

 # Comments from other users

> ## Bovard Doerschuk-Tiberi
> 
> Thanks for your thoughtful post, we are looking into options for getting better ratings signals. Will update when we have something to share!
> 
> 
> 
> > ## Bovard Doerschuk-Tiberi
> > 
> > We've adjusted the scoring algorithm to increase the rating gain/loss from win/loss and reduce the rating gain/loss from ties. This should be live now but it may take us a bit to dial it in correctly.
> > 
> > 
> > 
> > > ## Bovard Doerschuk-Tiberi
> > > 
> > > You can see the effects of this new scoring paradigm here: [https://www.kaggle.com/competitions/llm-20-questions/leaderboard?dialog=episodes-submission-38522755](https://www.kaggle.com/competitions/llm-20-questions/leaderboard?dialog=episodes-submission-38522755)
> > > 
> > > Losing < 5 points for a tie and getting 50+ for a win
> > > 
> > > 
> > > 
> > > ## Kha VoTopic Author
> > > 
> > > [@bovard](https://www.kaggle.com/bovard) I think losing points in tied games must also be strictly positive although can be small (a good team must be deducted at least 1 point in tied game with lower bots). It can't be 0 otherwise you'll have many local minima on the LB, all will come to luck when a new bot is submitted: who will it be paird to.
> > > 
> > > 
> > > 
> > ## Kha VoTopic Author
> > 
> > That looks better! Thanks Bovard. 
> > 
> > 
> > 


---

> ## tr
> 
> I think pairing just 2 agents (both as questioner and answerer) instead of 4 different engines would solve most problems with scoring system and still keep the original goal of the competition. Probably also a minor change for the hosts, but the scoring should also change, since there is no more competitiveness between pairs.
> 
> 
> 
> > ## JavaZero
> > 
> > This can lead to malicious misdirection and prevent the adversary from guessing the correct key word
> > 
> > 
> > 
> > > ## Kha VoTopic Author
> > > 
> > > [@jimmyisme1](https://www.kaggle.com/jimmyisme1) How?
> > > 
> > > 
> > > 


---

> ## Giba
> 
> I posted about it last week but got no reaction at all. LB right now is a periodic random shuffle. Only hosts can fix the scoring system.
> 
> To be fair, agents should simply alternate between questioner and answerer at each game. Guessers agent should be given much more points than answerers. A Draw should give zero (or -1) points to everyone independent of the level/skill.
> 
> 
> 
> > ## Kha VoTopic Author
> > 
> > Right Giba. The most annoying part is that a bad answerer will damage the good guesser so much
> > 
> > 
> > 


---

> ## RS Turley
> 
> Many of these problems arise from there being very little differentiation across rankings in the early leaderboard—so low quality agents are getting matched in with high quality ones and dragging them down. 
> 
> Even a small change (like this week’s keyword update?) that creates more differentiation in LB scores might solve these issues as low quality agents drop in score and high quality agents match with each other more frequently. 
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# コンペティションのスコアリングシステムに関する懸念とその改善案
**Kha Vo** *2024年6月4日(火) 11:42:45 GMT+0900 (日本標準時)* (8票)
Kaggleチームの皆さんへ、
このコンペティションに参加することにとても興味がありますが、以下の懸念により興味を失いつつあります。ぜひゲームデザインを検討し、コメントや調整を行って、もっと多くの人をコンテストに引き込んでいただければと思います。

1. 対戦の真の競争性がない
過去のKaggleシミュレーションコンペ（Halite、Rock/Paper/Scissors、Snakeなど）では、実際に「対戦」が存在しましたが、この「20の質問ゲーム」には「対戦」と呼べる要素が全くありません。具体的には、質問者と回答者から構成されるチームのパフォーマンスが、対戦相手のチームに全く影響を及ぼさないため、マッチアップを形成する意味がありません。実際、単一の「テスト」チームを形成し、正しいキーワードを推測するのに必要な質問数をカウントする方が、リーダーボードにおいてはるかに良い指標となるでしょう。

2. 引き分けが多く、高ランクのボットにとっては壊滅的で、低ランクのボットにとっては説明のつかない恩恵となる
対戦が真に競争的でないため（1点目で説明した通り）、各ボットは自分自身のことだけを気にするようになり、対戦相手に対しても無関心になります。しかし、正しいキーワードを推測するためには、完璧な質問者も回答者の能力に依存してしまいます。
要するに、実際に「勝つ」ことは非常に難しいのです。勝つためには、以下の3つの要素が必要です：
a) 質問者が「20の質問」を上手くプレイすること
b) 回答者が、少なくとも妥当で良いLLMであること
c) 4つのボットのいずれかでもエラーを起こさないこと
私のボットの一つが、驚くことに4ステップでキーワードを推測し、リーダーボードで45ポイントを獲得して1位に躍り出ました。しかし、それ以降の3つのゲームでは回答者としてプレイし、すべてのゲームを引き分けに持ち込んだものの、ポイントが大幅に減点され、その素晴らしい勝利が帳消しになってしまいました。
良い勝利と引き分けの比率は極めて低いため、引き分けに対する高ランクボットのポイント減点のメカニズム（および低ランクボットへのポイント増加）を修正する必要があります。そうでないと、良いボットがリーダーボードの上位に浮上することは決してありません。
しかし、そのようにスコアリングを修正することは、見えない他の弱点を生じる恐れがあります。私はマッチアップ形式を「テスト」メトリック、すなわち質問者と回答者のペアリングのみで対戦は行わず、リーダーボードは次のような平均メトリックに基づくべきだと考えています：
0.8 * (質問者として正しく推測するのに必要な平均質問数) + 0.2 * (回答者として正しく推測するのに必要な平均質問数)
ぜひ私の意見をご覧ください。
[@bovard](https://www.kaggle.com/bovard) [@addisonhoward](https://www.kaggle.com/addisonhoward) [@mylesoneill](https://www.kaggle.com/mylesoneill)

---
# 他のユーザーからのコメント
> ## Bovard Doerschuk-Tiberi
> 
> 貴重な投稿をありがとうございます。より良いレーティングシグナルを得るための選択肢を検討しています。何か共有できることがあれば更新します！
> 
> > ## Bovard Doerschuk-Tiberi
> > 
> > スコアリングアルゴリズムを調整し、勝利/敗北からのレーティングの増加/減少を増大させ、引き分けからのレーティングの増加/減少を減少させました。これが今反映される予定ですが、正確に調整するには少し時間がかかるかもしれません。
> > 
> > > ## Bovard Doerschuk-Tiberi
> > > 
> > > この新しいスコアリングパラダイムの効果をここで見ることができます：[https://www.kaggle.com/competitions/llm-20-questions/leaderboard?dialog=episodes-submission-38522755](https://www.kaggle.com/competitions/llm-20-questions/leaderboard?dialog=episodes-submission-38522755)
> > > > 引き分けで-5ポイント、勝利で50ポイント以上を得られるようになっています。
> > > 
> > > 
> > > ## Kha Vo トピック作成者
> > > > [@bovard](https://www.kaggle.com/bovard) 引き分けのゲームでのポイント減少は、厳格にプラスであるべきだと思います（小さくても）。良いチームは、引き分けの際には少なくとも1ポイント減点されるべきです。0になれば、リーダーボード上で多くの局所的なミニマが発生し、新しいボットが提出された際に、どのボットとペアリングされるかによって運が左右されてしまいます。
> > > 
> > > ## Kha Vo トピック作成者
> > > > より良い方向に向かっているようですね！ありがとうございます、Bovard。

---
> ## tr
> 
> エージェントを2つ（質問者と回答者）だけのペアにすることで、スコアリングシステムのほとんどの問題が解決され、コンペティションの本来の目標も維持できると思います。おそらくホスト側での小さな変更ですが、対戦の競争性がなくなるためスコアリングの変更も必要です。
> 
> > ## JavaZero
> > 
> > これにより、悪意のある誤誘導が生じ、対戦相手が正しいキーワードを推測することを妨げる可能性があります。
> > 
> > > ## Kha Vo トピック作成者
> > > > [@jimmyisme1](https://www.kaggle.com/jimmyisme1) それはどういう意味ですか？

---
> ## Giba
> 
> 先週このことについて投稿しましたが、全く反応がありませんでした。現状のリーダーボードは周期的にランダムにシャッフルされています。ホスト側の修正が必要です。
> 
> フェアにするためには、エージェントは各ゲームで質問者と回答者を交互に行うべきです。推測エージェントには、回答者よりもはるかに多くのポイントを与え、引き分けにはすべてのボットに対してゼロ（または-1）ポイントを与えるべきです。
> 
> > ## Kha Vo トピック作成者
> > > そうですね、Giba。最も苛立たしいのは、悪い回答者が良い推測者を非常に大きく損なうことです。

---
> ## RS Turley
> 
> これらの問題の多くは、初期のリーダーボードにおけるランク間での差が非常に少ないことに起因しています。そのため、低品質のエージェントが高品質のエージェントと対戦し、彼らを引きずり下げてしまうのです。
> 
> 少しの変更（今週のキーワードのアップデートなど）でも、リーダーボードのスコアに差別化をもたらすかもしれません。低品質のエージェントがスコアを下げ、高品質のエージェントがより頻繁に互いにマッチするようになるでしょう。


</div>