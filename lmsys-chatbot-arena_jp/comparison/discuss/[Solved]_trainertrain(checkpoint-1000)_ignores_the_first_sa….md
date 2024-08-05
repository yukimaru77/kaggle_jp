# 要約 
このディスカッションは、Transformers ライブラリでトレーニングを再開する際に、`trainer.train("checkpoint-x")` が最初のサンプルを無視するかどうかについてです。

質問者は、最初の4000サンプルでトレーニングを行い、その後、`trainer.train("checkpoint-1000")` を使用して4800サンプルでトレーニングを再開したところ、最初の4000サンプルがスキップされたように見えたと報告しています。

回答者は、トレーニングの再開には、以前に処理されたデータのバイパスが含まれることを説明しています。そのため、新しいデータセットでトレーニングを再開する場合、最初のサンプルを「ダミー」として追加する必要はありません。

質問者は、`dataset_a` でトレーニングを行い、`checkpoint` から `dataset_b` で再トレーニングした際に、`dataset_b` の最初のサンプルが無視されているように見えたと述べています。回答者は、この問題を解決するために、`model_name` を `checkpoint-1000` に指定し、その後、4800サンプルを使用して微調整することを提案しています。

このディスカッションは、Transformers ライブラリでトレーニングを再開する際に、最初のサンプルを無視する可能性があることを示しています。また、新しいデータセットでトレーニングを再開する場合、`model_name` を `checkpoint-x` に指定することで、最初のサンプルを無視せずにトレーニングを再開できることを示しています。


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

# [Solved] trainer.train("checkpoint-1000") ignores the first samples?: Resuming training in Transformers library. 

**ano** *Thu Aug 01 2024 15:27:59 GMT+0900 (日本標準時)* (0 votes)

My question is if trainer.train("checkpoint-x") ignores the first samples?

For example, I first trained using 4000 samples as train_dataset and got checkpoint-200, 400, 600, 800 and the last checkpoint as checkpoint-1000. And then I resumed training using 4800 samples by trainer.train("checkpoint-1000") and I got only checkpoint-1000 and checkpoint-1200 (no directory corresponding to 200-800). Does that mean the first 4000 samples were skipped?

In order to resume training using new training datasets, do we need to add the first samples as "dummy"? 



---

 # Comments from other users

> ## yechenzhi1
> 
> Yes, resuming training involves bypassing the previously processed data. If you wish to modify your dataset, you can specify 'model_name' as 'checkpoint-1000' and subsequently fine-tune it using your 4800 samples.
> 
> However, if you do so, your model will see the 4000 samples twice, is this what you want?
> 
> 
> 
> > ## anoTopic Author
> > 
> > Thank you for clarifying!
> > 
> > In my case, I trained with dataset_a and retrained with dataset_b from the checkpoint, but it seemed like the first samples in dataset_b was ignored. That's why I experimented a bit and asked this question here. Your answer is very helpful. Thank you so much!
> > 
> > 
> > 


---



</div>
<div class="column-right">

# 日本語訳

# [解決済み] trainer.train("checkpoint-1000") は最初のサンプルを無視するのか？: Transformers ライブラリでのトレーニング再開

**ano** *2024年8月1日 木曜日 15:27:59 JST* (0票)

trainer.train("checkpoint-x") は最初のサンプルを無視するのでしょうか？

例えば、最初に4000サンプルを train_dataset としてトレーニングし、checkpoint-200、400、600、800、そして最後のcheckpointとしてcheckpoint-1000を取得しました。その後、trainer.train("checkpoint-1000") を使用して4800サンプルでトレーニングを再開しましたが、checkpoint-1000とcheckpoint-1200しか取得できず（200-800に対応するディレクトリはありません）、最初の4000サンプルはスキップされたのでしょうか？

新しいトレーニングデータセットを使用してトレーニングを再開するには、最初のサンプルを「ダミー」として追加する必要があるのでしょうか？

---
# 他のユーザーからのコメント

> ## yechenzhi1
> 
> はい、トレーニングの再開には、以前に処理されたデータのバイパスが含まれます。データセットを変更したい場合は、'model_name' を 'checkpoint-1000' に指定し、その後、4800サンプルを使用して微調整することができます。
> 
> ただし、そうすると、モデルは最初の4000サンプルを2回見ます。これがあなたの意図でしょうか？
> 
> 
> 
> > ## anoTopic Author
> > 
> > ご説明ありがとうございます！
> > 
> > 私の場合、dataset_a でトレーニングし、checkpoint から dataset_b で再トレーニングしましたが、dataset_b の最初のサンプルが無視されているように見えました。そのため、少し実験して、ここで質問しました。あなたの回答は非常に役立ちます。どうもありがとうございました！
> > 
> > 
> > 
--- 



</div>