# 提出に関する問題（助けてください）
**tiny wood** *2024年7月5日 金曜日 09:43:09 GMT+0900（日本標準時）* (1票)
私はこのコンペティションの初心者です。
ノートブックを提出しようとしたのですが、「バリデーションエピソードが失敗しました（エラー）」と表示され続けます。
失敗後のログも読み取ろうとしましたが、ログは空でした。
問題は何でしょうか？
---
 # 他のユーザーからのコメント
> ## davide
> 
> 私も同じ問題に直面しており、自分のコードやエージェントの動作には関係ないようです。
> 
> こちらがエージェントの一つからのログです：
> 
> [[{"duration": 0.002077, "stdout": "", "stderr": "Traceback (most recent call last):\n  File \"/opt/conda/lib/python3.10/site-packages/kaggle_environments/agent.py\", line 43, in get_last_callable\n    code_object = compile(raw, path, \"exec\")\n  File \"/kaggle_simulations/agent/main.py\", line 1\n    include the main.py code under this for submission\n            ^^^\nSyntaxError: invalid syntax\n\nDuring handling of the above exception, another exception occurred:\n\nTraceback (most recent call last):\n  File \"/opt/conda/lib/python3.10/site-packages/kaggle_environments/agent.py\", line 159, in act\n    action = self.agent(*args)\n  File \"/opt/conda/lib/python3.10/site-packages/kaggle_environments/agent.py\", line 125, in callable_agent\n    agent = get_last_callable(raw_agent, path=raw) or raw_agent\n  File \"/opt/conda/lib/python3.10/site-packages/kaggle_environments/agent.py\", line 64, in get_last_callable\n    raise InvalidArgument(\"Invalid raw Python: \" + repr(e))\nkaggle_environments.errors.InvalidArgument: Invalid raw Python: SyntaxError('invalid syntax', ('/kaggle_simulatio"}]]
> 
> 誰か助けてくれませんか？ [@bovard](https://www.kaggle.com/bovard) 
> 
> ---
> ## OminousDude
> 
> エージェントには二つのログがあります：エージェント0とエージェント1。両方を確認しましたか？
> 
> ---
> ## Code Hacker
> 
> 私も同じです…助けてください…
> 
> > ## Krens
> > 
> > 最後に「バリデーションエピソードが失敗しました（エラー）」が発生したのは、デバッグ中に「はい」と「いいえ」の回答制限を取り除いたためで、提出時に他の回答をエージェントがしたときにエラーが発生しました。それに加えて、タイムアウトに注意することや、文字数が制限を超えていないかも確認する必要があります。
> > 
> > 
