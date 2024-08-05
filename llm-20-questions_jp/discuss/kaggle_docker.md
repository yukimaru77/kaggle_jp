# kaggle docker
**A. John Callegari Jr.** *2024年6月19日(水) 01:07:43 GMT+0900 (日本標準時)* (0票)
最新のKaggle Dockerイメージを「docker pull gcr.io/kaggle-gpu-images/python:latest」を使って取得しようとしていますが、アクセスが拒否されました。Google Container Registryで最新のKaggle Dockerにアクセスする方法はありますか？
よろしくお願いします。
ジョン

---
 # 他のユーザーからのコメント
> ## Melinda
> 
> まずは「gcloud auth configure-docker gcr.io」を実行してみましたか？

> 
> > ## A. John Callegari Jr. (トピック作成者)
> > 
> > はい、そのコマンドを実行し、GCRのウェブサイトに記載されている他のgoogle-cloud-cliの手順も試しましたが、やはりアクセス拒否に遭いました。KaggleのノートブックをGoogleノートブックにアップグレードして、その過程で課金プランのgcloudアカウントを作成することで、プルコマンドが成功したことがあります（お金は使っていません）。Googleは、gcloudアカウントを支払い方法に関連付けることを要求するかもしれません（一般のG Suiteの支払い方法とは別に）、その結果、CLI認証がDockerのプルに通るようになるのかもしれません。 
> > 
> > > 
