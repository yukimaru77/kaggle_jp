# 要約 
このディスカッションは、Kaggleコンペティションでノートブックを実行中に発生した例外に関するものです。投稿者は、ノートブックが長時間実行された後に例外が発生し、原因を突き止める方法がないと述べています。

他のユーザーからのコメントでは、いくつかの解決策が提案されています。

* Valentin Wernerは、"null"の処理方法が問題である可能性を指摘し、`response.replace("null","'null'")` を使用して解決策を提案しています。また、GPUがOOMになった場合、バッチサイズや最大長を小さくすることを提案しています。
* Varun Jagannathは、バッチサイズに問題があることを確認しています。
* Robert Turroは、ノートブックのログセクションを確認することを提案しています。

このディスカッションは、Kaggleコンペティションで発生する可能性のある一般的な問題と、その解決策について示しています。


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

# Notebook throwing Exception

**Varun Jagannath** *Wed Jul 10 2024 23:45:51 GMT+0900 (日本標準時)* (0 votes)

After submitting the notebook. And, after some grueling hours it throws exception and there is no way to find out about it. Is there any other way to check.



---

 # Comments from other users

> ## Valentin Werner
> 
> This is just one potential issue, but how are you handling the "null" that sometimes occur? Doing this helped for me in the early submissions: response.replace("null","'null'") <-- note the extra ' to make it a string before loading the string representation of the list an actual list (e.g., with ast.literal_eval(response))
> 
> I really hope this is doing it for you - because these exceptions can be nasty. If not, maybe try debugging by predicting on training data again.
> 
> If the GPU goes OOM its not an OOM error on kaggle but an Exception, so maybe reduce batch size or max length too. Best of luck!
> 
> 
> 
> > ## Varun JagannathTopic Author
> > 
> > Looks like its an issue with batch size
> > 
> > 
> > 


---

> ## Robert Turro
> 
> Try clicking on the notebook then going to the Logs section.
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# ノートブックで例外が発生

**Varun Jagannath** *2024年7月10日 水曜日 23:45:51 日本標準時* (0票)

ノートブックを提出した後、何時間もかけて実行した結果、例外が発生し、原因を突き止める方法がありません。確認する方法はあるでしょうか？

---
# 他のユーザーからのコメント

> ## Valentin Werner
> 
> これは考えられる問題の1つに過ぎませんが、時々発生する「null」をどのように処理していますか？ 私の初期の提出では、これを行うことで役立ちました: response.replace("null","'null'") <-- 注意: 文字列のリストの文字列表現を実際のリストにするために、追加の ' を付けて文字列にします (例: ast.literal_eval(response) を使用)。
> 
> これがあなたにも役立つことを願っています - なぜなら、これらの例外は厄介なものになり得るからです。そうでない場合は、トレーニングデータで再度予測することでデバッグを試してみてください。
> 
> GPU が OOM になった場合、Kaggle では OOM エラーではなく例外が発生するため、バッチサイズや最大長を小さくしてみてください。頑張ってください！
> 
> 
> 
> > ## Varun Jagannath トピック作成者
> > 
> > バッチサイズに問題があるようです。
> > 
> > 
> > 
---
> ## Robert Turro
> 
> ノートブックをクリックして、ログセクションに移動してみてください。
> 
> 
> 
--- 



</div>