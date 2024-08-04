# カスタム Python パッケージを提出物に追加する方法

**sakura** *2024年6月4日 火曜日 21:04:34 JST* (2 votes)
皆さん、こんにちは。Kaggle初心者です。オンライン評価でどのようなパッケージが使用できるのか、また新しいパッケージ（例えば、pip installから）を追加できるのか知りたいです。これはノートブックを提出することでできるようですが、tarファイルで提出することでカスタムパッケージを追加できるのでしょうか？（例えば、requirements.txtを追加するなど）。ご回答よろしくお願いいたします！

---
# 他のユーザーからのコメント
> ## VolodymyrBilyachat
> 
> pip install -q -U -t /kaggle/working/submission/lib your package
> 
> 私はこれを使用していました。
> 
> 
> 
> > ## sakuraTopic Author
> > 
> > こんにちは、ご回答ありがとうございます！しかし、main.pyファイルを提出する必要がある場合、この行はどこに置くべきでしょうか？😀
> > 
> > 
> > 
> > > ## Chris Deotte
> > > 
> > > こんにちは。main.pyファイルを/kaggle/working/submission/libに置き、pip installで必要なものをすべて/kaggle/working/submission/libにインストールしてください。最後に、/kaggle/working/submission/libフォルダ全体をtarball化します。その後、tarballをコンペティションに提出してください。
> > > 
> > > また、main.pyファイル内で、pipでインストールしたものを探せるようにシステムパスに追加する必要があります。
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
> > > tarball化の例については、スターターノートブックのコードセル#3と#4をご覧ください [こちら](https://www.kaggle.com/code/ryanholbrook/llm-20-questions-starter-notebook)。その後、submission.tar.gzをコンペティションに提出します。
> > > 
> > > 
> > > 
> > > ## sakuraTopic Author
> > > 
> > > わかりました。ありがとうございます！
> > > 
> > > 
> > > 
---

