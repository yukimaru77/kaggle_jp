# Kaggle Docker イメージの取得について

**A. John Callegari Jr.** *水曜日 6月 19日 2024 01:07:43 日本標準時* (0 票)

"docker pull gcr.io/kaggle-gpu-images/python:latest" を使って最新の Kaggle Docker イメージを取得しようとしていますが、アクセス拒否エラーが発生しています。Google Container Registry で最新の Kaggle Docker イメージにアクセスするにはどうすればよいでしょうか？

よろしくお願いします。
John

---
# 他のユーザーからのコメント

> ## Melinda
> 
> まず、`gcloud auth configure-docker gcr.io` を実行してみましたか？
> 
> 
> 
> > ## A. John Callegari Jr.トピック作成者
> > 
> > はい、そのコマンドと GCR ウェブサイトに記載されている他の Google Cloud CLI コマンドを実行しましたが、それでもアクセス拒否エラーが発生しました。Kaggle ノートブックを Google ノートブックにアップグレードし、その過程で有料の Google Cloud アカウントを作成したところ（Google にお金を払うことなく）、Docker イメージの取得に成功しました。Google は、Docker イメージの取得に必要な CLI 認証を通過するために、Google Cloud アカウントに支払い方法（一般的な G Suite 支払い方法とは別に）を関連付ける必要があるかもしれません。
> > 
> > 
> > 
--- 

