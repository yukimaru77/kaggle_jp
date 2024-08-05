# 要約 
このディスカッションは、KaggleのLlama 3アクセスの遅延に関するものです。ユーザーAllie K.は、Metaのウェブサイトではすぐにアクセス権を取得できたのに対し、Kaggleでのアクセスリクエストが6日間以上審査待ちの状態だったと報告しています。他のユーザーも同様の経験をしていることが明らかになり、コンペティションの公平性に疑問が生じています。

ユーザーRBは、Huggingfaceからモデルの重みをダウンロードしてKaggleにプライベートデータセットとしてアップロードする方法を提案しています。これは、Kaggleのアクセスリクエストが遅延している場合の回避策として役立ちます。

ディスカッションの最後には、Allie K.は、KaggleチームがLlama 3アクセスパイプラインを迅速に復旧してくれることを期待していると述べています。

要約すると、このディスカッションは、KaggleのLlama 3アクセスリクエストの遅延と、それがコンペティションの公平性に与える影響について議論しています。ユーザーは、問題を解決するための回避策を提案し、Kaggleチームに迅速な対応を求めています。


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

# Request for Kaggle Llama 3 access under review for over 6 days [Solved]

**Allie K.** *Mon Jul 08 2024 20:18:16 GMT+0900 (日本標準時)* (5 votes)

On Friday early morning MDT I submitted request for Llama 3 and Llama 2 access first via Meta website (of course with the same email address as I have on Kaggle) and I was granted the access in a minute.

Immediately I successfully submitted request to access Llama 3 model via Kaggle. 

Now, after more than 6 days, the request is still "pending a review from the authors".

As it can be seen from the discussion under the model, I am not alone in this desperate situation.

