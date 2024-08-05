# 要約 
ディスカッションでは、ユーザー「fauxsmart」が、リーダーボードが動き始めた理由として「フランス」というキーワードを使ったラッキーなゲームを挙げています。このゲームが唯一の非引き分けのゲームであることから、その影響でボットのパフォーマンスに変化があったと考えられます。また、このキーワードが「few_shot_examples」に使用されていることも関係しているようです。

他のユーザー、「Khoi Nguyen」が、エージェントの質問と回答が全て公開されていることが戦略に影響を与えないか懸念を示しています。これに対し、「fauxsmart」は、ゲームの複雑さから完全に同じ戦略を取るのは難しいとし、相手がどのように答えに至ったかを知ることが難しいため、大きなプールからのキーワードの選択肢も影響するだろうと述べています。さらに、リーダーボードのスコアに関連する操作についてのアドバイスも提示されています。

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

# [Offtopic] What got the LB moving

**fauxsmart** *Sat May 18 2024 20:45:39 GMT+0900 (日本標準時)* (0 votes)

If anyone is interested, I think the LB got moving from all 600.0 because of this lucky game where the keyword was "france". 😀 It is the only non-tied game I have seen this far.

[https://www.kaggle.com/competitions/llm-20-questions/leaderboard?dialog=episodes-episode-54792273](https://www.kaggle.com/competitions/llm-20-questions/leaderboard?dialog=episodes-episode-54792273)

Lucky, because the example notebook uses "france" in its few_shot_examples, which I guess primed the bot.



---

 # Comments from other users

> ## Khoi Nguyen
> 
> Wait so all of our agent's questions and answers are public? Does that spoil the whole strategy?
> 
> 
> 
> > ## fauxsmartTopic Author
> > 
> > We can, yes, but I don't see how that matters much -- the game seems too complex to actually "game". 
> > 
> > They wouldn't still know how you came to your answers + the keywords will (hopefully) come from a large pool, so creating a lookup table or something like that would be quite costly; you couldn't do it offline unless people submit totally barebones LLM solutions (you would also have to do that for each of many opponents). 
> > 
> > Also, from what I have seen this far, one might want to query an LLM many times per game turn to fix bad answers etc. (gemma-7b for example does not seem to play the game well out-of-the-box). All of those internal "moves" would still be hidden.
> > 
> > 
> > 
> > > ## Nicholas Broad
> > > 
> > > [@suicaokhoailang](https://www.kaggle.com/suicaokhoailang) ,
> > > 
> > > Go to the leaderboard and click the play button next to the scores
> > > 
> > > 
> > > 


---



</div>
<div class="column-right">

# 日本語訳

# [オフトピック] リーダーボードが動き始めた理由
**fauxsmart** *2024年5月18日 20:45:39 JST* (0票)
興味がある人のために言っておくと、リーダーボードが動き出したのは、キーワードが「フランス」であるラッキーなゲームのおかげだと思います。😀 これまで見てきた中で唯一の非引き分けのゲームです。
[リーダーボードのリンク](https://www.kaggle.com/competitions/llm-20-questions/leaderboard?dialog=episodes-episode-54792273)
ラッキーなことに、例のノートブックで「フランス」がfew_shot_examplesで使われているので、それがボットに影響を与えたのだと思います。

---
# 他のユーザーからのコメント
> ## Khoi Nguyen
> 
> 待って、私たちのエージェントの質問と回答は全部公開されているの？それって戦略全体を台無しにしない？
> 
> > ## fauxsmart（トピック作成者）
> > 
> > 確かに公開されていますが、それがどれほど重要かはわかりません。ゲームは実際に「ゲーム」するには複雑すぎるように見えます。
> > 
> > 相手があなたの答えに至った方法はわからないでしょうし、キーワードは（願わくば）大きなプールから来るので、ルックアップテーブルなどを作成するのはかなり手間がかかります。完全にオフラインでは行えませんし、人々が全く機能しないLLMソリューションを提出する場合を除いては、各対戦相手ごとにそれを行う必要があります。
> > 
> > また、これまでの経験から、ゲームのターンごとに悪い回答を修正するためにLLMに何度もクエリを送信したくなるかもしれません（例えば、gemma-7bはデフォルトではゲームをうまくプレイできないようです）。これらの内部的な「動き」はまだ隠されているでしょう。
> > 
> > > ## Nicholas Broad
> > > > [@suicaokhoailang](https://www.kaggle.com/suicaokhoailang) ,
> > > >
> > > > リーダーボードに行って、スコアの隣にある再生ボタンをクリックしてみてください。


</div>