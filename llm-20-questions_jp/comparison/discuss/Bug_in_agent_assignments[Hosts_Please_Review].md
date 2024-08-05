# 要約 
**ディスカッション要約:**

クリス・スミスは、コンペのスクリプト関数にバグがある可能性を指摘しています。具体的には、`llm_20_questions.py`ファイル内で、`guess`と`answer`の両方に「guesser」が設定されてしまうという問題です。彼は他の参加者が指摘した内容を受けて、この問題がリーダーボード用のコードに影響を与えるか確認したいとしています。

彼は、スクリプトの後半で適切なエージェントに再割り当てされるため、最初の設定が問題ではないかもしれないと考えているものの、ホストに実際にこのバグが影響を与えていないか確認をお願いしています。関連するコードのリンクも示されています。

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

# Bug in agent assignments[Hosts Please Review]

**Kris Smith** *Mon May 20 2024 03:07:46 GMT+0900 (日本標準時)* (3 votes)

I decided to start a new discussion thread to get some eyes on this. 

[@robikscube](https://www.kaggle.com/robikscube) mentioned this in another thread: 

We noticed that in the llm_20_questions.py file there looks to be a bug where both guesser and answerer are set as "guesser". Is this the same code used on the leaderboard?

[https://github.com/Kaggle/kaggle-environments/blob/da684ac3cd41a43c8cf7e103989c98bba8d05a61/kaggle_environments/envs/llm_20_questions/llm_20_questions.py#L31](https://github.com/Kaggle/kaggle-environments/blob/da684ac3cd41a43c8cf7e103989c98bba8d05a61/kaggle_environments/envs/llm_20_questions/llm_20_questions.py#L31)

```
GUESSER = "guesser"
ANSWERER = "guesser"

```

You can see his post here: [https://www.kaggle.com/competitions/llm-20-questions/discussion/503163#2821043](https://www.kaggle.com/competitions/llm-20-questions/discussion/503163#2821043)

I noticed the same thing in the code but ignored it as further down in the same script those variables are assigned using methods defined above them: 

```
agents = {GUESSER: guesser_agent, ANSWERER: answerer_agent}

```

[https://github.com/Kaggle/kaggle-environments/blob/da684ac3cd41a43c8cf7e103989c98bba8d05a61/kaggle_environments/envs/llm_20_questions/llm_20_questions.py#L87](https://github.com/Kaggle/kaggle-environments/blob/da684ac3cd41a43c8cf7e103989c98bba8d05a61/kaggle_environments/envs/llm_20_questions/llm_20_questions.py#L87)

Am I missing something? It does look like a bug when they are assigned the same value at the beginning of the code but then further down they appear to be assigned new appropriate values. 

Hosts could you please confirm this is not causing an issue?





</div>
<div class="column-right">

# 日本語訳

# エージェントの割り当てに関するバグ[ホストの確認をお願いします]
**クリス・スミス** *2024年5月20日 03:07:46 GMT+0900 (日本標準時)* (3票)

この問題について多くの人に目を向けてもらうために新しいディスカッションスレッドを始めることにしました。
[@robikscube](https://www.kaggle.com/robikscube)が別のスレッドで言及していたのですが、
llm_20_questions.pyファイルにおいて、guessとanswerの両方が「guesser」と設定されるバグがあるようです。これはリーダーボードで使用されているコードと同じなのでしょうか？
[こちらのリンク](https://github.com/Kaggle/kaggle-environments/blob/da684ac3cd41a43c8cf7e103989c98bba8d05a61/kaggle_environments/envs/llm_20_questions/llm_20_questions.py#L31)にご覧ください。
```
GUESSER = "guesser"
ANSWERER = "guesser"
```
彼の投稿は[こちらで確認できます](https://www.kaggle.com/competitions/llm-20-questions/discussion/503163#2821043)。
私も同様のことに気づきましたが、無視していました。その理由は、スクリプトの後半でそれらの変数が上で定義されたメソッドを使用して新たに割り当てられているからです：
```
agents = {GUESSER: guesser_agent, ANSWERER: answerer_agent}
```
[こちらのリンク](https://github.com/Kaggle/kaggle-environments/blob/da684ac3cd41a43c8cf7e103989c98bba8d05a61/kaggle_environments/envs/llm_20_questions/llm_20_questions.py#L87)にご覧ください。
私は何か見落としているのでしょうか？最初に同じ値が割り当てられた後、さらに下の部分では適切な新しい値が割り当てられるように見えます。
ホストの方々、この問題が実際に影響を及ぼしていないことを確認していただけますか？


</div>