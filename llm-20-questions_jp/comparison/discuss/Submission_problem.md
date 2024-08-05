# 要約 
このディスカッションでは、ユーザー「Naive Experimentalist」がFlan T5に基づいたエージェントの提出に関する問題を報告しています。彼は新しいエージェントを開発したものの、バリデーションラウンドでエラーが発生し、ログが空で手がかりが掴めないと述べています。分析の結果、Kaggle環境でエージェントの名前が一致しなかったため、ファイル内の最後の関数が呼び出されたことに気づきましたが、正しい名前の付け方がわからず回避策を講じているとのことです。

他のユーザーからは、デバッグのためにエージェント関数にprint文を追加することを提案されています。Naive Experimentalistは、既存の考え方を改め、デバッグを行うことに同意しています。もう一人のユーザー「玛丽·伊丽莎白·马テミス」は、同様に困惑しているとコメントしています。

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

# Submission problem

**Naive Experimentalist** *Fri Jun 14 2024 04:45:36 GMT+0900 (日本標準時)* (2 votes)

Hi there.

I was able to submit my very first and very weak agent based on flan t5 large model.

Now I developed a new one (hopefully much smarter) using both Gemma and Flan T5. When submitting I have the validation round error, but logs are empty. I have no idea where to find help with this one. How to debug it? Before when having validation round problems, I saw some errors in the logs.

My logs look as follows:

log0: [[{"duration": 26.110363, "stdout": "", "stderr": ""}]]

log1: [[{"duration": 26.111393, "stdout": "", "stderr": ""}]]

Also no errors in the notebook execution log: Successfully ran in 483.4s

I have absolutely no idea what to do. Maybe someone was in this situation before.

UPDATE (Jun 14, 2024):

After a thorough analysis, it turned out that the Kaggle environment, when trying to run an agent and failing to match the appropriate name, calls the last function defined in the file. This may be obvious to everyone else, but it was a surprising discovery for me.

BTW, I still don't know how to name agents correctly so that the Kaggle environment calls them directly. For now, I have worked around this by defining a def proxy(obs) function at the end, which calls the appropriate agent depending on obs.role. 



---

 # Comments from other users

> ## waechter
> 
> You can add print in your agent function to help you debug, you will see them in stdout
> 
> 
> 
> > ## Naive ExperimentalistTopic Author
> > 
> > You are right. I thought the only problem with validation round can be when raising error from my notebook during the play, therefore didn't make traditional print-based debugging. Will do and try.Thx
> > 
> > 
> > 


---

> ## 玛丽·伊丽莎白·马特米斯
> 
> I have absolutely no idea too
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# 提出に関する問題
**Naive Experimentalist** *2024年6月14日金曜日 04:45:36 JST* (2票)
こんにちは。
私はFlan T5の大規模モデルに基づいた初めての非常に弱いエージェントを提出できました。
今、新たにGemmaとFlan T5の両方を使用した（おそらくはるかに賢い）エージェントを開発しました。提出の際にバリデーションラウンドエラーが発生しましたが、ログは空です。この問題の解決方法が全くわかりません。どのようにデバッグすれば良いのでしょうか？以前もバリデーションラウンドの問題が発生した際には、ログに何らかのエラーが表示されていました。
私のログは次の通りです：
log0: [[{"duration": 26.110363, "stdout": "", "stderr": ""}]]
log1: [[{"duration": 26.111393, "stdout": "", "stderr": ""}]]
また、ノートブックの実行ログにもエラーは表示されておらず：実行は成功し、483.4秒かかりました。
私には全く手がかりがありません。もしかしたら、同じ状況に直面した方がいるかもしれません。
更新（2024年6月14日）：
徹底的な分析の結果、Kaggle環境でエージェントを実行し、適切な名前と一致しなかった場合、ファイル内で定義された最後の関数を呼び出すことが判明しました。これは他の人には明らかかもしれませんが、私にとっては驚きの発見でした。
ところで、Kaggle環境が直接それらを呼び出すためにエージェントの名前を正しく付ける方法はまだわかりません。現在は、obs.roleに応じて適切なエージェントを呼び出すproxy(obs)関数をファイルの最後に定義することで回避しています。

---
# 他のユーザーからのコメント
> ## waechter
>
> エージェント関数にprintを追加してデバッグを手伝うことができます。stdoutに表示されます。
>
> 
> > ## Naive Experimentalist トピック作成者
> > 
> > 確かにそうですね。私はバリデーションラウンドの問題は、プレイ中にノートブックからエラーを発生させたときだけだと考えていたので、従来のprintを使ったデバッグを行いませんでした。試してみます。ありがとう。
> > 
> > 
---
> ## 玛丽·伊丽莎白·马テミス
> 
> 私も全くわかりません。


</div>