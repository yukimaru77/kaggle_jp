# 要約 
このディスカッションは、Kaggleのコンペティション参加者が提出時にタイムアウトエラーに遭遇した問題について議論しています。

**主なポイント:**

* **問題:** ユーザーyechenzhi1は、ローカル環境では正常に動作するコードが、Kaggleの提出時にタイムアウトエラーを起こすことに悩んでいました。
* **原因:** 問題は、バッチサイズが大きすぎるために推論時間が長くなっていたことが判明しました。バッチサイズを1に減らすことで、問題は解決しました。
* **警告:** ユーザーは、cuDNN、cuFFT、cuBLASの登録に関する警告メッセージも受け取っていました。これは、バッチサイズを1に設定することで解決されましたが、警告自体は無視しても問題ないことがわかりました。
* **推論時間:** ユーザーは、推論時間の最適化について質問し、他のユーザーからいくつかのヒントを得ました。例えば、bf116=True、autocast()の使用、モデルの初期化などが挙げられます。
* **テストデータ:** ユーザーは、テストデータセットのサイズと、パブリックリーダーボードとプライベートリーダーボードでのデータ分割について質問しました。他のユーザーは、テストデータセット全体が使用され、プライベートデータ部分のスコアはコンテスト終了時に公開されることを説明しました。

**結論:**

このディスカッションは、Kaggleのコンペティションで発生する可能性のある一般的な問題と、その解決策について示しています。特に、バッチサイズ、推論時間、警告メッセージの処理など、重要なポイントが強調されています。


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

# submissions get timeout?

**yechenzhi1** *Sun May 19 2024 11:28:12 GMT+0900 (日本標準時)* (6 votes)

Hi, I'm new to kaggle. I've submitted several times, all all my submissions failed due to timeout, but when I run it in my local Kaggle environment with T4*2 the inference time is as follows:

And I got a warning like this:

2024-05-19 01:36:52.192095: E external/local_xla/xla/stream_executor/cuda/cuda_dnn.cc:9261] Unable to register cuDNN factory: Attempting to register factory for plugin cuDNN when one has already been registered

  2024-05-19 01:36:52.192192: E external/local_xla/xla/stream_executor/cuda/cuda_fft.cc:607] Unable to register cuFFT factory: Attempting to register factory for plugin cuFFT when one has already been registered

  2024-05-19 01:36:52.309490: E external/local_xla/xla/stream_executor/cuda/cuda_blas.cc:1515] Unable to register cuBLAS factory: Attempting to register factory for plugin cuBLAS when one has already been registered

But I'm sure GPU is used during the inference.

Any help would be appreciated. 



---

 # Comments from other users

> ## yechenzhi1Topic Author
> 
> thanks everyone helped! Setting batch size=1 solved my problem😃
> 
> 
> 


---

> ## yechenzhi1Topic Author
> 
> Another question is that, when we score in the public leaderboard, is the test dataset about 25000 * 0.3 rows? And when tested in the private leaderboard, it's about 25000 * 0.7 rows?
> 
> 
> 
> > ## Kishan Vavdara
> > 
> > Yes, that's correct! 
> > 
> > 
> > 
> > ## Rich Olson
> > 
> > I'll add that assuming this is like most contests - you're notebook is always run for the entire private / public test set.  It's just the scores for the private data portion of the scores is revealed at the end of the contest.
> > 
> > 
> > 


---

