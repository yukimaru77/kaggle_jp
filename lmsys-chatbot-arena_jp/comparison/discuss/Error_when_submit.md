# 要約 
このディスカッションは、Kaggleコンペティション「LMSYS - Chatbot Arena 人間による好み予測チャレンジ」における提出に関する問題についてです。

ユーザーの Nguyễn Anh Tú は、ノートブックを提出した際に「Submission Scoring Error」と「Notebook Threw Exception」という2つのエラーに遭遇しました。

Valentin Werner は、この問題に対する解決策を提案しました。

* **提出スコアエラー:** 提出ファイルに `id` 列が含まれていることを確認する必要があります。
* **ノートブックが例外をスローしました:** これは、GPU のメモリ不足、応答に「null」が含まれている、または実行時に実際にエラーが発生しているなどの理由が考えられます。

Nguyễn Anh Tú は、Valentin Werner のアドバイスが役に立ったとコメントしています。

要約すると、このディスカッションは、Kaggleコンペティションにおける提出エラーのトラブルシューティングに関するものであり、Valentin Werner はユーザーに役立つ解決策を提供しました。


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

# Error when submit

**Nguyễn Anh Tú** *Mon Jul 15 2024 16:23:48 GMT+0900 (日本標準時)* (0 votes)

I got the error "Submission Scoring Error" when I submitted  my notebook, I thought that I set the wrong format for my submission.csv. Then, I read the sample_submission.csv and change the the value of ['winner_model_a', 'winner_model_b', 'winner_tie'] columns with my y_predict. The worst thing is my notebook ran successful but when I submitted again I got the error "Notebook Threw Exception", please help me!



---

 # Comments from other users

> ## Valentin Werner
> 
> ### Submission scoring error -> make sure that you include id
> 
> An example way to get a working submission:
> 
> ```
> # Submit
> sub = pd.DataFrame(sm, index = test.id, columns = ["winner_model_a","winner_model_b","winner_tie"]).reset_index()
> sub.to_csv('submission.csv', index=False)
> sub.head()
> 
> ```
> 
> where sm is an array like np.array([0.123,0.567,0.234],…,[0.999,0.000,0.001])
> 
> ### Notebook threw exception
> 
> You managed to make a working notebook not work anymore 😀 This could have some reasons: GPU goes OOM (this does not trigger an OOM Error); There are some "null" responses in the responses which need to be handled (e.g., replace null with 'null' before loading the string representation of the list as real list); There is actually an error raised during runtime.
> 
> What you can do to evaluate the errors is try to run your inference code on the half the train set (which is basically the size of test) and see what happens.
> 
> 
> 
> > ## Nguyễn Anh TúTopic Author
> > 
> > It's very helpful for me. Thanks a lot.
> > 
> > 
> > 


---



</div>
<div class="column-right">

# 日本語訳

# 提出時のエラー

**Nguyễn Anh Tú** *2024年7月15日 月曜日 16:23:48 日本標準時* (0票)
ノートブックを提出した際に「Submission Scoring Error」というエラーが発生しました。提出ファイルのフォーマットが間違っているのではないかと考え、`submission.csv` のフォーマットを確認し、`['winner_model_a', 'winner_model_b', 'winner_tie']` 列の値を自分の `y_predict` で置き換えました。最悪なことに、ノートブックは正常に実行されたのですが、再度提出したところ「Notebook Threw Exception」というエラーが発生しました。助けてください！
---
# 他のユーザーからのコメント
> ## Valentin Werner
> 
> ### 提出スコアエラー -> `id` を含めることを確認してください
> 
> 動作する提出ファイルの例：
> 
> ```
> # 提出
> sub = pd.DataFrame(sm, index = test.id, columns = ["winner_model_a","winner_model_b","winner_tie"]).reset_index()
> sub.to_csv('submission.csv', index=False)
> sub.head()
> 
> ```
> 
> ここで、`sm` は `np.array([0.123,0.567,0.234],…,[0.999,0.000,0.001])` のような配列です。
> 
> ### ノートブックが例外をスローしました
> 
> 動作していたノートブックが動かなくなったんですね 😀 これにはいくつかの理由が考えられます。GPU が OOM になった（これは OOM エラーをトリガーしません）。応答に「null」が含まれていて、処理する必要がある（例えば、文字列表現のリストを実際のリストとして読み込む前に、null を 'null' に置き換える）。実行時に実際にエラーが発生している。
> 
> エラーを評価するためにできることは、推論コードをトレーニングセットの半分（テストのサイズと同じ）で実行してみて、何が起こるかを確認することです。
> 
> 
> 
> > ## Nguyễn Anh Túトピック作成者
> > 
> > とても役に立ちました。ありがとうございます。
> > 
> > 
> > 
---



</div>