# 要約 
ディスカッションでは、ユーザーのYangtze Haoが、ノートブックで正常に動作するエージェントを提出した際に「[validation episode error]」というエラーが発生した問題について述べています。オフラインテストではエラーはなく、成功したラウンドが続いた後にエラーが発生したことがログから確認できたため、問題はLLMモデルの.generateメソッドにあると推測しています。しかし、ノートブック内では問題がなかったため、他の参加者に助けを求めています。

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

# Notebook runs succeccfully but submission error

**Yangtze Hao** *Mon Jul 15 2024 17:59:44 GMT+0900 (日本標準時)* (1 votes)



I have tested the agent in the notebook with the internet off and no error occurred. But the submission keep showing [validation eposide error]. 

The agent 0 log shows that the error occurred after a few successful rounds

To make it clearer, I print the last error output in the log json. It seems that there's something wrong with .generate method of my llm model. But i didn't have any problems running the agent in the notebook. Can anyone help me





</div>
<div class="column-right">

# 日本語訳

# ノートブックは正常に動作していますが、提出でエラーが発生
**Yangtze Hao** *2024年7月15日 17:59:44 GMT+0900 (日本標準時)* (1票)
ノートブックでエージェントをオフラインでテストしたところ、エラーは発生しませんでした。しかし、提出すると「[validation episode error]」が表示され続けています。エージェント0のログを見ると、いくつかの成功したラウンドの後にエラーが発生したようです。状況を明確にするために、ログのJSON内の最後のエラー出力を印刷しました。どうやら私のLLMモデルの.generateメソッドに何か問題があるようです。しかし、ノートブックでエージェントを実行した際には問題はありませんでした。誰か助けてくれませんか？


</div>