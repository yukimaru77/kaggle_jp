# スコアに関する質問

**CchristoC** *2024年7月6日土曜日 01:32:10 日本標準時* (0票)

スコア結果の [ ] 内にある名前以外の "Err"、"1st"、"3rd" はどういう意味ですか？

私のエージェントの1つで、"Err" は -184 と -95 を示しています。

この [3rd] は -118 を示し、その後別の [Err] が -118 を示します。

一方、この試合では、単に -5 を示しています。

これらは一体何を意味するのでしょうか？

"Err" のエージェントログ:

[[{"duration": 44.487901, "stdout": "", "stderr": "\rLoading checkpoint shards:   0%|          | 0/4 [00:00<?, ?it/s]\rLoading checkpoint shards:  25%|##5       | 1/4 [00:01<00:05,  1.72s/it]\rLoading checkpoint shards:  50%|#####     | 2/4 [00:03<00:03,  1.69s/it]\rLoading checkpoint shards:  75%|#######5  | 3/4 [00:09<00:03,  3.58s/it]\rLoading checkpoint shards: 100%|##########| 4/4 [00:09<00:00,  2.33s/it]\n"}],
 [{"duration": 13.157402, "stdout": "", "stderr": ""}],
 [{"duration": 16.281109, "stdout": "", "stderr": ""}],
 [{"duration": 12.956681, "stdout": "", "stderr": ""}],
 [{"duration": 16.44063, "stdout": "", "stderr": ""}],
 [{"duration": 13.028765, "stdout": "", "stderr": ""}],
 [{"duration": 16.632452, "stdout": "", "stderr": ""}],
 [{"duration": 13.089482, "stdout": "", "stderr": ""}],
 [{"duration": 17.155518, "stdout": "", "stderr": ""}],
 [{"duration": 13.45727, "stdout": "", "stderr": ""}],
 [{"duration": 17.283259, "stdout": "", "stderr": ""}],
 [{"duration": 13.368639, "stdout": "", "stderr": ""}],
 [{"duration": 17.24138, "stdout": "", "stderr": ""}],
 [{"duration": 13.452842, "stdout": "", "stderr": ""}],
 [{"duration": 17.626067, "stdout": "", "stderr": ""}],
 [{"duration": 13.794647, "stdout": "", "stderr": ""}],
 [{"duration": 17.637258, "stdout": "", "stderr": ""}],
 [{"duration": 13.83658, "stdout": "", "stderr": ""}],
 [{"duration": 17.712688, "stdout": "", "stderr": ""}],
 [{"duration": 13.759209, "stdout": "", "stderr": ""}],
 [{"duration": 18.127925, "stdout": "", "stderr": ""}],
 [{"duration": 13.800963, "stdout": "", "stderr": ""}],
 [{"duration": 18.1417, "stdout": "", "stderr": ""}],
 [{"duration": 14.120216, "stdout": "", "stderr": ""}],
 [{"duration": 18.17651, "stdout": "", "stderr": ""}],
 [{"duration": 14.179938, "stdout": "", "stderr": ""}],
 [{"duration": 18.513849, "stdout": "", "stderr": ""}],
 [{"duration": 14.198519, "stdout": "", "stderr": ""}],
 [{"duration": 18.581085, "stdout": "", "stderr": ""}],
 [{"duration": 14.242732, "stdout": "", "stderr": ""}],
 [{"duration": 18.963667, "stdout": "", "stderr": ""}],
 [{"duration": 14.60338, "stdout": "", "stderr": ""}],
 [{"duration": 19.000409, "stdout": "", "stderr": ""}],
 [{"duration": 14.624762, "stdout": "", "stderr": ""}],
 [{"duration": 19.019398, "stdout": "", "stderr": ""}],
 [{"duration": 14.982776, "stdout": "", "stderr": ""}],
 [{"duration": 19.442042, "stdout": "", "stderr": ""}],
 [{"duration": 15.000276, "stdout": "", "stderr": ""}],
 [{"duration": 9.141473, "stdout": "", "stderr": "Traceback (most recent call last):\n  File \"/opt/conda/lib/python3.10/site-packages/kaggle_environments/agent.py\", line 159, in act\n    action = self.agent(*args)\n  File \"/opt/conda/lib/python3.10/site-packages/kaggle_environments/agent.py\", line 130, in callable_agent\n    agent(*args) \\\n  File \"/kaggle_simulations/agent/main.py\", line 193, in agent\n    response = robot.on(mode = \"asking\", obs = obs)\n  File \"/kaggle_simulations/agent/main.py\", line 47, in on\n    output = self.asker(obs)\n  File \"/kaggle_simulations/agent/main.py\", line 141, in asker\n    output = generate_answer(chat_template)\n  File \"/kaggle_simulations/agent/main.py\", line 28, in generate_answer\n    out_ids = model.generate(**inp_ids,max_new_tokens=15).squeeze()\n  File \"/opt/conda/lib/python3.10/site-packages/torch/utils/_contextlib.py\", line 115, in decorate_context\n    return func(*args, **kwargs)\n  File \"/opt/conda/lib/python3.10/site-packages/transformers/generation/utils.py\", line 1758, in generate\n    result = self._sample(\n  File \"/opt/"}]]

---
# 他のユーザーからのコメント

> ## Araik Tamazian
> 
> "Err" は、ゲーム中にコードが例外をスローしたことを意味します。
> 
> 
> 
---
> ## Krens
> 
> 私も同じ "Err" に遭遇しました。解決しましたか？
> 
> 
> 
> > ## CchristoCTopic Author
> > 
> > エージェントログを確認してください。タイムアウトではなく、エージェントがゲーム中に "Err" を返す場合（事前にいくつかの成功したターンを実行できる場合）、メモリ不足の問題が発生している可能性があります。（チームメイトのエージェントが長いプロンプトを返す場合、それは本当でしょう。自分のプロンプトを短くするか、プロンプトが長すぎる場合は切り捨てるか、またはより小さなモデルを使用するなど、他の解決策があります。）
> > 
> > 
> > 
> > > ## Krens
> > > 
> > > ありがとうございます。メモリ不足の問題だと思います。私の "Err" エージェントは常に回答者であり、プロンプトに履歴情報を追加したため、長すぎます。
> > > 
> > > 
> > > 
---
> ## CchristoCTopic Author
> 
> "3rd" は、負けたグループを意味することがわかりました。
> 
> 
> 
---

