# 要約 
ディスカッションでは、A. John Callegari Jr.がKaggleの最新Dockerイメージを取得しようとしたが、アクセス拒否に遭ったことを報告しています。彼は「docker pull gcr.io/kaggle-gpu-images/python:latest」コマンドを使用してみましたが、成功しませんでした。他のユーザーであるMelindaが「gcloud auth configure-docker gcr.io」コマンドの実行を提案しましたが、ジョンはその手順や他のGoogle Cloud CLIの手順も試した結果、依然としてアクセスが拒否されたと述べています。また、彼はKaggleノートブックのアップグレードの過程で課金プランのgcloudアカウントを作成することでプルコマンドが成功した経験も共有し、GoogleがCLI認証に影響を与える可能性があることを示唆しています。

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

# kaggle docker

**A. John Callegari Jr.** *Wed Jun 19 2024 01:07:43 GMT+0900 (日本標準時)* (0 votes)

I'm trying to pull the latest kaggle docker image using "docker pull gcr.io/kaggle-gpu-images/python:latest" but permission is denied.  How can I obtain access to the up-to-date kaggle dockers on Google Container Registry?  

thanks,

John



---

 # Comments from other users

> ## Melinda
> 
> Did you already try doing gcloud auth configure-docker gcr.io first?
> 
> 
> 
> > ## A. John Callegari Jr.Topic Author
> > 
> > Yes, I had executed that command and the other google-cloud-cli formulas listed on the GCR website but I still ran into permission denied.  I did get the pull command to work after following the link to upgrade my Kaggle notebook to a google notebook and in the process creating a pay tier gcloud account (without spending any money on Google).  Google may require you to associate your gcloud account with a payment method (apart from your general gsuite payment method) in order for your account login to pass cli authentication to work for the docker pull
> > 
> > 
> > 


---



</div>
<div class="column-right">

# 日本語訳

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


</div>