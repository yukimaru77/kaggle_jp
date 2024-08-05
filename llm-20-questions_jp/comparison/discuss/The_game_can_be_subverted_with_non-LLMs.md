# 要約 
このディスカッションでは、言語モデル（LLM）を使用せずに行う「20の質問」ゲームに関する仮説が討論されています。特に、正規表現や二分探索を用いた非LLMのアプローチがLLMを上回る可能性について意見が交わされています。トピックの作成者、loh-maaは、現在のゲーム形式では最適な戦略を適用するための共通プロトコルが欠如しているため、非LLMのアプローチが優位に立つ可能性があると述べています。

彼は非LLMのエージェントがリーダーボードを占め始めており、もしこのアプローチが広く採用されると、LLMよりも高い位置に維持されるだろうと警告しています。また、秘匿された共謀の可能性を排除するために、共通のオープンプロトコルを採用することが重要であると提案しています。

他の参加者も同様の考えを示し、特定のキーワードリストに基づく解決策がLLMに劣らないと考えている中で、その利便性や効果的な応用について意見を交わしています。全体として、ディスカッションはコンペティションの目的やルールの見直しの必要性に関するものとなっています。

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

# The game can be subverted with non-LLMs

**loh-maa** *Mon Jun 10 2024 18:59:06 GMT+0900 (日本標準時)* (11 votes)

It's just a hypothesis for now, but I believe a near-optimal solution to the game doesn't involve LLMs. It's possible to ask questions using plain regular expressions, and if the answering agent is able to understand, the answer will always be perfect -- a huge advantage over LLMs. Also bisecting the space is much more efficient with REs than with natural language.

The only thing missing is.. adoption. Once there is a critical mass, REs should be able to take over the top, or at least be necessary to stay on top.

Very interesting dynamics regarding who's gonna talk which language.. and of course the critical question -- are we going to see any new regulation regarding this?



---

 # Comments from other users

> ## loh-maaTopic Author
> 
> Update
> 
> Let me share some thoughts on the situation, please.
> 
> In the current phase, when the list of keywords is known, optimal game plays exist, and they're not based on LLMs. The only factor holding them back from domination is lack of adoption or a common protocol to apply them during the games. They can be based on many techniques, I thought of regular expressions first but soon I realized a simple alphabetical bisection is just perfect. I published a [notebook here.](https://www.kaggle.com/code/lohmaa/llm20-agent-alpha)
> 
> In the evaluation phase, when the list of keywords is unknown, the performance of those previously optimal solutions would depend on the assumed list of keywords, but even with rough assumptions I think it's going to be superior to LLMs. Perhaps we may call such solutions near-optimal. Here I must wave to our dear hosts [@bovard](https://www.kaggle.com/bovard) [@addisonhoward](https://www.kaggle.com/addisonhoward) -- I'm afraid changing the list of keywords will not suddenly favor LLMs,  and thus it won't solve this issue.
> 
> Suppose all players play the "LLM" game by default, but there is a group of people that (secretly or openly) agreed to apply the optimal strategy whenever they are paired in a team. Surely such a group would come on top of the LB, given everything else being equal. And surely nobody would like to be outplayed by a group of friends who secretly adopted an optimal protocol. If it was done openly and not last minute, then perhaps it would be fair, but let's not hope for the best, we must assume collusion attempts will be made. So what can be done?
> 
> With the current format of the game, one thing that decent players can do is to adopt a common protocol to apply the optimal play (spontaneously.) This would effectively eliminate any advantage of secret collusion (aka rigging?) However this would also shift the competition from LLMs to a very simple conventional solution, which is fine to me and good for the planet, but this would miss the goal of the competition.
> 
> Perhaps there is one path to keep the LLMs in play, though, if only the agents would have to play with a wide spectrum of players in the ranking, and provided some players (or perhaps "neutral" agents?) would play LLM only -- this would force everybody to be at least able to play LLMs as well. (Then however, is another question whether the ELO/ranking can work in such a mode… BTW if it was published we could do simulations.)
> 
> Another option would be to change the format and instead of teaming players force the play against a neutral/reference LLM which would not adhere to any particular protocols except natural language. This in turn would make the competition all about trying to figure out the reference LLM -- what it can understand and why not.
> 
> I don't think the above remedies are great, but still sound better to me than falling to collusion. I am very interested in your opinion.
> 
> 
> 
> > ## tr
> > 
> > I agree with you. My conclusion was that the list of viable keywords has to be fairly limited (<50K) anyway, so not really unknown, so solvable with "classical" approaches, at least for questioner/guesser. For the answerer I'm still not sure since it is more dependent on "protocol" of other agent, but looks viable.
> > 
> > EDIT: maybe the list of viable keywords is bigger than my estimate, wikipedia has almost 7M articles.  
> > 
> > 
> > 
> > > ## loh-maaTopic Author
> > > 
> > > Thanks for sharing your perspective, well, if I understand correctly, non-LLM approaches are not more restricted than LLMs.. how many keywords an LLM of size 7b can handle, practically? Maybe 1 or 2k? So far it's not looking very effective even for 560.
> > > 
> > > 
> > > 
> > > ## tr
> > > 
> > > Sorry for confusing posts, maybe I'm just rambling, but I'll try to elaborate :) 
> > > 
> > > Yes, I think classical approach is valid at least as LLM approach, but only for questioner/guesser. 
> > > 
> > > Classical would need a list of keywords to perform some kind of bisection with hard-coded questions and guesses from the list. I believe such list can be made, since I estimate <50K viable places, persons or things. Such agent would be optimal, depending on accuracy of answerer and completeness of the list (like in your notebook).
> > > 
> > > LLM questioner/guesser doesn't strictly need such list, but I expect it to be inferior to classical approach above. Thus defeating part of the goal of competition. 
> > > 
> > > For LLM "word capacity", in theory I'd estimate much higher. I mean, you can ask it pretty much about any entity and it will give you a reasonable reply. No?
> > > 
> > > 
> > > 
> > > ## loh-maaTopic Author
> > > 
> > > Yes, well, non-LLM works only when paired with another compatible non-LLM, and then they make one solution.
> > > 
> > > Yes, the "word capacity" is probably much higher than my estimate, but then what is the power of questions and reliability of answers as the search descends into more details? Even a small error rate in answering can affect the search, 20% error rate usually ends in a bush.. certainly improving this, is the primary objective behind this competition, and optimistically, as long as non-LLMs need LLMs for a backup it may prevail.
> > > 
> > > 
> > > 


