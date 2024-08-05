# 要約 
コンペティションのディスカッションでは、上位9のリーダーボード（LB）のエージェントが、チームメイトのエラーによりポイントを獲得していることが問題視されています。クリス・デオッテ氏は、エラーにより不公平なポイント分配が生じていると指摘し、エラーを起こしたエージェントはポイントを失い、他のエージェントがゼロポイントで再ゲームを開始すべきだと主張しています。

その後の更新では、同様の問題が繰り返し発生しており、特に新しい1位のエージェントもチームメイトのエラーからポイントを得ていることが明らかにされています。この状況について、コンペの主催者であるボバード・ドーチュク-ティベリ氏は、エラーを起こしたエージェントが-21ポイントになり、他の3つのエージェントはそれぞれ平均+7ポイントを得るシステムを実装する考えを示しています。

また、アンドレス・H・ザプケ氏の質問では、回答者がどのように機能するか、そしてなぜチームメイトにのみ応じるのかが議論されています。ディスカッションでは、エラーによる不公平の解決策や、ゲームのルールに関する理解を深めるための意見交換が行われており、参加者は問題の早急な修正を求めています。

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

# [FIXED] - The Top 9 LB is the result Errors

**Chris Deotte** *Wed May 29 2024 23:00:06 GMT+0900 (日本標準時)* (19 votes)

On May 29 at 14:00 UTC, I noticed the top 9 agents on the LB were all the result of gaining points from their teammate throwing an error. (The top 9 teams at 14:00 UTC were: Dapeng, Agney, Neel, Mitul, Neige, Agney, Gol-eel, tr, Mesmerized).

For each of the top 9 agents on LB, I reviewed their most recent game where they achieved positive points. I display these below. In each case, they received points because their teammate errored.

