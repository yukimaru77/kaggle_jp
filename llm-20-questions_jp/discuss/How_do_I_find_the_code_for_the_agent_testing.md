# エージェントのテストコードを見つける方法

**OminousDude** *2024年7月4日 09:07:24 (日本標準時)* (0票)

自分のローカルマシンで "submission.tar.gz" ファイルからモデルをロードしようとしています。モデル/agent_fn を取得してテストするにはどうすればよいですか？ご協力よろしくお願いいたします。

---
# 他のユーザーからのコメント

> ## Melinda
> 
> Kaggle 環境をローカルマシンで実行したいということですか？それとも何か別のことをしようとしていますか？いずれにしても、これが私のローカルでの実行方法です。もしかしたら、ここで探しているものがあるかもしれません。これは、submission.tar.gz が ./submission/lib に main.py があるフォルダに展開されていることを前提としています（[https://www.kaggle.com/code/rturley/run-debug-llm-20-questions-in-a-notebook](https://www.kaggle.com/code/rturley/run-debug-llm-20-questions-in-a-notebook) から改変）。
> 
> ```python
> # これらは単なるダミーエージェントなので、エージェントの 4 つのバージョンを実行していません。
> def simple_agent1(obs, cfg):
>     # エージェントが推測者で turnType が "ask" の場合
>     if obs.turnType == "ask": response = "Is it a duck?"
>     elif obs.turnType == "guess": response = "duck"
>     elif obs.turnType == "answer": response = "no"
>     return response
> 
> def simple_agent2(obs, cfg):
>     # エージェントが推測者で turnType が "ask" の場合
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
> また、私の main.py には、環境変数に基づいてマシンで実行されているかどうかを確認するコードがあり、実行されている場合は、正しい相対パスからモデルをロードし、マシンに適したデバイスタイプを設定します。
> 
> 
> 
> > ## OminousDudeTopic Author
> > 
> > ありがとうございます。これでうまくいくと思います。ありがとうございます！
> > 
> > 
> > 
---

