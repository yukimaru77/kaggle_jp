# 要約 
このディスカッションは、Kaggleの「LLM 20 Questions」コンペティションにおけるランキングシステムの公平性に関する懸念を中心に展開されています。ユーザー「gguillard」は、自らの初回提出のエピソードと他の参加者の懸念を踏まえ、ランキングがスキルの近い相手との対戦で収束しない可能性を指摘しています。また、同じモデルが異なるランクに入ることがある現象を挙げ、この評価システムの妥当性に疑問を呈し、改善を提案しています。

他の参加者が彼の意見に同意し、特にエラーが発生したボットに対するペナルティや、過去のパフォーマンスを反映するための対戦回数の増加などのアイデアを提案しています。また、新しいボットの頻繁なプレイや、回答者のランダムな組み合わせが参加者にとって公平性を増すかもしれないとの意見も述べられています。

全体として、評価システムの修正についての議論が活発であり、参加者たちはより公正で実力が反映された順位付けを求めています。

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

# Is this competition a lottery, or is it not ?

**gguillard** *Sat Jul 20 2024 21:47:38 GMT+0900 (日本標準時)* (11 votes)

No offense to the Kaggle team, but I was quite puzzled after watching episodes from my first submission and reading many concerns in discussions, so I had to convince myself of the fairness of the ranking system in order to decide if it was worth investing more time in this competition.

Therefore I made a small toying notebook to play with it :

