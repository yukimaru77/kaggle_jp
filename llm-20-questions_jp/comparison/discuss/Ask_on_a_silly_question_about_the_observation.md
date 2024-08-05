# 要約 
コンペのディスカッションでは、参加者のGODDiaoが、llm_20_questions.pyのコードにおいて「active」や「inactive」といったオブジェクトが十分に説明されていないことに気づき、obsオブジェクトのメソッド（obs.turnTypeやobs.questionなど）についての情報をどこで確認できるかを尋ねています。それに対して、Bovard Doerschuk-Tiberiが、デバッグモードで実行し、`print(dir(obs))`を使うことで利用できるオブジェクトの詳細を確認できると回答しています。

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

# Ask on a silly question about the observation

**GODDiao** *Sun Jun 02 2024 16:32:43 GMT+0900 (日本標準時)* (1 votes)

I have read the code in llm_20_questions.py. I have noticed that many objects like active, and inactive has not been explained very clearly.

I am wondering where I can see the methods of the objects like obs…

obs.turnType, obs. question etc….



---

 # Comments from other users

> ## Bovard Doerschuk-Tiberi
> 
> throwing a print(dir(obs)) in and running with debug mode should show you everything in there!
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# 観察に関するちょっとした質問
**GODDiao** *2024年6月2日 16:32:43 JST* (1票)
llm_20_questions.pyのコードを読んでみたところ、activeやinactiveといった多くのオブジェクトが明確に説明されていないことに気付きました。
obsのようなオブジェクトのメソッド（obs.turnTypeやobs.questionなど）をどこで見ることができるのか、気になっています。
---
 ## ユーザーからのコメント
> ## Bovard Doerschuk-Tiberi
> 
> debugモードで実行し、print(dir(obs))を使えば、そこにあるすべてのものが表示されるはずですよ！


</div>