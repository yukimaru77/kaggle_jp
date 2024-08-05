# 要約 
このディスカッションでは、Kaggleの「LLM 20 Questions」コンペティションにおけるリーダーボードスコアの不安定さについて議論されています。ユーザー**alekh**は、トップから急落し再浮上するスコア変動に疑問を呈し、全プレイヤーのスコアがいつか収束するかどうかに懸念を示しています。

他のユーザーからのコメントでは、以下のような意見が寄せられています：
- **RS Turley**は、スキルの高いエージェントが勝利を重ねるにつれて収束が進むと予測しつつ、公開キーワードに最適化されたエージェントが偽のスコアを生む可能性があることを指摘。また、締切後には新しいエージェントが上位に昇るかもしれないとも述べています。
- **Kuldeep Rathore**も同様の感想を持ち、運の要素が大きいと感じています。
- **Giba**は、リーダーボードが周期的なランダムシャッフルのように見え、エージェントの不具合によって安定しないことを述べています。また、相手のエージェントのエラーを利用してポイントを大幅に得ることができるとも指摘しています。

全体として、参加者たちはリーダーボードの不安定さとその要因について様々な視点から考察しています。

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

# Convergence of leaderboard scores

**alekh** *Sun May 26 2024 07:12:10 GMT+0900 (日本標準時)* (2 votes)

I don't understand, how can I go from 1st, down to 36th, back up to 1st, and down to 94th on the leaderboard?

Are you guys sure this will converge to a stable score for all players? Because if not it will be quite arbitrary who wins and be based on timing.



---

 # Comments from other users

> ## RS Turley
> 
> In looking through the current matches, most of the submissions seem to be random experiments. I'd guess: 
> 
> - we will see a lot more convergence as agents with more skill start to consistently win matches
> 
> - part of the convergence will be fake as some agents are optimized on the public keywords
> 
> - after August 13th, the agents at top of the leaderboard that are optimized on the public keywords will drop off and a new set of agents will converge to the top of the leaderboard
> 
> 
> 


---

> ## Kuldeep Rathore
> 
> I also feel the same. Here the luck is dependent on person, place and thing 😂
> 
> 
> 
> > ## VolodymyrBilyachat
> > 
> > Yes and some agents seems to take return default yes or no all the time :D
> > 
> > 
> > 


---

> ## Giba
> 
> Current LB looks like a periodic random shuffle.  There are many broken agents all around which makes impossible to have a stable LB.
> 
> 
> 
> > ## Giba
> > 
> > Also watching some replays is possible to get +40 to +100 LB points just because one opponent agent returns error.
> > 
> > 
> > 


---



</div>
<div class="column-right">

# 日本語訳

# リーダーボードスコアの収束について
**alekh** *2024年5月26日 07:12:10 JST* (2票)
どういうことなのか理解できません。どうして1位から36位に落ち、その後再び1位に返り咲き、またしても94位に落ちることができるのでしょうか？皆さん、本当に全プレイヤーのスコアは安定して収束すると思いますか？そうでなければ、誰が勝つかがかなり恣意的になり、タイミング次第ということになります。

---
# 他のユーザーからのコメント
> ## RS Turley
> 現在の試合を見ていると、多くの提出物はランダムな実験のように思えます。私の予想では：
> - より高いスキルを持つエージェントが一貫して試合に勝つようになると、収束がさらに見られるようになるでしょう。
> - 収束の一部は、公開キーワードに最適化されたエージェントによるもので、偽のものになるでしょう。
> - 8月13日以降、公開キーワードに最適化されたリーダーボードの上位のエージェントは順位を下げ、新たなエージェントがトップに収束するはずです。

---
> ## Kuldeep Rathore
> 私も同じように感じています。ここでは運が人、場所、物に依存していますね 😂
>
> > ## VolodymyrBilyachat
> > はい、一部のエージェントは常に「はい」または「いいえ」のデフォルトで返答しているようです :D
> > 

---
> ## Giba
> 現在のリーダーボードは周期的なランダムシャッフルのように見えます。多くの不具合を抱えたエージェントが存在するため、安定したリーダーボードが保持できません。
>
> > ## Giba
> > また、再生を見ていると、相手のエージェントがエラーを返すことで、+40から+100のリーダーボードポイントを獲得することも可能です。
> > 


</div>