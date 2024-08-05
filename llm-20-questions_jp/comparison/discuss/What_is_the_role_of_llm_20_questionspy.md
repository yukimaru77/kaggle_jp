# 要約 
ディスカッションでは、参加者のMatthew S Farmerが、コンペティションにおける入力ファイル「llm_20_questions.py」の役割や提出物のフォーマットについて疑問を持っています。特に、エージェント構築時にこのファイルを参照すべきか、プロンプトが上書きされるかどうかを尋ねています。

それに対して、別のユーザー（loh-maa）が回答し、llm_20_questions.pyはゲーム実行環境の一部であり、参加者が実装する必要があるのは「agent_fn」関数であると説明しています。具体的なコード例を挙げて、どのように機能するかを示し、理解を助けるためのノートブックリンクを提供しています。

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

# What is the role of llm_20_questions.py

**Matthew S Farmer** *Wed Jun 12 2024 05:41:55 GMT+0900 (日本標準時)* (0 votes)

I am having trouble understanding the role of the input .py file when thinking of this competition in context and the way that a submission should be formatted. 

Do the agents defined in the input notebook override any prompts set in our submissions? 

Should we be referencing this input file during agent creation? 

I apologize if the answer is painfully obvious, I am trying to learn here. 



---

 # Comments from other users

> ## loh-maa
> 
> You don't need to worry about llm_20_questions.py, it's part of the environment to run the game. You need to implement agent_fn function, e.g.:
> 
> ```
> def agent_fn(obs, cfg):
>     if obs.turnType == "ask":
>         response = "Is it a duck?"
>     elif obs.turnType == "answer":
>         response = "no"
>     elif obs.turnType == "guess":
>         response = "two ducks"
>     return response
> 
> ```
> 
> [This notebook](https://www.kaggle.com/code/rturley/run-debug-llm-20-questions-in-a-notebook) should help you understand.
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# llm_20_questions.pyの役割について
**Matthew S Farmer** *2024年6月12日 05:41:55 JST* (0票)
このコンペティションにおける入力の.pyファイルの役割と、提出物のフォーマットについて考えるとき、よく理解できていません。  
入力ノートブックで定義されたエージェントは、私たちの提出物に設定されたプロンプトを上書きするのでしょうか？  
エージェントを作成する際にこの入力ファイルを参照するべきですか？  
もし答えが明白であれば申し訳ありません、私は学ぼうとしています。

---

# 他のユーザーからのコメント
> ## loh-maa
> 
> llm_20_questions.pyについて心配する必要はありません。これはゲームを実行するための環境の一部です。あなたが実装する必要があるのは、agent_fn関数です。例えば、以下のようになります：
> 
> ```
> def agent_fn(obs, cfg):
>     if obs.turnType == "ask":
>         response = "それはアヒルですか？"
>     elif obs.turnType == "answer":
>         response = "いいえ"
>     elif obs.turnType == "guess":
>         response = "アヒルが2匹"
>     return response
> ```
> 
> [このノートブック](https://www.kaggle.com/code/rturley/run-debug-llm-20-questions-in-a-notebook)が理解の助けになると思います。
> 
> ---


</div>