---

> ## Kha Vo
> 
> [@bovard](https://www.kaggle.com/bovard) [@addisonhoward](https://www.kaggle.com/addisonhoward) 
> 
> As shown by this topic's author, his agent is now starting to dominate the leaderboard. More teams are submitting this agent which is a binary search based solely on the keyword list. Both questioner and answerer of this agent are non-LLM, just rule-based. So as long as many more teams submit this agent, they will all occupy top of LB very soon.
> 
> You can see one episode example here: [https://www.kaggle.com/competitions/llm-20-questions/submissions?dialog=episodes-episode-55060055](https://www.kaggle.com/competitions/llm-20-questions/submissions?dialog=episodes-episode-55060055)
> 
> I guess all these below changes may have to be made at the same time to make the competition better:
> 
> - List of keywords must be changed
> 
> - List of keywords must not be accessible by any agents by any means, even from this early stage
> 
> - Replays must not display the keyword publicly. Replays may not also display guesses.
> 
> - Keywords must not be obtained via aggregating past gameplays
> 
> 
> 
> > ## loh-maaTopic Author
> > 
> > Hello Kha Vo, I share your concern about the situation, it's not going in the right direction, however I think the remedy you just proposed is not a real solution. Non-LLM optimal solution would become conditionally optimal (if that's the right term) but I bet it would stay in play even after those changes. Perhaps they would make adoption slower, but they would also make the current testing stage unclear and less fun.
> > 
> > As I stated in the update, I think that common adoption of a near-optimal solution based on an open protocol is perhaps the only effective protection against collusion in the evaluation phase, given the current game format. If you can think of any other way to neutralize the advantage of potential collusion (again, given the current game format), then please show me wrong.
> > 
> > 
> > 
> > ## Max Brown
> > 
> > I don't see how your proposed changes would work. The bisecters can just create their own set of keywords (up to hundreds of thousands of words) and distribute this common set amongst themselves.
> > 
> > 
> > 


---

> ## Krens
> 
> Using non-LLM methods such as binary search is indeed a different and even brilliant solution. The difficulty of this method should be how to build a list that "completely" covers all possible keywords. Theoretically, we can search for millions of keywords in one round of competition, but when the search fails, we can also consider adding LLM to remedy it. (Although the effect should not be too good)
> 
> 
> 


---

> ## Max Brown
> 
> I'm only just looking at this competition now. A binary search based solution was the first thing that occurred to me as well. Is there any indication that the kaggle team is going to address this?
> 
> I'm struggling to think of how to fix this. 
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# ゲームは非LLMで覆される可能性がある
**loh-maa** *2024年6月10日 18:59:06 GMT+0900 (日本標準時)* (11票)
これは今のところ仮説ですが、ゲームに対するほぼ最適な解法がLLMを使用しないものであると考えています。通常の正規表現を使って質問をすることが可能で、もし答えるエージェントがそれを理解できれば、回答は常に完璧であり、LLMに対して大きなアドバンテージとなります。また、空間を二分するのは自然言語よりも正規表現の方が効率的です。唯一欠けているのは…採用です。クリティカルマスが形成されれば、正規表現はリーダーボードのトップを占めるか、少なくとも上位に位置し続ける必要があります。誰がどの言語を話すのかという非常に興味深い動きがありますね… そしてもちろん、重要な疑問は、これに関して新たな規制が見られるのかということです。
---
 # 他のユーザーからのコメント
> ## loh-maaトピック作成者
> 
> 更新
> 
> 現状についていくつか考えを共有させてください。
> 
> 現在の段階ではキーワードのリストが知られているため、最適なゲームプレイは存在しますが、それはLLMに基づくものではありません。それらが支配するのを妨げている唯一の要素は、採用の欠如またはゲーム中に適用するための共通のプロトコルの欠如です。それらは多くの技術に基づけますが、まず正規表現を考え、その後単純なアルファベット二分法が完璧であることに気づきました。私は[こちらでノートブックを公開しました。](https://www.kaggle.com/code/lohmaa/llm20-agent-alpha)
> 
> 評価段階で、キーワードのリストが未知の場合、その時点での以前の最適解のパフォーマンスは仮定されたキーワードのリストに依存しますが、大まかな仮定でもLLMに対して優位になると思います。おそらくこのような解法は「ほぼ最適」と呼べるでしょう。ここで、私たちの親しいホスト[@bovard](https://www.kaggle.com/bovard) [@addisonhoward](https://www.kaggle.com/addisonhoward)に挨拶を送りますが、キーワードリストを変更しても、LLMを突然有利にすることはなく、この問題を解決することにもならないでしょう。
> 
> もしすべてのプレイヤーがデフォルトで「LLM」ゲームをプレイし続けるとして、あるグループが（秘密裏にまたは公然と）最適な戦略を適用することに合意した場合、そのグループは他のすべてが平等であればリーダーボードの上位に位置することが確実です。そして、誰も秘密裏に最適なプロトコルを採用した友人たちに対して負けたくはありません。もしそれがオープンに行われ、最後の瞬間ではないとすれば、公正と言えるかもしれませんが、最善を期待せず、共謀の試みがなされると仮定しなければなりません。では、どのようにすればよいでしょうか？
> 
> 現在のゲーム形式では、まともなプレイヤーができる一つのことは、最適なプレイを適用するための共通のプロトコルを自発的に採用することです。これにより、秘密裏の共謀（いわゆるごまかし）のアドバンテージを実質的に排除することが可能になります。しかし、これによりLLMから非常にシンプルな従来の解決策へと競争がシフトすることにもなり、私にとっては問題ないことですが、コンペティションの目的からは外れてしまうことになります。
> 
> ただし、LLMを継続させるための一つの道があるとすれば、エージェントがランキングの広範囲なプレイヤーと対戦し、いくつかのプレイヤー（あるいは「中立的」エージェント）によってLLMのみでプレイされることが求められることです。これにより、全てのプレイヤーが少なくともLLMをプレイできるようになるでしょう。しかし、そうなると、ELO/ランキングがそのようなモードで機能するかどうかという別の問題があります… もしそれが公表されたら、シミュレーションを行うことも可能です。
> 
> もう一つの選択肢は形式を変更し、プレイヤーをチームにする代わりに中立的/参照のLLMに対戦させることです。これは特定のプロトコルに従わず自然言語のみを受け入れるLLMです。こうすることで、競争は参照LLMが何を理解し、なぜ理解しないのかを解明することに100%焦点を合わせることになるでしょう。
> 
> 上記の解決策は素晴らしいとは思いませんが、共謀への堕落を防ぐよりはましだと考えます。皆さんの意見を非常に楽しみにしています。
> 
> > ## tr
> > 
> > あなたに同意します。私の結論は、実行可能なキーワードのリストはかなり限られている必要があり（<50K）、したがって実際には不明ではないため、従来のアプローチで解決可能だということです。実際、回答者は他のエージェントの「プロトコル」に依存するため、まだ不明確ですが、実行可能であるように思えます。
> > 
> > 編集: 実行可能なキーワードのリストは私の推定よりも大きいかもしれません。ウィキペディアにはほぼ700万の記事があります。
> > 
> > > ## loh-maaトピック作成者
> > > 
> > > あなたの視点を共有してくれてありがとう。あなたの言う通り、非LLMのアプローチはLLMよりも制限されていないようです… 大きさ7bのLLMが実際に扱えるキーワード数はどうでしょうか？ おそらく1,000または2,000程度でしょうか？ 560にもかかわらず、今まであまり効果的ではありません。
> > > 
> > > > ## tr
> > > > > ごめんなさい、混乱させてしまったかもしれませんが、少し詳しく説明しますね :) 
> > > > 
> > > > はい、従来のアプローチは少なくともLLMアプローチと同等だと思いますが、質問者/推測者に対してのみです。 
> > > > 
> > > > 従来の方法は、ハードコーディングされた質問とリストからの推測を使用して二分法を行うためにはキーワードのリストが必要です。こうしたリストは作成できると考えています。なぜなら、行き先や人々、物事の実行可能な場所が<50Kと推定されるからです。そのようなエージェントは、回答者の正確さとリストの完全性（あなたのノートブックにおけるように）に依存して最適になります。
> > > > 
> > > > LLMの質問者/推測者はそのようなリストを厳密には必要としませんが、上記の従来のアプローチに比べて劣っていると予想しています。したがって、コンペティションの部分的な目標を達成し損なうことになります。 
> > > > 
> > > > LLMの「単語容量」については、理論的にははるかに高いと推定されます。つまり、ほとんどあらゆる実体について尋ねることができ、適切な返答が得られるのではないでしょうか？ 
> > > > 
> > > > > ## loh-maaトピック作成者
> > > > > > はい、非LLMは互換性のある他の非LLMと組み合わせて使用される場合にのみ機能し、彼らは一つの解を作ります。
> > > > > > 
> > > > > > はい、「単語容量」は私の推定よりもおそらくはるかに高いですが、では質問の力と詳細に降下するにつれての回答の信頼性はどうでしょうか？ 回答のエラー率が少しでもあれば、探索に影響を与える可能性があります。20%のエラー率は通常、茂みに終わります… 確かに、これを改善することがこの競技会の主な目的であり、楽観的に言えば、非LLMがバックアップとしてLLMを必要とする限り、勝利する可能性があるかもしれません。
> > > > 
---
> ## Kha Vo
> 
> [@bovard](https://www.kaggle.com/bovard) [@addisonhoward](https://www.kaggle.com/addisonhoward) 
> 
> このトピックの作者が示すように、彼のエージェントは今やリーダーボードを占め始めています。このエージェントはキーワードリストに基づいた二分探索に基づいています。質問者と回答者の両方が非LLM、ただしルールベースであるため、より多くのチームがこのエージェントを提出すれば、すぐに彼らはリーダーボードのトップを占めることになるでしょう。
> 
> 特定のエピソードの例はこちらで見ることができます: [https://www.kaggle.com/competitions/llm-20-questions/submissions?dialog=episodes-episode-55060055](https://www.kaggle.com/competitions/llm-20-questions/submissions?dialog=episodes-episode-55060055)
> 
> おそらく、以下の変更が同時に行われないと、競技会が改善されないかもしれません:
> 
> - キーワードリストを変更する必要があります
> 
> - キーワードリストは、いかなるエージェントによってもアクセスできないようにすべきです、この早い段階からでも
> 
> - リプレイはキーワードを公開表示しない必要があります。また、リプレイは推測も表示しない必要があります。
> 
> - 過去のゲームプレイを集約することで、キーワードを取得できるべきではありません。
> 
> > ## loh-maaトピック作成者
> > 
> > こんにちはKha Vo、状況についてあなたの懸念を共有します。正しい方向に進んでいませんが、あなたが提案した対策は本質的な解決にはならないと思います。非LLMの最適解は状況に応じて最適になるでしょうが、その変化があってもそのデータプレイは継続すると思います。変更は採用を遅くするかもしれませんが、現在のテスト段階を不明瞭で楽しくないものにすることにもつながります。
> > 
> > 更新で述べたように、評価段階における秘密の共謀に対する効果的な保護は、オープンプロトコルに基づいたほぼ最適な解法の共通採用だと思います。もし他に共謀の潜在的な ventaja を無効化する方法が考えられるのなら、現行のゲーム形式の下で示してみてください。
> > 
> > > ## Max Brown
> > > 
> > > あなたの提案した変更がどのように機能するのか分かりません。バイセクターは単に自分たちのキーワードリスト（数十万語に達することも可能）を作成し、それを互いに配布することができるでしょう。
> > > 
> > > 
> > 
---
> ## Krens
> 
> 非LLMの方法、例えばバイナリサーチを使用するのは、確かに異なる、さらには素晴らしい解決策です。この方法の難しさは、すべての可能なキーワードを「完全に」カバーするリストを作成することにあるべきです。理論的には、一回の競技で何百万ものキーワードを検索できますが、検索が失敗した場合にLLMを追加してその補助とすることも考えられます（ただし、その効果はあまり良くないはずですが）。
> 
> ---
> ## Max Brown
> 
> 私はこの競争を今見始めたところです。バイナリサーチに基づく解決策は私も最初に思いついたものです。Kaggleチームがこれに対処する意向があるのか、何か示されていますか？
> 
> どうやってこの問題を解決するか思いつかなくて困っています。
> 
> ---


</div>