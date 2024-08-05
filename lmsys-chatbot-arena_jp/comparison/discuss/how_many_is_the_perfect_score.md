# 要約 
このディスカッションは、Kaggleコンペティション「LMSYS - Chatbot Arena 人間による好み予測チャレンジ」における「完璧なスコア」について議論しています。

投稿者は、コンペティションで得られるスコアが0.5から1.7の範囲であることを知り、完璧なスコアがどのくらいなのか疑問に思っていました。

Valentin Wernerは、対数損失というメトリックでは、0.0のスコアが完璧な予測を表すことを説明しました。しかし、人間の好みは予測が難しいため、現実的な完璧なスコアは0.0よりもはるかに高く、0.75または0.8に近いだろうと推測しました。

その後、投稿者はリーダーボードでスコアが低いほどランキングが高いことに気づき、Yichuan Gaoは、スコアが対数損失として計算されるため、損失が低いほど予測が優れていることを説明しました。

このディスカッションは、コンペティションのメトリックと、人間の好みを予測する難しさについて理解を深めるのに役立ちます。


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

# how many is the perfect score?

**Anya** *Sat Jun 22 2024 17:17:35 GMT+0900 (日本標準時)* (0 votes)

Im new to kaggle.

Till now, Ive seen scores range in 0.5 to 1.7

I wonder how many is the perfect score so I can evaluate my score level.

Is it 5, 10 or 100?



---

 # Comments from other users

> ## Valentin Werner
> 
> The metric "log_loss" allows for a score of 0.0 (e.g., exactly perfect predictions every time). An "educated guess" score (predicting the distribution of the train set) gets you a score of about 1.097.
> 
> The problem is that human preferences, which we are trying to predict, are not clearly predictable. This is because if we both write a prompt, we may prefer different responses - so how is our model supposed to learn which responses are better. Because the problem is this hard to predict, the "ceiling" of the score is much higher than 0.0 - more along the lines of 0.75 or 0.8 (just a gut feeling)
> 
> 
> 
> > ## AnyaTopic Author
> > 
> > I got it😃. Thanks  for such a detailed reply.
> > 
> > 
> > 


---

> ## AnyaTopic Author
> 
> After reading the leaderboard I find that the lower one scores, the higher he ranks?
> 
> 
> 
> > ## Yichuan Gao
> > 
> > Yes it is, since the score is calculated as log loss, the lower the loss, the better your guesses are
> > 
> > 
> > 


---



</div>
<div class="column-right">

# 日本語訳

# 完璧なスコアはいくつ？
**Anya** *2024年6月22日(土) 17:17:35 JST* (0 votes)
Kaggle初心者です。
今まで、スコアは0.5から1.7の範囲で見てきました。
自分のスコアのレベルを評価するために、完璧なスコアがいくつなのか知りたいです。
5、10、それとも100でしょうか？
---
# 他のユーザーからのコメント
> ## Valentin Werner
> 
> メトリック「log_loss」は、0.0のスコアを可能にします（例：毎回完全に正確な予測）。「推測に基づいた予測」（トレーニングセットの分布を予測する）では、約1.097のスコアになります。
> 
> 問題は、私たちが予測しようとしている人間の好みは、明確に予測可能ではないということです。これは、私たちが両方ともプロンプトを書いた場合、異なる応答を好む可能性があるため、モデルはどの応答がより良いかをどのように学習すればいいのかということです。問題がこのように予測しにくいことから、スコアの「上限」は0.0よりもはるかに高く、0.75または0.8に近いでしょう（単なる直感です）。
> 
> 
> 
> > ## AnyaTopic Author
> > 
> > わかりました😃。とても詳細な回答をありがとうございます。
> > 
> > 
> > 
---
> ## AnyaTopic Author
> 
> リーダーボードを見ると、スコアが低いほどランキングが高いように思えます。
> 
> 
> 
> > ## Yichuan Gao
> > 
> > はい、そうです。スコアは対数損失として計算されるため、損失が低いほど、あなたの推測はより良いものになります。
> > 
> > 
> > 
---



</div>