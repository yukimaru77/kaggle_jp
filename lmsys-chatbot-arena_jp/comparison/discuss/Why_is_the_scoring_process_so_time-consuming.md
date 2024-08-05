# 要約 
このディスカッションは、Kaggleコンペティションにおけるスコア計算の遅延に関するものです。ユーザー「David.Ricardo.H.X」は、提出したコードが正常に実行されたにもかかわらず、スコア計算が完了していないことを報告しています。

他のユーザーからのコメントでは、この遅延の原因として、以下の点が挙げられています。

* **データ量**: 提出時には、保存時よりもはるかに多くのデータが使用されるため、処理時間が長くなる。
* **ノートブックの複雑さ**: 複雑な計算や大規模なデータセットを使用している場合、処理時間が長くなる。
* **リソースの制約**: 計算リソースが限られている場合、処理時間が長くなる。
* **エラー処理**: システムはエラーが発生しても、すべてのセルを実行しようとすることがあるため、処理時間が長くなる。
* **自動評価**: 包括的なテストと検証には、時間がかかる。
* **システムオーバーヘッド**: コンテナのセットアップやデータ転送などのインフラストラクチャタスクは、遅延の原因となる。

これらのコメントから、スコア計算の遅延は、コンペティションの規模、ノートブックの複雑さ、システムの負荷など、さまざまな要因によって発生する可能性があることがわかります。


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

# Why is the scoring process so time-consuming

**David.Ricardo.H.X** *Thu May 30 2024 12:13:45 GMT+0900 (日本標準時)* (1 votes)


I submit successfully the code, the scoring is still running.
The submitted notebook throws error, the scoring is still running. 

Does anybody have the same issue? 



---

 # Comments from other users

> ## Valentin Werner
> 
> Note that time difference between Submission and save come from the data difference. During saving (the success / error you mentioned) the test data only has 3 rows, during submission its 25,000 rows. A subset of these rows are used for Public Leaderboard (what we see on Leaderboard right now), while most IS used for private Leaderboard / the score we see once the competition finished, and which is used for actual evaluation in the competition placement.
> 
> So you are running A LOT more data during submission, increasing runtime for row based operations
> 
> 
> 
> > ## Nguyễn Anh Tú
> > 
> > Does the data in file train.csv in submission environment different from the data in that file when we training model with our private notebook sir? 
> > 
> > 
> > 


---

> ## [Deleted User]
> 
> The scoring process can be time-consuming due to several factors:
> 
> Complexity of Notebook: Long-running computations or large datasets extend execution time.
> Resource Constraints: Limited computational resources and high submission volumes cause delays.
> Error Handling: Systems may attempt to run all cells despite errors to gather complete data.
> Automated Evaluation: Comprehensive testing and validation can take a significant amount of time.
> System Overhead: Infrastructure tasks such as container setup and data transfer add to the delay
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# スコアリングプロセスがなぜこんなに時間がかかるのですか？

**David.Ricardo.H.X** *2024年5月30日 木曜日 12:13:45 日本標準時* (1票)

コードを正常に提出しましたが、スコア計算がまだ実行中です。
提出されたノートブックがエラーをスローしても、スコア計算は実行中です。
同じ問題を抱えている人はいますか？
---
# 他のユーザーからのコメント
> ## Valentin Werner
> 
> 提出と保存の間の時間の差は、データの違いによるものです。保存時（あなたが言及した成功/エラー）には、テストデータは3行のみですが、提出時には25,000行です。これらの行のサブセットはパブリックリーダーボード（現在リーダーボードに表示されているもの）に使用され、ほとんどはプライベートリーダーボード/コンペティションが終了したときに表示されるスコアに使用され、コンペティションの順位付けの実際の評価に使用されます。
> 
> つまり、提出時にははるかに多くのデータを実行しているため、行ベースの操作の実行時間が長くなります。
> 
> 
> 
> > ## Nguyễn Anh Tú
> > 
> > 提出環境のtrain.csvファイルのデータは、プライベートノートブックでモデルをトレーニングするときのtrain.csvファイルのデータとは異なりますか？
> > 
> > 
> > 
---
> ## [削除されたユーザー]
> 
> スコアリングプロセスは、いくつかの要因により時間がかかる場合があります。
> 
> ノートブックの複雑さ: 長時間実行される計算や大規模なデータセットは、実行時間を延長します。
> リソースの制約: 計算リソースが限られている場合や、提出量が大きい場合は、遅延が発生します。
> エラー処理: システムは、エラーが発生しても、完全なデータを取得するためにすべてのセルを実行しようとすることがあります。
> 自動評価: 包括的なテストと検証には、かなりの時間がかかる場合があります。
> システムオーバーヘッド: コンテナのセットアップやデータ転送などのインフラストラクチャタスクは、遅延の原因となります。
> 
> 
--- 



</div>