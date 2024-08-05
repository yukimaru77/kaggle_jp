# 要約 
ディスカッションでは、Kaggle環境で最新のtransformersライブラリ（バージョン4.42.4）をインストールしたにもかかわらず、本番環境で自動的に古いバージョン（4.41.2）にダウングレードされてしまう問題について話し合われています。ユーザーの**TomFuj**がこの問題を最初に提起し、他の参加者も同様の問題を経験していると報告しています。

**Mitsutani**と**JacobStein**は、インストールした新しいバージョンが優先されず、古いバージョンが使用されてしまうことに困惑しています。一方、**Chris Deotte**は、Kaggleでのパッケージインストール方法に関する参考リンクを提供し、解決策を探る手助けを試みています。しかし、**Mitsutani**はその提案を試行したものの、古いバージョンが読み込まれる問題は解決されていないと述べています。

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

# How can I use the latest version of the transformers library in the production environment?

**TomFuj** *Fri Jul 19 2024 01:04:06 GMT+0900 (日本標準時)* (2 votes)

Dear Kaggle Staff

The latest transformers library (ver 4.42.4) installed via pip in the Kaggle environment is being downgraded to ver 4.41.2 in the production environment and is not being reflected properly.

Could you please advise on the best way to use the latest transformers library in the production environment ?



---

 # Comments from other users

> ## Mitsutani
> 
> I'm having the same issue. Following to see if anyone has suggestions
> 
> 
> 


---

> ## JacobStein
> 
> Our team is experiencing the same issue. The old version of the transformers library is taking precedence over the newer one we installed during the build.
> 
> 
> 


---

> ## Chris Deotte
> 
> You can view my starter notebook to learn how to pip install packages to be used during submission [here](https://www.kaggle.com/code/cdeotte/starter-code-for-llama-8b-llm-lb-0-750)
> 
> 
> 
> > ## Mitsutani
> > 
> > I've tried using this setup but I'm running Gemma 2. I followed the same steps as in the notebook (changing sys.path etc), but when importing transformers in the production environment I get the older version too so it can't load Gemma 2. I think your main doesn't need transformers 4.42.4 so it runs fine, but correct me if I'm wrong.
> > 
> > 
> > 


---



</div>
<div class="column-right">

# 日本語訳

# 最新のtransformersライブラリを本番環境で使用するにはどうすれば良いですか？
**TomFuj** *2024年7月19日 01:04:06 JST* (2票)
Kaggleスタッフの皆様へ、
Kaggle環境でpipを使ってインストールした最新のtransformersライブラリ（バージョン4.42.4）が、本番環境ではバージョン4.41.2にダウングレードされ、正しく反映されていません。
最新のtransformersライブラリを本番環境で使用するための最良の方法についてアドバイスをいただけますか？

---
# 他のユーザーからのコメント
> ## Mitsutani
> 
> 私も同じ問題に直面しています。どなたか提案があれば教えてください。

---
> ## JacobStein
> 
> 私たちのチームも同じ問題を経験しています。インストールした新しいバージョンのtransformersライブラリよりも古いバージョンが優先されてしまっています。

---
> ## Chris Deotte
> 
> こちらのスタート用ノートブックを参考にして、提出時に使用するためのパッケージのpipインストール方法を学んでください [こちら](https://www.kaggle.com/code/cdeotte/starter-code-for-llama-8b-llm-lb-0-750) からご覧いただけます。

> > ## Mitsutani
> > 
> > このセットアップを試してみましたが、Gemma 2を使用しています。ノートブックに従ってsys.pathなどを変更したのですが、本番環境でtransformersをインポートすると古いバージョンが読み込まれてしまい、Gemma 2を読み込めません。あなたのメインファイルにはtransformers 4.42.4は必要ないと思うので正常に動作するのでしょうけれど、間違っていたら教えてください。
> > 
> > 


</div>