[https://www.kaggle.com/code/gguillard/llm-20-questions-trueskill-simulator](https://www.kaggle.com/code/gguillard/llm-20-questions-trueskill-simulator)

I was really hoping it would prove my intuition wrong, but it didn't.  On the contrary, assuming there's no serious flaw in my investigation, my finding is that the ranking never converges enough to distinguish between opponents of not-so-similar skills :

Hopefully I got some parameter wrong and the organizers will point it out, otherwise it is not too late to amend the ranking system.

Amongst many discussions about this subject, I think [the spectacular example recently shown by ](https://www.kaggle.com/competitions/llm-20-questions/discussion/520928)[@c-number](https://www.kaggle.com/c-number), where the same model posted at the same date is ranked both 1st, 6th and and 60th (!) on the current leaderboard, is quite convincing that there is no point in using the current evaluation system.

In its current state, the competition is indeed a (biased, but still) lottery.  Not that I have anything against lotteries, but it's good to know when it's one, because it's better not to expect too much of it.

If they want the competition to be meaningful in terms of rewarding the best submissions, I urge the host to reconsider the ranking options.  It'd be a pity if the competition was despised because of its scoring system, because that's really a fun competition.

[@bovard](https://www.kaggle.com/bovard) [@addisonhoward](https://www.kaggle.com/addisonhoward)

PS : Maybe that changed with the latests improvements of my notebook (I didn't check), but from my firsts tests the TrueSkill system didn't seem very stable whatever the combination of parameters for such a competition.  For what it's worth, I'd just go for a plain n_wins ranking (guesser + answerer), with a fixed number of games per submission.

Edit :

Here are the leaderboards for 4 such experiments with just a different random seed (see the bottom of the last version of the notebook) :

```
Leaderboard 1
rank    id  skill   mu
1        1   0.98    977
2        4   0.77    985
3        0   0.98    962
4        2   0.96    926
5        20  0.43    978

Leaderboard 2
rank    id  skill   mu
1        0   0.98    1021
2        2   0.96    925
3        9   0.58    974
4        4   0.77    854
5        8   0.59    941

Leaderboard 3
rank    id  skill   mu
1        1   0.98    1019
2        0   0.98    1038
3        2   0.96    1014
4        4   0.77    913
5        5   0.73    988

Leaderboard 4
rank    id  skill   mu
1        4   0.77    969
2        8   0.59    978
3        1   0.98    912
4        0   0.98    948
5        3   0.82    986

```



---

 # Comments from other users

> ## Andrew Tratz
> 
> I think this reflects a few realities of this competition as it currently stands:
> 
> The highest-ranked bots still lose the majority of their games.
> Some of the high-ranking bots are relying on the public keyword list and may not be robust when the private list is released
> Pairing two bots together compounds this randomness
> Wins seem to be awarded lots of points, losses do not seem to decrease points as rapidly
> When a bot errors, all others receive a win
> Relatively slow frequency of games played for "mature" bots
> 
> This means a few lucky wins will cause a quick jump on the LB but a fairly slow decay. Using over-reliance on the keyword list may allow bots to remain on top for a while but also expose them to risk when private keywords are released.
> 
> I think the organizers should change #5 to have the error bot penalized but give no reward to the other players, since this just adds distortion. It makes sense in other simulation competitions but perhaps not this one. Perhaps some tweaks would help with #4 as well.
> 
> I imagine we'll see some healthy shake-up on the private LB, although this shake-up may also be somewhat random unless a few people come up with distinctly better bots.
> 
> 
> 
> > ## OminousDude
> > 
> > I think the shake-up on private will be quite massive too. I am almost fully convinced everyone in the top ~25 uses the public LB keywords list.
> > 
> > 
> > 
> > > ## VolodymyrBilyachat
> > > 
> > > Nope my agent doesn't know about keywords but it has only categories. But unfortunately this is very much luck based. 
> > > 
> > > 
> > > 
> > ## gguillardTopic Author
> > 
> > Bots relying on the public keyword list is the responsibility of their developers, it's not the matter of the organizers IMO — although I am curious if non-LLM or part-LLM bots may be disqualified, since it's an LLM competition.
> > 
> > Point #4 is slightly wrong : you're confusing losses with draws.  The relation between a win and a loss is roughly symmetric, although it depends on the different mu and sigma of the players.  Anyway this is by design, due to the TrueSkill settings (see notebook), and I believe it was deliberately chosen by the hosts.
> > 
> > 
> > 
> > > ## loh-maa
> > > 
> > > No disqualifications should/can be applied on a whim, there must be solid grounds to do so. Since there are no specific rules regarding techniques, then presumably all techniques are allowed (except cheating in general of course.) And surely it is way too late to change the rules.
> > > 
> > > 
> > > 


---

> ## OminousDude
> 
> I fully agree and believe that this is a massive problem and I sincerely hope that the competition hosts find a way to fix this.
> 
> One way this score deviation could be minimized is by removing agents that have not had a single win in the last ~50 rounds. This will stop them from bringing down agents at the top of the leaderboard as low bots and high bots will sometimes be placed with each other to help overcome the "pit of dumbness" that comes between scores ~650 down to zero.
> 
> Another way is to play the game three times instead of one so that each agent will play against each other. For example, if round one is won by team a consisting of agent1 and agent2, in the next round agent1 will go against agent3 and then agent4, this way each agent will play each other model. The second option would fix the problem of one questioner agent getting a "bad" answerer. If no one wins any round then the default points will be given. If 2 rounds are won the agent that is included in both of the winning teams will get a boost and the other agents in those rounds that only won one round will get a smaller (but still substantial) reward.
> 
> Finally, a third way to fix this could be if one agent constantly loses/does not win the other agent in its team will get a small boost (+10 or so) and the losing bot will lose a bit (-10 or so) this will split bots that win and lose quicker so that the bots that actually can play and win will be playing against higher level bots.
> 
> I hope the competition hosts consider at least one of these options (preferably the second and third ones). Such small changes as I have described above will make massive changes to the "lottery" aspect of the scoring.
> 
> 
> 
> > ## gguillardTopic Author
> > 
> > The good thing is that all these options are now straightforward to test through the simulator notebook, so they can decide which is best based on facts.
> > 
> > 
> > 
> > > ## OminousDude
> > > 
> > > Oh yes, I just realized that! I suggest that we run a few of the possible strategies on your notebook to find the best.
> > > 
> > > 
> > > 
> > > ## gguillardTopic Author
> > > 
> > > As far as I'm concerned I will try to focus for a while on making a second submission. :D
> > > 
> > > But if the hosts acknowledge that they're open to modifying the evaluation I'll be happy to help if needed.
> > > 
> > > 
> > > 


---

> ## loh-maa
> 
> There is much confusion and good reasons to wonder what's going, on especially for new players. If you notice, any agent reaching the score of around 750, suddenly stops playing frequently and plays only a game or two a day. This obviously affects the LB and I'm pretty sure it's going to be reverted to normal in the final stage. I'm not really sure why this alteration has been introduced but it could be to obscure real performance, it could help in preventing particular solutions from gaining too much of critical mass and thus spoiling the whole thing. So, anyway, I think there's no need to worry, join in with your best ideas!
> 
> 
> 


---

> ## VolodymyrBilyachat
> 
> Wouldn't answerer mixture of answerers improve this competition? I see the single answer is driving into completely wrong direction :( It wont solve the problem for 100% but still could improve alot
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# このコンペティションは宝くじなのか、それともそうではないのか？
**gguillard** *2024年7月20日(土) 21:47:38 JST* (11票)
Kaggleチームに対して失礼になるかもしれませんが、自分の初回提出のエピソードを見たり、ディスカッションでの多くの懸念を読んだりした後、ランキングシステムの公平性にかなり混乱しました。そのため、もっと時間を投資するべきかを決定するために、自分なりにランキングシステムの妥当性を納得させる必要がありました。そこで、少し楽しみながら試せるノートブックを作成しました：
[https://www.kaggle.com/code/gguillard/llm-20-questions-trueskill-simulator](https://www.kaggle.com/code/gguillard/llm-20-questions-trueskill-simulator)
自分の直感が間違っていることを証明できることを期待していましたが、逆にそうではありませんでした。私の調査に深刻な欠陥がないと仮定すると、ランキングは相手のスキルがあまりにも似ていない場合、十分に収束しないことがわかりました。
何かパラメータを間違えたのかもしれませんが、主催者が指摘してくれることを願っています。さもなければ、ランキングシステムを修正するのはまだ遅くありません。この件に関しての多くの議論の中で、最近[@c-number](https://www.kaggle.com/c-number)によって示された雄大な例（同じモデルが同じ日付に1位、6位、60位にランクインされる）は、現在の評価システムを使用する意味がないことを非常に納得させられました。現状のままでは、このコンペティションは実際には（偏ったついでの）宝くじです。宝くじ自体には何の問題もないわけではありませんが、宝くじであることを知っておくことは良いことです。期待を過剰に持たない方がいいですからね。
もし彼らがコンペティションを賞金を得る上で意味のあるものにしたいなら、評価オプションを再考することを強くお勧めします。このスコアリングシステムのせいでコンペティションが嫌われるのは残念です。本当に楽しいコンペティションなのですから。
[@bovard](https://www.kaggle.com/bovard) [@addisonhoward](https://www.kaggle.com/addisonhoward)
追記：もしかしたら私のノートブックの最近の改良で何かが変わったのかもしれませんが（確認していません）、私の初期のテストではTrueSkillシステムはこのコンペティションのためには非常に不安定であるように見えました。そんなことも考慮して、単純な勝利数のランキング（質問者 + 回答者）で、各提出物につき固定数のゲームを行うのが最良だと思います。

編集：
以下、異なるランダムシードでの4つの実験のリーダーボードを示します（ノートブックの最新版の下部を参照）：
```
リーダーボード1
ランク    ID  スキル   mu
1        1   0.98    977
2        4   0.77    985
3        0   0.98    962
4        2   0.96    926
5        20  0.43    978
リーダーボード2
ランク    ID  スキル   mu
1        0   0.98    1021
2        2   0.96    925
3        9   0.58    974
4        4   0.77    854
5        8   0.59    941
リーダーボード3
ランク    ID  スキル   mu
1        1   0.98    1019
2        0   0.98    1038
3        2   0.96    1014
4        4   0.77    913
5        5   0.73    988
リーダーボード4
ランク    ID  スキル   mu
1        4   0.77    969
2        8   0.59    978
3        1   0.98    912
4        0   0.98    948
5        3   0.82    986
```
---
# 他のユーザーからのコメント
> ## Andrew Tratz
> 
> 現在のコンペティションの現実を反映していると思います：
> 
> 最高ランクのボットでも、ゲームの大半を失っています。
> いくつかの高ランクのボットは公開されたキーワードリストに依存しており、プライベートリストが公開されると堅牢でなくなる可能性があります。
> ボットをペアにすることで、このランダム性が増します。
> 勝利にはたくさんのポイントが与えられ、敗北はそれほど急速にポイントを減少させていないようです。
> ボットにエラーが発生すると、他のすべてのボットが勝利を受け取ります。
> "成熟した”ボットに対しては、ゲームのプレイ頻度が比較的低いです。
> 
> これにより、運の良い勝利がリーダーボードに急上昇を引き起こし、緩やかに減少します。キーワードリストへの過剰依存は、ボットがしばらくはトップに留まることを可能にするかもしれませんが、プライベートキーワードが公開されると危険にさらされることになります。
> 
> 主催者は#5を変更し、エラーを発生させたボットをペナルティーを与え、他のプレイヤーには報酬を与えないようにすべきだと思います。このような設定は他のシミュレーションコンペには当てはまるかもしれませんが、このコンペには当てはまらないかもしれません。#4の部分でも何か調整があれば良いと思います。
> 
> プライベートリーダーボードでは、アクティブな変動が見られると思いますが、ただし、数人が顕著に優れたボットを生み出さない限り、何らかのランダム性を伴うかもしれません。
>
> > ## OminousDude
> > 
> > 私も同じように思いますし、これは大きな問題だと思います。コンペティションの主催者がこれを解決する方法を見つけることを心から願っています。
> >
> > このスコアの偏差を最小限に抑えるための1つの方法は、過去約50ラウンドで単独で勝利していないエージェントを排除することです。これにより、トップのボットを引き下げることなく、低いボットと高いボットが時々一緒に置かれるのを防ぐことができます。
> >
> > もう1つの方法は、ゲームを1回ではなく3回行って、それぞれのエージェントを互いにプレイさせることです。たとえば、最初のラウンドでボットaが勝った場合、次のラウンドではエージェント1がエージェント3、およびエージェント4と対戦し、すべてのエージェントが互いのモデルと対戦することになります。この2つ目のオプションは、1人の質問者エージェントが「悪い」回答者を得てしまう問題を解決するでしょう。もし誰もラウンドで勝たなかった場合、デフォルトのポイントが与えられます。もし2ラウンドが勝利した場合、一方のチームに含まれるエージェントはブーストを受け、他のラウンドで1回しか勝利しなかったエージェントには小さな（しかし依然として十分な）報酬が与えられます。
> >
> > 最後に、3つ目の解決策は、あるエージェントが常に敗北/勝ちがない場合、チームの他のエージェントが少しブーストを受け（+10程度）て、敗北したボットが少し減少する（-10程度）というものです。これにより、勝利と敗北が分かれる速度が速くなるため、実際に勝つことができるボットがより高いレベルのボットと対戦することになります。
> >
> > コンペティション主催者は、少なくともこれらのどれか1つ（できれば2番目と3番目のもの）を検討してくれることを願っています。このような小さな変更が、スコアリングの「宝くじ」方面を大きく変えるかもしれません。
> 
> > 
> > ## gguillardTopic Author
> > 
> > 幸いなことに、これらのオプションはすぐにノートブックでテストできるので、ホストは事実に基づいてどれが最適かを決定できます。
> > 
> > > ## OminousDude
> > > 
> > > ああ、そうですね！どの戦略をノートブックで実行して、最善のものを見つけるか提案します。
> > >
> > > > ## gguillardTopic Author
> > > > 私に関しては、しばらくの間、2回目の提出物を作成することに集中しようと思います。 :D
> > > > ただ、ホストが評価の修正にオープンであることを認めた場合、必要に応じて手伝うことは喜んで行います。
> > > > 
---
> ## loh-maa
> 
> 新しいプレイヤーにとって何が起こっているのか疑問を抱く理由が多いのは理解できます。750のスコアに達しようとするエージェントは、突然頻繁にプレイするのをやめて1日あたりゲームを1つか2つだけプレイするようになります。これは明らかにリーダーボードに影響し、最終段階では正常に戻ると確信しています。この変更が導入された理由は不明ですが、実際のパフォーマンスを隠すためなのか、特定の解決策があまりにもアクティブにならないようにするためなのかはわかりません。とにかく、心配する必要はなく、あなたのベストアイデアで参加してください！
> 
> 
---
> ## VolodymyrBilyachat
> 
> 回答者を混ぜ合わせることがこのコンペティションを改善すると思いませんか？1つの回答が完全に間違った方向に進んでしまっています :( それが100％の問題を解決するわけではありませんが、かなりの改善につながるでしょう。


</div>