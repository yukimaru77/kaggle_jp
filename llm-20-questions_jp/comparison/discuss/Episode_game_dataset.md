# 要約 
ディスカッションでは、リーダーボードからダウンロードできるjsonリプレイファイルが読みづらいことが指摘されています。このファイルには、20ラウンドにわたる6つのエージェントに関する観測が含まれており、重複が多いため扱いが難しいとのことです。ユーザーは、これらのデータをより軽量なデータフレームにフォーマットし、csvとして保存するためのノートブックを作成したと述べています。また、毎日更新される全てのゲームを取得するためにmeta kaggleデータセットを使用していることも言及されています。ノートブックのリンクも提供されています。

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

# Episode game dataset

**waechter** *Wed May 22 2024 04:32:41 GMT+0900 (日本標準時)* (3 votes)

Hello,

The json replay files that can be download from the leaderboaed are not very readable. It contains observation for each 6 agents ( 'ask', 'guess', 'answer' * 2 teams) for each rounds (up to 20), so there is a lot of duplicate. 

I made a notebook to format them into a lighter dataframe and save it a csv for later use. Using the meta kaggle dataset to get all game played, updated daily

link : [https://www.kaggle.com/code/waechter/llm-20-questions-games-dataset](https://www.kaggle.com/code/waechter/llm-20-questions-games-dataset)

I think it can be useful





</div>
<div class="column-right">

# 日本語訳

> こんにちは、  
> リーダーボードからダウンロードできるjsonリプレイファイルはあまり読みやすくありません。各ラウンド（最大20ラウンド）の6つのエージェント（'ask'、'guess'、'answer' * 2チーム）に関する観測が含まれているため、重複が多いです。  
> 私は、それらをより軽量なデータフレームにフォーマットし、後で使用するためにcsvとして保存するノートブックを作成しました。毎日更新される全てのゲームを取得するためにmeta kaggleデータセットを使用しています。  
> リンク: [https://www.kaggle.com/code/waechter/llm-20-questions-games-dataset](https://www.kaggle.com/code/waechter/llm-20-questions-games-dataset)  
> これが役に立つと思います。


</div>