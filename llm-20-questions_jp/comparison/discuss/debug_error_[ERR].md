# 要約 
ディスカッション概要:

Paul Pawlettaがコンペティションに参加し、LLama 8Bノートブックを使ったテスト提出で、エージェントが一回のラウンドで-237のペナルティを受けたことに関するデバッグエラーについて報告しています。リプレイは正常に動作するものの、エージェントのログには何の情報も記録されていないと述べています。この問題について、他の参加者からの助言を求めています。

それに対して、waechterはデバッグを助けるために提出物にprint文を追加することを提案し、stdoutに表示されるはずだとアドバイス。また、応答がコンペティションのルールに従っていることを確認するように促しています。

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

# debug error [ERR]

**Paul Pawletta** *Wed Jul 31 2024 00:32:11 GMT+0900 (日本標準時)* (0 votes)

just joined the competition now and ran the LLama 8B notebook as a test submission. It works fine until one round where the agent gets penalized with -237 in one round.

The replay works fine until the very end and the agent logs don't show anything 🤷‍♂️ Did anyone encounter this issue too or knows ways to debug this?



---

 # Comments from other users

> ## waechter
> 
> To help you debug you can add print to your submission, you will see them in stdout
> 
> Make sure your response follows the [rules](https://www.kaggle.com/competitions/llm-20-questions/overview/20-questions-rules)
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# デバッグエラー [ERR]
**Paul Pawletta** *2024年7月31日 00:32:11 (日本標準時)* (0票)
今コンペに参加して、テスト提出としてLLama 8Bノートブックを実行しました。うまく動作していたのですが、一回のラウンドでエージェントが-237のペナルティを受けてしまいました。
リプレイは最後まで正常に動作するのですが、エージェントのログには何も表示されていません 🤷‍♂️ 同じ問題に遭遇した方や、デバッグの方法を知っている方はいませんか？

---
 # コメント
> ## waechter
>
> デバッグを助けるために、提出物にprint文を追加することをお勧めします。stdoutに表示されるはずです。
>
> 応答が[ルール](https://www.kaggle.com/competitions/llm-20-questions/overview/20-questions-rules)に従っていることを確認してください。


</div>