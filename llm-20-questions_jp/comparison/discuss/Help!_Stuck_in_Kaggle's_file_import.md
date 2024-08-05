# 要約 
**ディスカッション要約:**
ユーザーのAndres H. Zapkeが、Kaggleのノートブックを用いて「20の質問」コンペティション用のエージェントを作成する際のファイル構造について問題を報告しています。彼は、`main.py`がサブミッションフォルダー内にあり、以前は問題なく動作していたが、`gemma`モジュールのメソッドをインポートする際にエラーが発生していると述べています。具体的には、`No module named 'gemma.config'`というエラーが出ているとのことで、`sys.path.insert`を用いてライブラリのパスを追加しようとしたものの、インポートに成功していないようです。彼は、`__init__.py`ファイルが確認済みであることを強調し、インポートの解決策を求めています。

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

# Help! Stuck in Kaggle's file import

**Andres H. Zapke** *Fri Jun 07 2024 18:40:39 GMT+0900 (日本標準時)* (1 votes)

Following the tutorial, I have a notebook and the following file structure (see Image).  This graphical interface is a bit misleading, main.py is inside of submission folder, not inside the lib folder.

So I run the game from my Kaggle notebook with game_output = env.run(agents=[simple_agent, simple_agent, simple_agent , "/kaggle/working/submission/main.py"]) and everything works until now.

However now "main.py" needs some methods of the "gemma" module. I tried importing them with sys.path.insert(0, "/kaggle/working/submission/lib")
    sys.path.insert(0, "./lib") and from gemma.config import * but I always get: "No module named 'gemma.config'".

I confirmed that gemma has an "init.py" file and I can't figure out how to import its methods into my main. Any tips appreciated!!

[Captura de pantalla 2024-06-07 a las 11.34.58.png](https://storage.googleapis.com/kaggle-forum-message-attachments/2859842/20789/Captura de pantalla 2024-06-07 a las 11.34.58.png)



</div>
<div class="column-right">

# 日本語訳

> **Andres H. Zapke** *2024年6月7日（金）18:40:39 日本標準時* (1票)  
> チュートリアルに従ってノートブックを作成し、以下のファイル構造にしています（画像参照）。このグラフィカルインターフェースは少し誤解を招くところがあり、main.pyはlibフォルダーの中ではなく、submissionフォルダーの中にあります。  
> そのため、Kaggleのノートブックからゲームを実行する際に、game_output = env.run(agents=[simple_agent, simple_agent, simple_agent, "/kaggle/working/submission/main.py"])とすると、これまでは問題なく動作していました。しかし、今度は「main.py」が「gemma」モジュールのいくつかのメソッドを必要としています。sys.path.insert(0, "/kaggle/working/submission/lib")やsys.path.insert(0, "./lib")を使用してインポートしようとしたのですが、from gemma.config import *とすると「No module named 'gemma.config'」というエラーが出ます。gemmaには__init__.pyファイルがあることを確認したのですが、main.pyにそのメソッドをインポートする方法が分かりません。何かアドバイスをいただけると嬉しいです！


</div>