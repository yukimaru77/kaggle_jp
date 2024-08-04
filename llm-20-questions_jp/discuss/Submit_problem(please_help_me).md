# 提出に関する問題（助けてください）
**tiny wood** *2024年7月5日 金曜日 09:43:09 GMT+0900 (日本標準時)* (1票)
このコンペティション初心者です。
ノートブックを提出しようとしましたが、ずっと「検証エピソードが失敗しました（エラー）」と表示されます。
失敗後のログも確認しようとしましたが、ログは空です。
何が問題でしょうか？
---
# 他のユーザーからのコメント
> ## davide
> 
> 私も同じ問題に遭遇しており、私のコードやエージェントの動作とは関係ないように思えます。
> 
> これは、エージェントの1つから見られるログです。
> 
> [[{"duration": 0.002077, "stdout": "", "stderr": "Traceback (most recent call last):\n  File \"/opt/conda/lib/python3.10/site-packages/kaggle_environments/agent.py\", line 43, in get_last_callable\n    code_object = compile(raw, path, \"exec\")\n  File \"/kaggle_simulations/agent/main.py\", line 1\n    include the main.py code under this for submission\n            ^^^\nSyntaxError: invalid syntax\n\nDuring handling of the above exception, another exception occurred:\n\nTraceback (most recent call last):\n  File \"/opt/conda/lib/python3.10/site-packages/kaggle_environments/agent.py\", line 159, in act\n    action = self.agent(*args)\n  File \"/opt/conda/lib/python3.10/site-packages/kaggle_environments/agent.py\", line 125, in callable_agent\n    agent = get_last_callable(raw_agent, path=raw) or raw_agent\n  File \"/opt/conda/lib/python3.10/site-packages/kaggle_environments/agent.py\", line 64, in get_last_callable\n    raise InvalidArgument(\"Invalid raw Python: \" + repr(e))\nkaggle_environments.errors.InvalidArgument: Invalid raw Python: SyntaxError('invalid syntax', ('/kaggle_simulatio"}]]
> 
> もしかしたら誰かが助けてくれるかもしれません。[@bovard](https://www.kaggle.com/bovard) 
> 
> 
> 
---
> ## OminousDude
> 
> ログはエージェント0とエージェント1の2つあります。両方を確認しましたか？
> 
> 
> 
---
> ## Code Hacker
> 
> 私も… 助けてください…
> 
> 
> 
> > ## Krens
> > 
> > 以前「検証エピソードが失敗しました（エラー）」というエラーに遭遇したのは、デバッグ中に「はい」と「いいえ」の回答に対する制限を解除したため、提出時にエージェントが他の回答をした際にエラーが発生したためです。また、実行タイムアウト、文字数制限の超過などにも注意する必要があります。
> > 
> > 
> > 
---

