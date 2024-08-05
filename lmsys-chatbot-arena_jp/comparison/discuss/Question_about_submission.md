# 要約 
このディスカッションは、Kaggleコンペティションにおける提出方法について、参加者Stanislav9801が質問しているものです。

Stanislav9801は、提出時に自分のノートブックがtest.csvファイルを入力として受け取り、submission.csvファイルを出力する必要があるのか、また、このtest.csvファイルは提供されたデータのtest.csvとは異なるものなのかを質問しています。

Cristóbal Mackenzieは、Stanislav9801の理解が正しいと回答し、提出時にtest.csvファイルには、ノートブックを編集しているときに表示される3つのサンプルだけでなく、すべてのテストデータが含まれると説明しています。 


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

# Question about submission

**Stanislav9801** *Thu Jul 18 2024 05:44:16 GMT+0900 (日本標準時)* (0 votes)

When creating submission, do my notebook should take as input test.csv file and produce output.csv file?

I mean, when I submit notebook, does test data will be loaded there dynamically, and through notebook inference submission.csv file should be produced? And this test.csv will not be the same as test.csv in the data provided?

So in this case my notebook should behave as a function, which takes test.csv as input, and submission.csv as output? Am I right?

This is my first time submission, so I don't understand this process a bit.

Thanks.



---

 # Comments from other users

> ## Cristóbal Mackenzie
> 
> Yes, you are right. On submission, the test.csv file will contain all test data, not just the three samples you see when editing a notebook.
> 
> 
> 
> > ## Stanislav9801Topic Author
> > 
> > Thank you!
> > 
> > 
> > 


---



</div>
<div class="column-right">

# 日本語訳

# 提出に関する質問

**Stanislav9801** *2024年7月18日 木曜日 05:44:16 日本標準時* (0票)
提出を作成する際、私のノートブックはtest.csvファイルを入力として受け取り、output.csvファイルを出力する必要がありますか？
つまり、ノートブックを提出すると、テストデータが動的にロードされ、ノートブック推論を通じてsubmission.csvファイルが生成されるのでしょうか？そして、このtest.csvは、提供されたデータのtest.csvとは異なるものになるのでしょうか？
つまり、この場合、私のノートブックは、test.csvを入力として、submission.csvを出力として受け取る関数として動作する必要がありますか？私の理解は正しいですか？
これは私の初めての提出なので、このプロセスをあまり理解していません。
ありがとうございます。
---
# 他のユーザーからのコメント
> ## Cristóbal Mackenzie
> 
> はい、その通りです。提出時に、test.csvファイルには、ノートブックを編集しているときに表示される3つのサンプルだけでなく、すべてのテストデータが含まれます。
> 
> 
> 
> > ## Stanislav9801トピック作成者
> > 
> > ありがとうございます！
> > 
> > 
> > 
---



</div>