[@addisonhoward](https://www.kaggle.com/addisonhoward) is the access to the model on Kaggle somehow restricted? 

In this case all the competition wouldn't be fair at all. It isn't fair even now, because I couldn't make submission with Llama 3 for 3 days due to problems on Kaggle side.  

Edited:

And suddenly, after "only" 6 days a magic happened and the access is granted.

The magic seems to be triggered by another discussion thread.



---

 # Comments from other users

> ## CPMP
> 
> Reading this only now. It is wrong that your post did not have effect until mine. 
> 
> 
> 


---

> ## RB
> 
> I downloaded Transformer weights for Gemma (since they are not [yet available on Kaggle](https://www.kaggle.com/models/google/gemma-2/discussion/516164)) You can do the same for Llama as well 
> 
> Following code will save weights in /kaggle/working directory of your kernel. You do need read access token from Huggingface and your request must be approved there.
> 
> Typically I found process is much faster when the models are released, so apply even if you are not planning to use it. 
> 
> ```
> import os
> os.environ["HF_HUB_ENABLE_HF_TRANSFER"] = "1"
> 
> from kaggle_secrets import UserSecretsClient
> user_secrets = UserSecretsClient()
> secret_value_0 = user_secrets.get_secret("HF_TOKEN")
> 
> from huggingface_hub import  snapshot_download, login
> login(token=secret_value_0, add_to_git_credential=False)
> 
> ## Download model from HuggingfaceHub
> ## https://huggingface.co/google/gemma-2-9b-it/tree/main
> 
> snapshot_download(repo_id="google/gemma-2-9b-it", 
>                   revision="main", 
>                   repo_type="model",
>                   allow_patterns="*",
>                   local_dir = "/kaggle/working/", 
>                   ignore_patterns="consolidated.safetensors")
> 
> ```
> 
> 
> 
> > ## BladeRunner
> > 
> > This approach seems to only support models with weight files under 20GB, because of the capacity cap of /kaggle/working/, I wonder how it should be handled for models 13b and above?😀
> > 
> > 
> > 
> > > ## RB
> > > 
> > > You can download in /tmp directory - I think there's 50+ GB space available there. 
> > > 
> > > From /tmp you can upload to a Kaggle Dataset with [Kaggle API  ](https://github.com/Kaggle/kaggle-api/blob/main/docs/README.md#datasets)
> > > 
> > > 
> > > 


---

> ## sayoulala
> 
> [https://www.kaggle.com/datasets/junglebeastds/llama3instruct](https://www.kaggle.com/datasets/junglebeastds/llama3instruct) .Someone upload the model here
> 
> 
> 


---

> ## Allie K.Topic Author
> 
> Big thanks to everybody who suggested me (and hopefully not only to me) a solution how to solve the unpleasant situation. I could start submitting.
> 
> Anyway I hope that Kaggle team will restore the broken Llama 3 access pipeline in a reasonable time, not only after the competition ends. 
> 
> 
> 


---

> ## Pamin
> 
> Same, 3 days ago.
> 
> 
> 


---

> ## hn
> 
> Same here actually. 
> 
> 
> 


---

> ## Valentin Werner
> 
> This is wild, it has been approved for me within 10 minutes on a weekend
> 
> 
> 


---

> ## Xinyuan Qiao
> 
> Just do it again, I got same situation before.
> 
> 
> 


---

> ## Arindam Roy
> 
> Same here 
> 
> 
> 


---

> ## samson
> 
> You can get an access via [meta's webpage](https://llama.meta.com/) or directly on [huggingface](https://huggingface.co/meta-llama/Meta-Llama-3-8B), then download the weights and upload all the stuff as a private dataset on Kaggle. Its much faster! Basically minutes (I have submitted a request for model access via Kaggle 4 days ago and still waiting)
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# Kaggle Llama 3 アクセスリクエストが6日間以上審査中 [解決済み]
**Allie K.** *2024年7月8日月曜日 20:18:16 GMT+0900 (日本標準時)* (5票)

金曜日の早朝MDTに、Metaのウェブサイト（もちろんKaggleと同じメールアドレスで）を通じてLlama 3とLlama 2へのアクセスをリクエストし、1分以内にアクセス権を取得しました。
すぐに、Kaggleを通じてLlama 3モデルへのアクセスリクエストを正常に提出しました。
しかし、6日以上経った今でも、リクエストは「作成者による審査待ち」の状態です。
モデルの下のディスカッションを見ればわかるように、私だけではありません。
[@addisonhoward](https://www.kaggle.com/addisonhoward) Kaggleでのモデルへのアクセスは制限されていますか？
もしそうなら、このコンペティションは全く公平ではありません。Kaggle側の問題でLlama 3を使って提出ができなかったため、すでに3日間公平ではありません。
編集：
そして突然、わずか6日後に魔法が起こり、アクセス権が与えられました。
魔法は、別のディスカッションスレッドによって引き起こされたようです。
---
# 他のユーザーからのコメント
> ## CPMP
> 
> 今になってこの投稿を読みました。私の投稿が効果を発揮するまであなたの投稿が効果を発揮しなかったのは間違っています。
> 
> 
> 
---
> ## RB
> 
> GemmaのTransformerの重みをダウンロードしました（まだKaggleで利用可能ではないため[Kaggleでまだ利用可能ではありません](https://www.kaggle.com/models/google/gemma-2/discussion/516164)）。Llamaでも同じようにできます。
> 
> 以下のコードは、カーネルの/kaggle/workingディレクトリに重みを保存します。Huggingfaceから読み取りアクセス権トークンを取得する必要があり、Huggingfaceでリクエストが承認されている必要があります。
> 
> 通常、モデルがリリースされるとプロセスがはるかに速くなるため、使用しない場合でも申請してください。
> 
> ```
> import os
> os.environ["HF_HUB_ENABLE_HF_TRANSFER"] = "1"
> 
> from kaggle_secrets import UserSecretsClient
> user_secrets = UserSecretsClient()
> secret_value_0 = user_secrets.get_secret("HF_TOKEN")
> 
> from huggingface_hub import  snapshot_download, login
> login(token=secret_value_0, add_to_git_credential=False)
> 
> ## HuggingfaceHubからモデルをダウンロード
> ## https://huggingface.co/google/gemma-2-9b-it/tree/main
> 
> snapshot_download(repo_id="google/gemma-2-9b-it", 
>                   revision="main", 
>                   repo_type="model",
>                   allow_patterns="*",
>                   local_dir = "/kaggle/working/", 
>                   ignore_patterns="consolidated.safetensors")
> 
> ```
> 
> 
> 
> > ## BladeRunner
> > 
> > このアプローチは、/kaggle/working/の容量制限のため、20GB以下の重みファイルを持つモデルのみをサポートしているようです。13b以上のモデルはどうすればいいのか、疑問です。😀
> > 
> > 
> > 
> > > ## RB
> > > 
> > > /tmpディレクトリにダウンロードできます。そこには50GB以上の空き容量があると思います。
> > > 
> > > /tmpから[Kaggle API](https://github.com/Kaggle/kaggle-api/blob/main/docs/README.md#datasets)を使ってKaggleデータセットにアップロードできます。
> > > 
> > > 
> > > 
---
> ## sayoulala
> 
> [https://www.kaggle.com/datasets/junglebeastds/llama3instruct](https://www.kaggle.com/datasets/junglebeastds/llama3instruct) .誰かがここにモデルをアップロードしました。
> 
> 
> 
---
> ## Allie K.トピック作成者
> 
> 不快な状況を解決する方法を提案してくれた皆さんに感謝します（私だけではないことを願っています）。提出を開始できました。
> 
> それでも、Kaggleチームが壊れたLlama 3アクセスパイプラインを、コンペティションが終了した後ではなく、合理的な時間内に復旧してくれることを願っています。
> 
> 
> 
---
> ## Pamin
> 
> 私も同じです。3日前から。
> 
> 
> 
---
> ## hn
> 
> 実は私も同じです。
> 
> 
> 
---
> ## Valentin Werner
> 
> これはすごいですね。週末に10分以内に承認されました。
> 
> 
> 
---
> ## Xinyuan Qiao
> 
> もう一度やってみてください。以前も同じ状況でした。
> 
> 
> 
---
> ## Arindam Roy
> 
> 私も同じです。
> 
> 
> 
---
> ## samson
> 
> [Metaのウェブページ](https://llama.meta.com/)または[Huggingface](https://huggingface.co/meta-llama/Meta-Llama-3-8B)でアクセスを取得し、重みをダウンロードして、Kaggleにプライベートデータセットとしてすべてアップロードできます。はるかに高速です！実際には数分です（4日前にKaggleを通じてモデルアクセスをリクエストしましたが、まだ待っています）。
> 
> 
> 
---



</div>