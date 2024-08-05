# 要約 
ディスカッションでは、現在のリーダーボードの状態とその影響について話し合われています。ユーザーのOminousDudeは、リーダーボードが古い優れたモデルによって混雑しているため、スコアの比較が難しく、スコアを600に戻すことができるか尋ねています。彼の意見に対して、他のユーザーはリセットしても状況が改善されないとし、「愚かさの穴」に直面する問題を指摘しています。この穴は、スコア600以下でパートナーと組むことで生じる難しさを表現しており、参加者はより賢いボットを競技に持ち込む必要があるかもしれないと考えています。

コンペティション主催者のBovardは、リーダーボードの改善策として、エージェントがランダムに他のボットとマッチングされる「ランダム」エピソードを追加することを予定していると述べています。この変更は、エージェントが高評価の相手と対戦する機会を増やし、デッドロックを打破するためのものです。ユーザーたちはこの変更を歓迎しており、以前のエージェント間のスコアの差が縮まっていることを報告しています。全体として、コミュニティはリーダーボードの公平性を求めつつ、主催者の対応を支持しています。

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

# Can we reset the entire leaderboard?

**OminousDude** *Tue Jun 25 2024 11:24:45 GMT+0900 (日本標準時)* (2 votes)

Currently, the leaderboard is clogged up by old (and great) location-only models that will slowly move down. However, this will also affect other models that have adjusted to the changes. As of right now, it is much harder to compare scores because of all of the half-keyword models. Is it possible to return scores to 600 or is this not possible to achieve for the competition hosts? [@bovard](https://www.kaggle.com/bovard) 



---

 # Comments from other users

> ## loh-maa
> 
> The current LB is not very meaningful, but in my opinion resetting would not make it better, or fix anything.
> 
> I believe our hosts are watching closely and will adjust the ranking algorithm to ensure convergence in the final stage, which doesn't seem to be very robust at the moment. One particular issue appears to be a "pit of dumbness" down there around 600 and below (no offense to any cute agents always saying "yes"), and it's difficult to get out of there even if your agent is relatively smart (e.g. it can play reasonably against itself.)
> 
> Let's understand the reluctance of the hosts to react, regarding any issue. Any intervention or unexpected change works against reliability and trust, and is potentially disrespectful to someone's effort already made, so the justification must be rock solid.
> 
> 
> 
> > ## RS Turley
> > 
> > I agree with you: the "pit of dumbness" is a big challenge. It is relatively difficult to win games when you are paired with a partner in the 600-range. The solution to that may fall on us, as a community of competitors, to get more intelligent bots in the competition!
> > 
> > That said, I really appreciate that a new submission gets a dozen or more matches during their first day, so there is a reasonable chance to escape that pit of dumbness with just one win.
> > 
> > 
> > 
> > > ## OminousDudeTopic Author
> > > 
> > > I have been stuck in this "pit" for my last 7 submissions. I doubt my model is the problem since it works very well against itself in validation but I hate the only yes/no bots.
> > > 
> > > 
> > > 


---

> ## Bovard Doerschuk-Tiberi
> 
> Thanks for bringing this up! To address this we are adding some "random" episodes where agents will be matched with anyone from the leaderboard. Initially this should be about 10% of the total games, and we will adjust as needed. This should allow agents an opportunity to play with higher rated opponents enough to break the deadlock.
> 
> EDIT: looks like there is a bug with this functionality. It is currently disabled until we can get that fixed.
> 
> 
> 
> > ## DJ Sterling
> > 
> > This change should be rolled out now.
> > 
> > 
> > 
> > ## Melinda
> > 
> > Nice! Previously my three very similar agents had vastly different scores (different by 200 points), but over the last few days they have converged to nearly the same score, so this change seems to be making a difference!
> > 
> > 
> > 


---

> ## Matthew S Farmer
> 
> I second this request. 
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# リーダーボードをリセットすることは可能ですか？
**OminousDude** *2024年6月25日 火曜日 11:24:45 JST* (2票)
現在、リーダーボードは古い（そして優れた）ロケーションモデルで混雑していますが、それらは徐々に下がっていくでしょう。しかし、これは変化に適応した他のモデルにも影響を与えます。現時点では、ハーフキーワードモデルが多く存在するため、スコアの比較が非常に難しくなっています。スコアを600に戻すことは可能でしょうか？それとも、コンペティションの主催者にとっては実現不可能なことなのでしょうか？ [@bovard](https://www.kaggle.com/bovard) 
---
# 他のユーザーからのコメント
> ## loh-maa
>
> 現在のリーダーボードはあまり意味がありませんが、リセットしても良くなるとは思いませんし、何も解決しないと思います。
> 
> 主催者が注意深く見守っており、最終段階でランキングアルゴリズムを調整することが期待されますが、現時点ではあまり堅牢だとは思えません。特に、600ポイント以下には「愚かさの穴」があるようです（「はい」と言い続ける可愛いエージェントには失礼ですが）。たとえあなたのエージェントが比較的賢くても（たとえば、自身に対してそれなりにプレイできる場合でも）、そこから抜け出すのは難しいです。
>
> 何か問題があった場合、主催者が反応しづらい理由を理解しましょう。介入や予期しない変更は、信頼性と信頼に逆らい、すでに誰かが努力したことに対して不敬に働く可能性があるため、正当化は非常に重要です。
>
> > ## RS Turley
> >
> > あなたに賛成です：「愚かさの穴」は大きな課題です。600レンジのパートナーとペアになると、ゲームに勝つのは難しいです。この解決策は、競技者のコミュニティでより賢いボットをコンペティションに持ち込むことにかかっているかもしれません！
> >
> > それはさておき、新しい提出物が初日だけで10試合以上をこなすことは本当にありがたいので、たった1勝でその愚かさの穴から脱出する合理的なチャンスがあると思います。
> >
> > > ## OminousDude トピック作成者
> > > > 私は過去7回の提出でこの「穴」にハマっています。私のモデルに問題があるとは思いません。なぜなら、バリデーションでは非常にうまく機能するからです。しかし、唯一の「はい/いいえ」ボットには本当に困っています。
> >
> > > 
---
> ## Bovard Doerschuk-Tiberi
>
> この問題を取り上げてくれてありがとう！これに対処するために、エージェントがリーダーボード上の誰とでもマッチングされる「ランダム」エピソードを追加する予定です。最初は合計ゲームの約10％を想定しており、必要に応じて調整します。これにより、エージェントがより高評価の相手とプレイし、デッドロックを破る機会が増えるはずです。
>
> 編集：この機能にバグがあるようです。修正が完了するまで現在は無効化されています。
>
> > ## DJ Sterling
> >
> > この変更は今すぐに実施されるべきです。
> >
> > 
> > ## Melinda
> >
> > いいですね！以前、私の3つの非常に似たエージェントは200ポイントも異なるスコアを持っていましたが、ここ数日でほぼ同じスコアに収束しているので、この変更は効果を発揮しているようです！
> >
> > 
---
> ## Matthew S Farmer
>
> このリクエストに賛成します。 
> 
>


</div>