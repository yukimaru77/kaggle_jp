# 提出時にカスタムPythonパッケージを追加する方法
**sakura** *2024年6月4日 火曜日 21:04 (日本標準時)* (2票)
皆さん、こんにちは。Kaggleに新しく参加しました。オンライン評価で使用されているパッケージを知る方法と、新しいパッケージ（例えば、pip installから）を追加できるかどうかを教えていただきたいです。ノートブックを提出することでこれが可能なようですが、tarファイルを提出する際にカスタムパッケージを追加できるのでしょうか？（requirements.txtを追加するような形で）。ご助言やご返信いただければ幸いです！

---
 # 他のユーザーからのコメント
> ## VolodymyrBilyachat
> 
> pip install -q -U -t /kaggle/working/submission/lib あなたのパッケージ
> 
> これを使っていました。
> 
> 
> > ## sakuraTopic オーサー
> > 
> > こんにちは、ご返信ありがとうございます！でも、main.pyファイルを提出する必要がある場合、この行はどこに入れるべきですか？😀
> > 
> > > ## Chris Deotte
> > > 
> > > こんにちは。main.pyファイルを/kaggle/working/submission/libに置き、すべてのパッケージを/kaggle/working/submission/libにpipでインストールしてください。最後に、全フォルダー/kaggle/working/submission/libをtarballします。そして、そのtarballをコンペティションに提出します。
> > > 
> > > また、main.pyファイル内で、自分のpipインストールを見つけられるようにシステムパスを追加する必要があります：
> > > 
> > > ```
> > > KAGGLE_AGENT_PATH = "/kaggle_simulations/agent/"
> > > if os.path.exists(KAGGLE_AGENT_PATH):
> > >     sys.path.insert(0, os.path.join(KAGGLE_AGENT_PATH, 'lib'))
> > > else:
> > >     sys.path.insert(0, "/kaggle/working/submission/lib")
> > > 
> > > ```
> > > 
> > > tarballの例については、こちらのスターターノートブックのコードセル#3と#4を参照してください [こちら](https://www.kaggle.com/code/ryanholbrook/llm-20-questions-starter-notebook)。その後、submission.tar.gzをコンペティションに提出します。
> > > 
> > > 
> > > 
> > > ## sakuraTopic オーサー
> > > 
> > > なるほど、理解しました。ありがとうございます！
> > > 
> > > 
