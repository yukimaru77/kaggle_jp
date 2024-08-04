# どのようにzipファイルで提出すればいいですか？
**sakura** *2024年6月6日 木曜日 17:26:32 JST* (0票)
皆さん、こんにちは。エージェントをzipファイルで提出したいのですが、ファイル構造は以下のようになっています。
```
├── lib
├── main.py
├── models
```
kaggle competitions submit -c llm-20-questions -f submission.zip -m "debug-file-upload" でアップロードしましたが、エージェントチェックに失敗し、agent-1とagent-2のログはどちらも空で、リプレイもありません。どうやらmain.pyを間違った場所に置いているようです。
このzipファイルはアップロード後どのように処理されるのでしょうか？どこに置かれ、どのように解凍されるのでしょうか？zipファイルにsubmission/サブディレクトリを含める必要がありますか？
---
# 他のユーザーからのコメント
> ## Chris Deotte
> 
> 提出時に、zipファイルは"/kaggle_simulations/agent/"フォルダに解凍されますので、コードがモデルを見つけられるように、このフォルダをシステムパスに追加する必要があります。main.pyの先頭に以下のコードを追加してください。
> 
> ```
> KAGGLE_AGENT_PATH = "/kaggle_simulations/agent/"
> if os.path.exists(KAGGLE_AGENT_PATH):
>     sys.path.insert(0, os.path.join(KAGGLE_AGENT_PATH, 'lib'))
> else:
>     sys.path.insert(0, "/kaggle/working/submission/lib")
> 
> ```
> 
> 
> 
> > ## sakuraTopic Author
> > 
> > ご回答ありがとうございます！このことは知っていて、実際このようなコードがあります。さらに、スターターノートブックにmain.pyをすべてコピーして対応する位置に貼り付け、ノートブックを提出すると、正常に提出できます。しかし、なぜかzipファイルをアップロードすると動作しません（エラーメッセージも表示されません）。
> > 
> > 
> > 
> > > ## Chris Deotte
> > > 
> > > では、別のエラーがあるかもしれません。
> > > 
> > > ボットが自分自身と対戦する検証ゲームでコードが失敗した場合、ログをダウンロードするボタンがあります。ログをダウンロードすると、具体的なエラーメッセージが表示されます。
> > > 
> > > また、main.pyファイル内にprint文を使用してデバッグ情報を表示することもできます。これらのprint文はログに表示されます。
> > > 
> > > 
> > > 
---
> ## Bovard Doerschuk-Tiberi
> 
> zipではなくtar.gzを試してみませんか？
> 
> 
> 
---
> ## sakuraTopic Author
> 
> 更新：これはunzipコマンドを使用した私の構造です。
> 
> ```
> unzip -l example.zip | awk -F/ 'NF<=3'
> 
> ```
> 
> 
> 
---

