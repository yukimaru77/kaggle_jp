# 要約 
このディスカッションでは、コンペティションの基本的なゲームメカニズムについての質問が交わされています。ユーザーの**GODDiao**が、ゲームには2対2の形式で4つのエージェントが必要なのか、また、ファイルの提出形式について疑問を投げかけています。さらに、Kaggleの環境で提出したエージェントがどのように動作するのかに関する詳しい説明を求めています。

これに対して、**RS Turley**が回答し、提出するエージェントは「質問」「回答」「推測」の役割を果たす1つの関数で十分であると説明しています。具体的には、簡単なエージェントの例を示し、エージェントの関数をPythonファイルにまとめて提出する必要があることを述べています。また、参加者は自分のエージェントが実際にチームとしてプレイする役割を担うことを確認しています。彼は上位チームのリプレイを観ることでも理解を深めることを勧めています。

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

# Question about the game mechanism

**GODDiao** *Thu Jun 06 2024 10:29:03 GMT+0900 (日本標準時)* (0 votes)

Hi, I am wondering about the basic 2v2 mechanism of the game. **Are we required to submit 4 agents that have 2 pairs of questioner and answerer agents in total? **

By the way, what form of the file do we need to submit? Is it the format like what we see in the LLM_20_questions starter notebook? 

The next problem is that we are unclear about how our file will work in the Kaggle environments. It means that after we submit our agents, how can the environment organize and use our codes to play the game? Hope I can get the explanation asap. 



---

 # Comments from other users

> ## RS Turley
> 
> You just need to submit one agent that knows how to handle 3 different roles: "ask", "answer" and "guess." For example, in the [notebook](https://www.kaggle.com/code/rturley/run-debug-llm-20-questions-in-a-notebook) that I posted to show how to run the environment locally, I made a simplistic agent like below:
> 
> ```
> def simple_agent1(obs, cfg):
>     if obs.turnType == "ask": response = "Is it a duck?"
>     elif obs.turnType == "guess": response = "duck"
>     elif obs.turnType == "answer": response = "no"
>     return response
> 
> ```
> 
> When you submit to the competition, you'll want your agent function to be in a python file like the "submission/main.py" example in the starter notebook, and the notebook shows you can add supporting files and zip them in one "submission.tar.gz" file.
> 
> During the competition, you're agent will be one of four different players in a 2v2 environment. Your agent will either be assigned to do all the "ask" and "guess" turns as it tries to guess the keyword for its team, or your agent will know the keyword and do all the "answer" turns as it teammate asks questions.
> 
> If you watch a replay or two from the top teams, it should make sense.
> 
> Good luck!
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# ゲームメカニズムに関する質問
**GODDiao** *2024年6月6日 10:29:03 JST* (0票)
こんにちは、ゲームの基本的な2対2メカニズムについて知りたいのですが、**質問者と回答者のエージェントのペアが2組合計4つのエージェントを提出する必要がありますか？**
それと、提出するファイルの形式は、LLM_20_questionsのスターターノートブックで見られる形式のようにする必要がありますか？次に、私たちのファイルがKaggleの環境でどのように動作するのかが不明です。つまり、エージェントを提出した後、環境はどのように私たちのコードを整理してゲームをプレイするのか、詳しい説明を期待しています。 

---
# 他のユーザーからのコメント
> ## RS Turley
>
> あなたが提出する必要があるのは、3つの異なる役割「質問」「回答」「推測」に対応できる1つのエージェントだけです。たとえば、私が地元での環境で実行する方法を示すために投稿した[ノートブック](https://www.kaggle.com/code/rturley/run-debug-llm-20-questions-in-a-notebook)には、以下のような単純なエージェントが含まれています：
> 
> ```python
> def simple_agent1(obs, cfg):
>     if obs.turnType == "ask": response = "それはアヒルですか？"
>     elif obs.turnType == "guess": response = "アヒル"
>     elif obs.turnType == "answer": response = "いいえ"
>     return response
> ```
> 
> コンペティションに提出する際には、エージェントの関数を「submission/main.py」のようなPythonファイルに入れる必要があります。ノートブックには、サポーティングファイルを追加し、それらを「submission.tar.gz」という1つのファイルに圧縮することができることが示されています。
> 
> コンペティション中、あなたのエージェントは2対2の環境の4人のプレイヤーの1人となります。あなたのエージェントは、チームのキーワードを推測しようとする際に、すべての「質問」と「推測」のターンを担当するか、キーワードを知っているにせよ、チームメイトが質問をする際にすべての「回答」のターンを担当します。
> 
> 上位チームのリプレイをいくつか見ると、理解が深まると思います。
> 
> 頑張ってください！


</div>