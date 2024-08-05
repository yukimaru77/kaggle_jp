# Zipファイルの提出方法について
**sakura** *2024年6月6日(木) 17:26:32 GMT+0900 (日本標準時)* (0票)
皆さん、こんにちは。エージェントをzipファイルで提出したいのですが、私のファイル構造は以下の通りです：
```
├── lib
├── main.py
├── models
```
私は次のコマンドで提出しました：
```
kaggle competitions submit -c llm-20-questions -f submission.zip -m "debug-file-upload"
```
しかし、エージェントチェックに失敗し、エージェント1と2のログはどちらも空で、返信もありません。どうやらmain.pyを間違った場所に置いたようです。
アップロード後、このzipファイルはどのように処理されるのか、どこに配置され、どのように解凍されるのか気になります。zipファイルにsubmission/サブディレクトリを含める必要があるのでしょうか？

---
# 他のユーザーからのコメント
> ## Chris Deotte
> 
> 提出時に、あなたのzipファイルは「/kaggle_simulations/agent/」フォルダに解凍されるので、コードがモデルを見つけられるように、これをシステムパスに追加する必要があります。main.pyの最初に以下のコードを追加してください：
> 
> ```python
> KAGGLE_AGENT_PATH = "/kaggle_simulations/agent/"
> if os.path.exists(KAGGLE_AGENT_PATH):
>     sys.path.insert(0, os.path.join(KAGGLE_AGENT_PATH, 'lib'))
> else:
>     sys.path.insert(0, "/kaggle/working/submission/lib")
> ```
> 
> 
> > ## sakuraTopic 著者
> > 
> > ご返信ありがとうございます！このことは知っており、確かにこのようなコードを書いています。さらに、スターターノートブックでmain.pyのすべてをコピーし、スターターノートブックの対応する位置に貼り付けて提出すると成功します。しかし、なぜかzipファイルをアップロードするとうまくいかず（エラーメッセージなし）、困っています。
> > 
> > 
> > > ## Chris Deotte
> > > 
> > > それなら、別のエラーがあるかもしれませんね。
> > > 
> > > あなたのコードがバリデーションゲーム（あなたのボットが自分のボットと対戦する）に失敗した場合、ログをダウンロードするボタンがあります。ログをダウンロードすれば、特定のエラーメッセージが見られます。
> > > 
> > > また、main.pyファイル内にprint文を使用してデバッグ情報を印刷することもできます。これらのprint文はログに表示されます。
> > > 
> > > 
---
> ## Bovard Doerschuk-Tiberi
> 
> zipの代わりにtar.gzを試してみてもいいですか？
> 
> ---
> ## sakuraTopic 著者
> > 更新：unzipコマンドを使用した時の構造は以下の通りです：
> > 
> ```bash
> unzip -l example.zip | awk -F/ 'NF<=3'
> ```
> > 
> ---
