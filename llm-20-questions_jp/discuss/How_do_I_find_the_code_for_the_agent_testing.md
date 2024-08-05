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
