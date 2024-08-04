# 要約 
このディスカッションは、KaggleのLlama 3アクセスの遅延に関するものです。ユーザーAllie K.は、Metaのウェブサイトではすぐにアクセス権を取得できたのに対し、Kaggleでのアクセスリクエストが6日間以上審査待ちの状態だったと報告しています。他のユーザーも同様の経験をしていることが明らかになり、コンペティションの公平性に疑問が生じています。

ユーザーRBは、Huggingfaceからモデルの重みをダウンロードしてKaggleにプライベートデータセットとしてアップロードする方法を提案しています。これは、Kaggleのアクセスリクエストが遅延している場合の回避策として役立ちます。

ディスカッションの最後には、Allie K.は、KaggleチームがLlama 3アクセスパイプラインを迅速に復旧してくれることを期待していると述べています。

要約すると、このディスカッションは、KaggleのLlama 3アクセスリクエストの遅延と、それがコンペティションの公平性に与える影響について議論しています。ユーザーは、問題を解決するための回避策を提案し、Kaggleチームに迅速な対応を求めています。


---
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