Is this the intended scoring mechanism? [@develra](https://www.kaggle.com/develra) [@addisonhoward](https://www.kaggle.com/addisonhoward) Should luck be the reason teams climb the LB?

IMO, when an agent throws an error, I suggest that the defective bot loses points and all 3 other bots ignore the game. (i.e. the other 3 bots get zero points and they immediately get a new game to replace the erroneous game). 

Guessing the keyword is difficult and there shouldn't be an easy way to gain lots of free points. (And on private LB, guessing will be even more difficult without a list of keywords).

## 1st Place

## 2nd Place

## 3rd Place

## 4th Place

## 5th Place

## 6th Place

## 7th Place

## 8th Place

## 9th Place



---

 # Comments from other users

> ## Chris DeotteTopic Author
> 
> UPDATE. I notice the same thing happening on May 30th at 14:00 UTC. The new first place jumped up to LB 660 because their teammate had an error. This destabilizes the leaderboard because now the original top LB bots will play with and against these bots whose true score is under 600. 
> 
> ## New 1st Place
> 
> ## New 5th Place
> 
> and the new 5th jumped there because their teammate had an error:
> 
> 
> 
> > ## OminousDude
> > 
> > The creators of this competition really need to fix this quickly.😑
> > 
> > 
> > 
> > > ## OminousDude
> > > 
> > > I am looking through the top 25 LB and out of the top 25 11 of them are boosted by errors.
> > > 
> > > 
> > > 


---

> ## OminousDude
> 
> Hi, the first place error bot is mine I have no idea why it is erroring I am fi I am finding out now thank you for alerting me to this. I had no intention of "illegally" giving top places points.
> 
> 
> 
> > ## OminousDude
> > 
> > My bot is also 3rd 😭. I have decided to submit three of my older bots to overwrite the offending error bots. This is my temporary solution since I do not want to be contributing to an unfair leaderboard.
> > 
> > 
> > 
> > ## Chris DeotteTopic Author
> > 
> > Hi OminousDude. There is no need to apoligize. Everybody's bots will make errors from time to time as we develop solutions. Earlier versions of my bots had errors and each day I remove errors and improve my bots. So don't worry about submitting bots with errors. Continue to try new things and submit whatever you want.
> > 
> > I think the competition metric should be updated so that bot errors do not help other bots.
> > 
> > 
> > 
> > > ## OminousDude
> > > 
> > > Yes, that would be the optimal solution but again the temporary solution is for me to remove the bots until their errors are fixed. Thank you for informing me on the issues of my bots. Because it was very weird that my agent improves almost all the time more or less +10 each time it goes up against another bot; however, its score is still always low.
> > > 
> > > 
> > > 


---

> ## Bovard Doerschuk-Tiberi
> 
> Taking a look at this now, thanks for reporting.
> 
> 
> 
> > ## Bovard Doerschuk-Tiberi
> > 
> > A fix for this should be rolling out tomorrow. The reward when an agent fails after this should be net zero. For example the failing agent might get -21 and the other three get an average of +7 each.
> > 
> > Penalizing the failing agent is important to keep the leaderboards clear and not allow a "error on purpose" strategy to exist. (eg if an agent hasn't guessed after X rounds and knows the average game at their level is X + 1, they could error on purpose if there was no penalty for doing so). 
> > 
> > 
> > 
> > > ## Bovard Doerschuk-Tiberi
> > > 
> > > This is rolled out now
> > > 
> > > 
> > > 


---

> ## Giba
> 
> I support what Chris says. I observed the same behaviour in LB, agent errors distribute free points to other agents.
> 
> 
> 


---

> ## Chris DeotteTopic Author
> 
> [@bovard](https://www.kaggle.com/bovard) I noticed that Mohammad just received 130 points (on June 4th) when his teammate (me Chris) errored. Other teams on the LB need to successfully win 5+ games to get 130 points (which requires the difficult accomplishment of guessing 5+ words correctly versus the lucky result of teammate error). 
> 
> FYI, Kaggle said they fixed awarding points for teammates of error teams but this doesn't look fixed:
> 
> 
> 
> > ## Bovard Doerschuk-Tiberi
> > 
> > Yeah I saw that as well. Looks like there was a bug if the agent errors on the last round of the competition. This has been fixed in [https://github.com/Kaggle/kaggle-environments/pull/275](https://github.com/Kaggle/kaggle-environments/pull/275)
> > 
> > 
> > 


---

> ## Andres H. Zapke
> 
> Hello!
> 
> One question, where does the answerer even come from? Is this supposed to be a separate LLM that has to be trained independently? 
> 
> And did I get it right, that because the answerer is not answering correctly, the "correct" guesses aren't being graded accordingly?
> 
> 
> 
> > ## Chris DeotteTopic Author
> > 
> > Each match has 4 Kaggle teams which are Questioner + Answerer versus Questioner + Answerer. So it is 2 vs. 2.
> > 
> > Each Answerer knows the correct answer and responds to their teammate the Questioner.
> > 
> > 
> > 
> > > ## Andres H. Zapke
> > > 
> > > Yes, but the Answerer cannot be a hard-coded bot, since it has to interpret the question correctly. I thought he is responsible for grading our "Questioner LLMs", so I think it should be universal to all games. 
> > > 
> > > Question: How and why does the Answerer respond to its teammate and not to the enemy Questioner?
> > > 
> > > 
> > > 


---



</div>
<div class="column-right">

# 日本語訳

# [修正済] - トップ9のLBはエラーによる結果
**クリス・デオッテ** *2024年5月29日 23:00:06 JST* (19票)
5月29日14:00 UTCに、LBの上位9エージェントが全て、チームメイトのエラーからポイントを得ていることに気付きました。（14:00 UTCの上位9チームは、Dapeng、Agney、Neel、Mitul、Neige、Agney、Gol-eel、tr、Mesmerizedです）。  
LBの上位9エージェントの最近のゲームをレビューし、ポジティブなポイントを得た状況を以下に示します。各ケースで、彼らはチームメイトのエラーによってポイントを得ました。  
これは意図されたスコアリングメカニズムなのでしょうか？[@develra](https://www.kaggle.com/develra) [@addisonhoward](https://www.kaggle.com/addisonhoward) 運がチームがLBを上げる理由になるべきなのでしょうか？  
私の意見では、エージェントがエラーを起こした場合、その不具合のあるボットはポイントを失い、他の3つのボットはゲームを無視するべきです。（つまり、他の3つのボットはゼロポイントになり、すぐにエラーのあったゲームを置き換える新しいゲームを開始するのです）。  
キーワードを予測するのは難しく、多くのフリーポイントを獲得するための簡単な方法があってはいけません。（そして非公開LBでは、キーワードリストがないため、予測がさらに難しくなるでしょう）。

## 1位 
## 2位 
## 3位 
## 4位 
## 5位 
## 6位 
## 7位 
## 8位 
## 9位 

---

 # 他のユーザーからのコメント
> ## クリス・デオッテ トピック作成者
> 
> アップデート。5月30日14:00 UTCに同じことが起こっていることに気付きました。新しい1位がLB660にジャンプしましたが、その原因はチームメイトのエラーです。このため、元々のトップLBボットは、実際のスコアが600未満のこれらのボットと対戦することになってしまいます。  
> 
> ## 新しい1位 
> 
> ## 新しい5位 
> 
> そして、新しい5位もチームメイトのエラーからそこにジャンプしました：
> 
> > ## オミナスデュード
> > 
> > このコンペの創設者は、これを早急に修正する必要があります。😑
> > 
> > > ## オミナスデュード
> > > > 上位25のLBを見ているのですが、その中の25チームのうち11チームがエラーによってポイントを得ています。
> > > > 

---
> ## オミナスデュード
> 
> こんにちは、1位のエラーボットは私のもので、なぜエラーが起こっているのか全くわかりません。今、調べているところです。このことを知らせてくれてありがとう。私は意図的に上位にポイントを与えようとは思っていませんでした。
> 
> > ## オミナスデュード
> > > 私のボットも3位です 😭。エラーボットを上書きするために、古いボットを三つ提出することにしました。これは一時的な解決策です。不公平なリーダーボードに貢献したくないからです。
> 
> > > > ## クリス・デオッテ トピック作成者
> > > > こんにちはオミナスデュード。謝る必要はありません。誰のボットも、解決策を開発する過程でエラーを起こすことがあります。私のボットの初期バージョンにもエラーがあり、毎日エラーを取り除いて改善しています。だから、エラーがあるボットを提出することを心配しないでください。新しいことを試し、自由に提出を続けてください。  
> > > > 私は競技のメトリックが更新され、ボットのエラーが他のボットに役立たないようにすべきだと思います。
> > > > 
> > > > > ## オミナスデュード
> > > > > > はい、それが最適な解決策です。しかし、今のところはエラーが修正されるまでボットを取り除くのが私の一時的な解決策です。私のボットに問題を知らせてくれてありがとう。私のエージェントが他のボットと対戦するたびにほぼ常に+10のように改善しているのに、スコアが常に低いのが何か変なことだと思っていました。
> > > > > > 
> > > > 

---
> ## ボバード・ドーチュク-ティベリ
> 
> 現在これを確認しています。報告してくれてありがとう。
> 
> > ## ボバード・ドーチュク-ティベリ
> > > 明日までにこれの修正が行われる予定です。この後エージェントがエラーを起こした場合の報酬はネットゼロにします。例えば、エラーを起こしたエージェントが-21ポイントになり、他の3つはそれぞれ平均+7ポイントを得ることになります。  
> > > エラーを起こしたエージェントを処罰することは、リーダーボードを明確に保ち、「意図的にエラーを起こす」戦略を存在させないために重要です。（例: エージェントがXラウンドの後にまだ推測しておらず、自分のレベルでの平均ゲームはX + 1であることを知っている場合、罰則がなければ意図的にエラーを起こすことができます）。  
> > > 
> > > 
> > > ## ボバード・ドーチュク-ティベリ
> > > > これは今実装されています
> > > > 
> > > > 
---
> ## ギバ
> 
> 私はクリスの言うことを支持します。LBでエージェントのエラーが他のエージェントにフリーポイントを分配するのを観察しました。
> 
> 
---
> ## クリス・デオッテ トピック作成者
> 
> [@ボバード](https://www.kaggle.com/bovard) 私は、モハメドが（6月4日）チームメイト（私クリス）のエラーによって130ポイントを受け取ったことに気付きました。LBの他のチームは130ポイントを得るために5回以上の勝利を収める必要があります（これは5つ以上の単語を正しく推測するという難しい業績を要します）運よくチームメイトのエラーによって得られた結果とは異なります。  
> 
> FYI、Kaggleはエラーがあるチームのチームメイトへのポイント付与を修正したと言っていますが、これは修正されたようには見えません：
> 
> > ## ボバード・ドーチュク-ティベリ
> > > はい、私もそれを見ました。競技の最後のラウンドでエージェントがエラーを起こした場合、バグが存在しているようです。この問題は[https://github.com/Kaggle/kaggle-environments/pull/275](https://github.com/Kaggle/kaggle-environments/pull/275)で修正されました。
> > > 
> > > 
---
> ## アンドレス・H・ザプケ
> 
> こんにちは！  
> 一つ質問がありますが、回答者はそもそもどこから来るのですか？これは独立してトレーニングされる必要がある単独のLLMであるべきなのでしょうか？  
> そして、回答者が正しく答えないために「正しい」推測が適切に評価されていないというのは、私の理解で合っていますか？
> 
> > ## クリス・デオッテ トピック作成者
> > > 各マッチには4つのKaggleチームがあります、質問者+回答者 対 質問者+回答者、すなわち2対2です。  
> > > 各回答者は正しい回答を知っており、その情報を質問者であるチームメイトに伝えます。  
> > >  
> > > > ## アンドレス・H・ザプケ
> > > > はい、でも回答者はハードコードされたボットではないはずで、質問を正しく解釈する必要があります。彼が私たちの「質問者LLM」を評価する役割を持っていると思ったので、すべてのゲームに共通であるべきだと思います。  
> > > > 質問：回答者はなぜ敵の質問者ではなく、チームメイトに応じるのですか？  
> > > > 
> > > >


</div>