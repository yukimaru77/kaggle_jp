# 要約 
ディスカッションでは、新しくKaggleに参加したユーザーがオンライン評価で使用されるパッケージについて質問し、新しいパッケージをどのように追加できるかを尋ねています。具体的には、カスタムPythonパッケージを提出時に追加できるかどうか、tarファイルとrequirements.txtの扱いについての助言を求めています。

他のユーザーからは、pipを使ってカスタムパッケージを指定のディレクトリにインストールする方法が提案され、main.pyファイルをそのディレクトリ内に配置することを指示されます。また、main.py内でシステムパスを適切に設定する必要があることも説明されています。最後に、コードの具体例と提出方法についての参照が提供されます。参加者は、提供された情報をもとに理解を深めた様子です。

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

# How to add custom python packages in the submission?

**sakura** *Tue Jun 04 2024 21:04:34 GMT+0900 (日本標準時)* (2 votes)

Hi, all. I'm a new hand to Kaggle. I want to know how can I know what packages are in the online evaluation, and whether I can add new packages (for example, from pip install). It seems that this can be done through submitting a notebook. I'm wondering if I can add custom packages through submitting the tar file? (Such as adding an requirements.txt?). Thanks for any help and response!



---

 # Comments from other users

> ## VolodymyrBilyachat
> 
> pip install -q -U -t /kaggle/working/submission/lib your package
> 
> I was using this
> 
> 
> 
> > ## sakuraTopic Author
> > 
> > Hi, thanks for your response! But if I need to submit a main.py file, where should I put this line in?😀
> > 
> > 
> > 
> > > ## Chris Deotte
> > > 
> > > Hi. Put your main.py file in /kaggle/working/submission/lib and pip install everything into /kaggle/working/submission/lib. Then finally tarball the entire folder /kaggle/working/submission/lib. Afterward submit the tarball to the competition.
> > > 
> > > Also note that inside your main.py file you will need to add to system path so that it can find your pip installs:
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
> > > To see an example of tarballing, see code cell #3 and #4 in starter notebook [here](https://www.kaggle.com/code/ryanholbrook/llm-20-questions-starter-notebook). Afterward we submit submission.tar.gz to the competition.
> > > 
> > > 
> > > 
> > > ## sakuraTopic Author
> > > 
> > > I understand now. Thanks a lot!
> > > 
> > > 
> > > 


---



</div>
<div class="column-right">

# 日本語訳

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


</div>