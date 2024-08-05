# 要約 
このディスカッションは、Kaggleコンペティション「LMSYS - Chatbot Arena 人間による好み予測チャレンジ」における、9時間の実行時間制限に関する質問と回答についてです。

質問者は、提出物が9時間の実行時間制限を超えても、リーダーボード（LB）スコアを取得した場合、プライベートスコア（PV）も取得できるのか疑問を持っています。

Valentin Wernerは、プライベートスコアは提出時にすでに計算されているため、LBスコアを取得していれば提出は問題ないと回答しています。

Rise_Handは、この回答を受けて、モデルのアンサンブルや後処理を行う際には注意が必要であるとコメントしています。

要約すると、このディスカッションは、コンペティションにおける時間制限と提出物の評価方法に関する質問と回答、そしてその回答に対する追加コメントで構成されています。


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

# [question]9h time limit 

**Roschild.Rui** *Thu Jul 25 2024 17:26:58 GMT+0900 (日本標準時)* (6 votes)

Will the organizers rerun our submission on the test set, or will we receive a PV score as long as we successfully submit and have an LB score? 

I saw some situations that when the running time was out of 9 hours the notebook was still running and got a lb score



---

 # Comments from other users

> ## Valentin Werner
> 
> Private scores are already calculated during your submission. So if you got a LB score, your submission is fine.
> 
> 
> 


---

> ## Rise_Hand
> 
> Yes, thus we should be very careful to ensemble our models or make any post processing
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# [質問] 9時間の時間制限

**Roschild.Rui** *2024年7月25日 17:26:58 (日本標準時)* (6票)

主催者はテストセットに対して私たちの提出物を再実行しますか？それとも、提出が成功してLBスコアがあれば、PVスコアを受け取れますか？

9時間の実行時間が過ぎても、ノートブックがまだ実行中でLBスコアを取得した状況をいくつか見ました。

---
# 他のユーザーからのコメント

> ## Valentin Werner
> 
> プライベートスコアは、提出時にすでに計算されています。そのため、LBスコアを取得した場合は、提出は問題ありません。
> 
> 
> 
---
> ## Rise_Hand
> 
> はい、そのため、モデルをアンサンブルしたり、後処理を行ったりする際には注意が必要です。
> 
> 
> 
--- 



</div>