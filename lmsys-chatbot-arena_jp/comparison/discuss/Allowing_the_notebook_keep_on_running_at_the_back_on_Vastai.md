# 要約 
このディスカッションは、KaggleユーザーのJamshaidSohailがVast.aiでGemma 2をトレーニングするためのノートブックをブラウザを閉じた後も実行し続ける方法について質問したことから始まりました。

Valentin Wernerは、Vast.aiを使った経験はありませんが、大学サーバーでノートブックをバックグラウンドで実行する方法として、ノートブックをPythonスクリプトに変換し、Linuxコマンドの"screen"を使ってスクリプトを起動してバックグラウンドに移すことを提案しました。

JamshaidSohailは、Valentin Wernerの提案がうまくいったことを報告し、ディスカッションは終了しました。


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

# Allowing the notebook keep on running at the back on Vast.ai

**JamshaidSohail** *Wed Jul 17 2024 00:34:15 GMT+0900 (日本標準時)* (1 votes)

Hi. I have successfully setup my instance on vast.ai for training Gemma 2. My notebook is running. I just want to make sure that it keeps on running even if close the browser. How would that be possible [@kishanvavdara](https://www.kaggle.com/kishanvavdara) [@valentinwerner](https://www.kaggle.com/valentinwerner).



---

 # Comments from other users

> ## Valentin Werner
> 
> How did I get to the point where I am directly tagged in open discussion questions? 😉
> 
> I have never used vast.ai, but what I did back when I had a university server with 4xV100 at my disposal:
> 
> - you should probably put your notebooks into a python script (train.py for example)
> 
> - you should start the scrip and move it to the background. I always used the linux command "screen" for this. Make sure to detach your screen before you close the browser and make sure the server keeps running (again, I never used vast.ai)..
> 
> ChatGPT should be able to give you more details, there are also plenty of documentations online
> 
> 
> 
> > ## JamshaidSohailTopic Author
> > 
> > Thank you so much. It works :D [@valentinwerner](https://www.kaggle.com/valentinwerner) 
> > 
> > 
> > 


---



</div>
<div class="column-right">

# 日本語訳

# Vast.ai でノートブックをバックグラウンドで実行し続ける方法

**JamshaidSohail** *2024年7月17日 水曜日 00:34:15 GMT+0900 (日本標準時)* (1票)

こんにちは。Vast.ai に Gemma 2 をトレーニングするためのインスタンスを正常にセットアップしました。ノートブックは実行中です。ブラウザを閉じても実行し続けられるようにしたいのですが、どうすればいいでしょうか？ [@kishanvavdara](https://www.kaggle.com/kishanvavdara) [@valentinwerner](https://www.kaggle.com/valentinwerner)

---
# 他のユーザーからのコメント

> ## Valentin Werner
> 
> どうして私がオープンなディスカッションの質問で直接タグ付けされているのでしょうか？😉
> 
> 私は Vast.ai を使ったことがありませんが、4xV100 を搭載した大学サーバーを使っていた頃には、次のようなことをしていました。
> 
> - ノートブックを Python スクリプト（例えば train.py）に入れるべきです。
> 
> - スクリプトを起動してバックグラウンドに移す必要があります。私はいつも Linux コマンドの "screen" を使用していました。ブラウザを閉じる前に screen をデタッチし、サーバーが実行し続けるようにしてください（繰り返しますが、私は Vast.ai を使ったことがありません）。
> 
> ChatGPT は詳細を教えてくれるはずです。オンラインにもたくさんのドキュメントがあります。
> 
> 
> 
> > ## JamshaidSohail トピック作成者
> > 
> > ありがとうございます。うまくいきました！:D [@valentinwerner](https://www.kaggle.com/valentinwerner) 
> > 
> > 
> > 
---



</div>