# 要約 
ディスカッションでは、ユーザーOminousDudeが自分のモデルをローカルマシンでテストするために、Kaggle環境での実行に関する情報を求めています。彼は「submission.tar.gz」ファイルからモデルをロードしたいと考えていますが、テスト用の「model/agent_fn」をどう取得するかに困っています。

MelindaはOminousDudeの質問に対して、ローカルマシンでの実行方法を説明し、具体的なサンプルコードを提供しています。彼女は、モデルが特定のパスにあることを前提に、ダミーエージェントの実装とKaggle環境のセットアップ方法を示しました。このコードは、異なるターンタイプに基づいて応答を生成するエージェントの例を含んでおり、ローカル環境での動作確認も可能にしています。

OminousDudeはMelindaの助けに感謝しており、提供された情報が役立つと感じていることを伝えています。

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

# How do I find the code for the agent testing?

**OminousDude** *Thu Jul 04 2024 09:07:24 GMT+0900 (日本標準時)* (0 votes)

I am trying to load my model on my local machine from my "submission.tar.gz" file how do I get the model/agent_fn so that I could test it? Thank you in advance for any help!



---

 # Comments from other users

> ## Melinda
> 
> Do you mean you want to run the kaggle env locally on your machine? Or are you trying to do something else? At any rate this is how I run it locally.  Maybe something in here is what you're looking for. It assumes your submission.tar.gz is unzipped in a way that main.py is in a folder ./submission/lib (adapted from [https://www.kaggle.com/code/rturley/run-debug-llm-20-questions-in-a-notebook](https://www.kaggle.com/code/rturley/run-debug-llm-20-questions-in-a-notebook))
> 
> ```
> # These are just dummy agents so that I'm not running 4 versions of my agent.
> def simple_agent1(obs, cfg):
>     # if agent is guesser and turnType is "ask"
>     if obs.turnType == "ask": response = "Is it a duck?"
>     elif obs.turnType == "guess": response = "duck"
>     elif obs.turnType == "answer": response = "no"
>     return response
> 
> def simple_agent2(obs, cfg):
>     # if agent is guesser and turnType is "ask"
>     if obs.turnType == "ask": response = "Is it a bird?"
>     elif obs.turnType == "guess": response = "bird"
>     elif obs.turnType == "answer": response = "no"
>     return response
> 
> from kaggle_environments import make
> import kaggle_environments
> keyword = "argentina"
> alts = ["argentina"]
> kaggle_environments.envs.llm_20_questions.llm_20_questions.category = "Place"
> kaggle_environments.envs.llm_20_questions.llm_20_questions.keyword_obj = {'keyword':keyword,'alts':alts}
> kaggle_environments.envs.llm_20_questions.llm_20_questions.keyword = keyword
> kaggle_environments.envs.llm_20_questions.llm_20_questions.alts = alts
> 
> env = make("llm_20_questions", debug=True)
> game_output = env.run(agents=[simple_agent1, simple_agent2, "./submission/lib/main.py", "./submission/lib/main.py"])
> env.render(mode="ipython", width=800, height=400)
> 
> ```
> 
> I also have some code in my main.py that looks to see if it's running on my machine or not, based on environment variables, and if it is, it loads the model from the right relative path and sets the device type appropriately for my machine.
> 
> 
> 
> > ## OminousDudeTopic Author
> > 
> > Ok thank you I think this should work for me thanks!
> > 
> > 
> > 


---



</div>
<div class="column-right">

# 日本語訳

# エージェントテストのコードを見つけるには？

**OminousDude** *2024年7月4日 Thu 09:07:24 GMT+0900 (日本標準時)* (0票)
私は「submission.tar.gz」ファイルから自分のモデルをローカルマシンにロードしようとしていますが、テストするための model/agent_fn をどのように取得すればいいのでしょうか？ 何か手助けしていただけると幸いです！

---
## 他のユーザーからのコメント
> ## Melinda
> 
> あなたが言いたいのは、Kaggleの環境をローカルマシンで実行したいということですか？それとも別のことをしようとしているのですか？いずれにしても、私は次のようにローカルで実行しています。これがあなたが探しているものに役立つかもしれません。これは、submission.tar.gz が適切に解凍されていて、main.py が ./submission/lib フォルダにあることを前提としています（[https://www.kaggle.com/code/rturley/run-debug-llm-20-questions-in-a-notebook](https://www.kaggle.com/code/rturley/run-debug-llm-20-questions-in-a-notebook) からの適応版です）。
> 
> ```
> # これは単なるダミーエージェントで、私のエージェントの4バージョンを実行しないためのものです。
> def simple_agent1(obs, cfg):
>     # エージェントが推測者でターンタイプが "ask" の場合
>     if obs.turnType == "ask": response = "それはアヒルですか？"
>     elif obs.turnType == "guess": response = "アヒル"
>     elif obs.turnType == "answer": response = "いいえ"
>     return response
> 
> def simple_agent2(obs, cfg):
>     # エージェントが推測者でターンタイプが "ask" の場合
>     if obs.turnType == "ask": response = "それは鳥ですか？"
>     elif obs.turnType == "guess": response = "鳥"
>     elif obs.turnType == "answer": response = "いいえ"
>     return response
> 
> from kaggle_environments import make
> import kaggle_environments
> keyword = "アルゼンチン"
> alts = ["アルゼンチン"]
> kaggle_environments.envs.llm_20_questions.llm_20_questions.category = "場所"
> kaggle_environments.envs.llm_20_questions.llm_20_questions.keyword_obj = {'keyword':keyword,'alts':alts}
> kaggle_environments.envs.llm_20_questions.llm_20_questions.keyword = keyword
> kaggle_environments.envs.llm_20_questions.llm_20_questions.alts = alts
> 
> env = make("llm_20_questions", debug=True)
> game_output = env.run(agents=[simple_agent1, simple_agent2, "./submission/lib/main.py", "./submission/lib/main.py"])
> env.render(mode="ipython", width=800, height=400)
> 
> ```
> 私の main.py の中にも、実行されている環境に基づいて自分のマシンで動いているかどうかを確認し、適切な相対パスからモデルをロードし、マシン用のデバイスタイプを設定するコードがあります。
> 
> > ## OminousDude トピック作成者
> > 
> > ありがとうございます、これでうまくいくと思います！感謝します！


</div>