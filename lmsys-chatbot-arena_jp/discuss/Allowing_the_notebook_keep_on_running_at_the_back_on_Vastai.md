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