> ## lijiang3859
> 
> Hey, [@yechenzhi1](https://www.kaggle.com/yechenzhi1). Thanks for your sharing! I also got this warning:
> 
> ```
>   warnings.warn(
> 2024-07-06 05:05:32.818151: E external/local_xla/xla/stream_executor/cuda/cuda_dnn.cc:9261] Unable to register cuDNN factory: Attempting to register factory for plugin cuDNN when one has already been registered
> 2024-07-06 05:05:32.818272: E external/local_xla/xla/stream_executor/cuda/cuda_fft.cc:607] Unable to register cuFFT factory: Attempting to register factory for plugin cuFFT when one has already been registered
> 2024-07-06 05:05:32.956771: E external/local_xla/xla/stream_executor/cuda/cuda_blas.cc:1515] Unable to register cuBLAS factory: Attempting to register factory for plugin cuBLAS when one has already been registered
> 
> ```
> 
> However, my program does not raise bugs. Is there any influence on it?  By setting batch_size=1, the warning is gone?
> 
> 
> 
> > ## yechenzhi1Topic Author
> > 
> > We can ignore this warning.
> > 
> > 
> > 


---

> ## lijiang3859
> 
> I think I also have the same issue with model=llama3-8B. Here is my script:
> 
> ```
> results = []
> df = pd.read_csv(args.test_file, dtype={'prompt': str, "response_a":str, "response_b":str})
> df.fillna("''", inplace=True)
> df.replace('null', "'null'", inplace=True)
> 
> eval_dataset = Dataset.from_pandas(df)
> length =  len(eval_dataset)
> for i in tqdm(range(length)): # batch_size = 1
>     data = eval_dataset[i]
>     idx = data["id"]
>     resp_a = template.format(data['prompt'], data['response_a'])
>     resp_b = template.format(data['prompt'], data['response_b'])
>     resp_tokens = tokenizer(
>         [resp_a, resp_b],
>         max_length=args.max_total_length,
>         padding=True,
>         truncation=True,
>         return_tensors="pt",
>     )
>     # concated responses to save inference time -> batch_size =2
>     output = model(resp_tokens)
> 
> ```
> 
> Here is some other settings to speed up the inference process:
> 
> use bf116=True for model initialization.
> use autocast() and
> 
> Is there any other process to speed up the inference? I have tested it with 25000 samples, it is very risky to excel the total training budget with 9hrs.
> 
> 
> 
> > ## yechenzhi1Topic Author
> > 
> > [https://www.kaggle.com/code/emiz6413/llama-3-8b-38-faster-inference](https://www.kaggle.com/code/emiz6413/llama-3-8b-38-faster-inference)  you can check this notebook to see if it can help.
> > 
> > 
> > 


---

> ## Valentin Werner
> 
> One Remark, the test data has 25000 samples, so this will 10x your runtime. Technically that is still less than 540 minutes, but it is a lot slower
> 
> 
> 
> > ## yechenzhi1Topic Author
> > 
> > yes, so the prediction time should be 40x10 minutes, that's about 7 hours,  so it shouldn't be timeout.
> > 
> > 
> > 


---

> ## Rich Olson
> 
> how many rows are you testing prediction with?
> 
> (when you score - it scores against 25,000)
> 
> 
> 
> > ## yechenzhi1Topic Author
> > 
> > I tested 2500 rows, it was about 40 minutes.
> > 
> > 
> > 
> > > ## Rich Olson
> > > 
> > > well - I can't think of anything obvious.  just assuming you aren't doing anything that takes a bunch of time before inference? (training / pre-processing / generating embeddings)?
> > > 
> > > if you run out of ideas - I would try to test the workflow as close as possible to submission.
> > > 
> > > I would load 25k rows from "train" into your "test" dataframe (and drop columns / etc to make it look like test).
> > > 
> > > Then - I would save a version of your notebook.  That will run it like it was getting submitted.
> > > 
> > > You should then be able to look at the logs (even if it times out before finishing).
> > > 
> > > Might want to try adding some logging / debug statements before doing.
> > > 
> > > 
> > > 


---



</div>
<div class="column-right">

# 日本語訳

# 提出がタイムアウトする？

**yechenzhi1** *2024年5月19日 11:28:12 GMT+0900 (日本標準時)* (6票)

Kaggle初心者です。何回か提出しましたが、すべてタイムアウトで失敗しました。ローカルのKaggle環境でT4*2を使って実行したところ、推論時間は以下の通りです。

そして、このような警告が表示されました。

```
2024-05-19 01:36:52.192095: E external/local_xla/xla/stream_executor/cuda/cuda_dnn.cc:9261] Unable to register cuDNN factory: Attempting to register factory for plugin cuDNN when one has already been registered
  2024-05-19 01:36:52.192192: E external/local_xla/xla/stream_executor/cuda/cuda_fft.cc:607] Unable to register cuFFT factory: Attempting to register factory for plugin cuFFT when one has already been registered
  2024-05-19 01:36:52.309490: E external/local_xla/xla/stream_executor/cuda/cuda_blas.cc:1515] Unable to register cuBLAS factory: Attempting to register factory for plugin cuBLAS when one has already been registered
```

しかし、推論中にGPUが使用されていることは確かです。

何か助けがあれば幸いです。

---
# 他のユーザーからのコメント

> ## yechenzhi1トピック作成者
> 
> みんなの助けに感謝します！バッチサイズを1に設定したら問題が解決しました😃
> 
> 
> 
---
> ## yechenzhi1トピック作成者
> 
> もう一つ質問ですが、パブリックリーダーボードでスコアを計算する場合、テストデータセットは約25000 * 0.3行ですか？そして、プライベートリーダーボードでテストする場合、約25000 * 0.7行ですか？
> 
> 
> 
> > ## Kishan Vavdara
> > 
> > はい、その通りです！
> > 
> > 
> > 
> > ## Rich Olson
> > 
> > ほとんどのコンテストと同じように、ノートブックは常にプライベート/パブリックテストセット全体に対して実行されます。プライベートデータ部分のスコアは、コンテスト終了時に公開されるだけです。
> > 
> > 
> > 
---
> ## lijiang3859
> 
> こんにちは、[@yechenzhi1](https://www.kaggle.com/yechenzhi1)。共有してくれてありがとう！私もこの警告を受けました。
> 
> ```
>   warnings.warn(
> 2024-07-06 05:05:32.818151: E external/local_xla/xla/stream_executor/cuda/cuda_dnn.cc:9261] Unable to register cuDNN factory: Attempting to register factory for plugin cuDNN when one has already been registered
> 2024-07-06 05:05:32.818272: E external/local_xla/xla/stream_executor/cuda/cuda_fft.cc:607] Unable to register cuFFT factory: Attempting to register factory for plugin cuFFT when one has already been registered
> 2024-07-06 05:05:32.956771: E external/local_xla/xla/stream_executor/cuda/cuda_blas.cc:1515] Unable to register cuBLAS factory: Attempting to register factory for plugin cuBLAS when one has already been registered
> 
> ```
> 
> しかし、私のプログラムはバグを起こしていません。何か影響があるのでしょうか？バッチサイズを1に設定すると、警告は消えますか？
> 
> 
> 
> > ## yechenzhi1トピック作成者
> > 
> > この警告は無視できます。
> > 
> > 
> > 
---
> ## lijiang3859
> 
> 私もmodel=llama3-8Bで同じ問題が発生していると思います。私のスクリプトはこちらです。
> 
> ```
> results = []
> df = pd.read_csv(args.test_file, dtype={'prompt': str, "response_a":str, "response_b":str})
> df.fillna("''", inplace=True)
> df.replace('null', "'null'", inplace=True)
> 
> eval_dataset = Dataset.from_pandas(df)
> length =  len(eval_dataset)
> for i in tqdm(range(length)): # batch_size = 1
>     data = eval_dataset[i]
>     idx = data["id"]
>     resp_a = template.format(data['prompt'], data['response_a'])
>     resp_b = template.format(data['prompt'], data['response_b'])
>     resp_tokens = tokenizer(
>         [resp_a, resp_b],
>         max_length=args.max_total_length,
>         padding=True,
>         truncation=True,
>         return_tensors="pt",
>     )
>     # concated responses to save inference time -> batch_size =2
>     output = model(resp_tokens)
> 
> ```
> 
> 推論プロセスを高速化するための他の設定をいくつか紹介します。
> 
> モデルの初期化にbf116=Trueを使用します。
> autocast()を使用します。
> 
> 推論を高速化するための他のプロセスはありますか？25000サンプルでテストしましたが、9時間のトレーニング予算を超えるのは非常に危険です。
> 
> 
> 
> > ## yechenzhi1トピック作成者
> > 
> > [https://www.kaggle.com/code/emiz6413/llama-3-8b-38-faster-inference](https://www.kaggle.com/code/emiz6413/llama-3-8b-38-faster-inference)  このノートブックが役立つかどうか確認できます。
> > 
> > 
> > 
---
> ## Valentin Werner
> 
> 一つだけ注意ですが、テストデータは25000サンプルなので、実行時間が10倍になります。技術的には540分未満ですが、かなり遅いです。
> 
> 
> 
> > ## yechenzhi1トピック作成者
> > 
> > はい、そのため予測時間は40 * 10分、つまり約7時間なので、タイムアウトするはずはありません。
> > 
> > 
> > 
---
> ## Rich Olson
> 
> 予測に何行テストしていますか？
> 
> (スコアを計算する場合、25,000行に対して計算されます)
> 
> 
> 
> > ## yechenzhi1トピック作成者
> > 
> > 2500行テストしました。約40分かかりました。
> > 
> > 
> > 
> > > ## Rich Olson
> > > 
> > > うーん、明らかなものは思いつきません。推論の前に時間がかかる処理（トレーニング/前処理/埋め込みの生成）はしていないですよね？
> > > 
> > > アイデアが尽きたら、提出にできるだけ近いワークフローをテストしてみてください。
> > > 
> > > "train"から25k行を"test"データフレームにロードし（列を削除したりして、テストのようにします）、
> > > 
> > > ノートブックのバージョンを保存します。これにより、提出されたときと同じように実行されます。
> > > 
> > > ログを確認できます（最後まで完了する前にタイムアウトした場合でも）。
> > > 
> > > ログ/デバッグステートメントを追加してから実行してみてください。
> > > 
> > > 
> > > 
---



</div>