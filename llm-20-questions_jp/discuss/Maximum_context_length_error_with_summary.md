# 要約 
このディスカッションは、Kaggleの「LLM 20 Questions」コンペティションにおける「最大コンテキスト長エラー」に関するものです。

ユーザーのKha Voは、コンペティション中に、8回目や19回目の質問時にエラーが発生していることを報告しています。このエラーは、OpenAIのモデルが最大コンテキスト長を超えたために発生しているようです。

ユーザーのRob Mullaは、Kha Voが自分のモデルをベースにしていることを指摘し、エラーの原因を尋ねています。

ユーザーのwaechterは、このエラーは質問が長すぎるために発生している可能性があると指摘しています。コンペティションのルールでは、質問は2000文字に制限されているため、過去の質問をすべて含めると、トークン数が上限を超えてしまう可能性があります。

Kha Voは、自分のボットは長い質問をするように設定されていないことを説明しています。

waechterは、エラーが発生した際に、Kha Voのボットが質問者か回答者のどちらの役割を担っていたのかを尋ねています。

このディスカッションは、コンペティション参加者が直面する技術的な問題と、その解決策について議論しています。特に、OpenAIモデルの最大コンテキスト長に関する問題と、質問の長さに関する制限が、コンペティション参加者にとって課題となっていることがわかります。


---
# 最大コンテキスト長エラー

**Kha Vo** *2024年6月2日日曜日 21:42:00 GMT+0900 (日本標準時)* (1票)

奇妙なエラーが発生しています。8回目の質問で発生することもあれば、19回目の質問で発生することもあります。

パブリック（Rob Mulla）からフォークしたRiggingモデルのバージョンを使用しています。

同じようなエラーが発生している人はいますか？

[[{"duration": 82.005355, "stdout": "vLLM Started\n\n", "stderr": ""}],
 [{"duration": 1.975345, "stdout": "", "stderr": ""}],
 [{"duration": 3.674225, "stdout": "", "stderr": ""}],
 [{"duration": 2.703787, "stdout": "", "stderr": ""}],
 [{"duration": 3.001207, "stdout": "", "stderr": ""}],
 [{"duration": 4.30606, "stdout": "", "stderr": ""}],
 [{"duration": 1.13816, "stdout": "", "stderr": ""}],
 [{"duration": 3.413029, "stdout": "", "stderr": ""}],
 [{"duration": 1.112546, "stdout": "", "stderr": ""}],
 [{"duration": 4.805608, "stdout": "", "stderr": ""}],
 [{"duration": 3.679116, "stdout": "", "stderr": ""}],
 [{"duration": 3.024704, "stdout": "", "stderr": ""}],
 [{"duration": 1.29648, "stdout": "", "stderr": ""}],
 [{"duration": 5.255335, "stdout": "", "stderr": ""}],
 [{"duration": 2.962781, "stdout": "", "stderr": ""}],
 [{"duration": 375.321071, "stdout": "\n\u001b[1;31mGive Feedback / Get Help: [https://github.com/BerriAI/litellm/issues/new\u001b[0m\nLiteLLM.Info:](https://github.com/BerriAI/litellm/issues/new\u001b[0m\nLiteLLM.Info:) If you need to debug this error, use `litellm.set_verbose=True'.\n\n", "stderr": "OpenAIException - Error code: 400 - {'object': 'error', 'message': \"This model's maximum context length is 8192 tokens. However, you requested 8231 tokens in the messages, Please reduce the length of the messages.\", 'type': 'BadRequestError', 'param': None, 'code': 400}\nTraceback (most recent call last):\n  File \"/kaggle_simulations/agent/lib/litellm/llms/openai.py\", line 414, in completion\n    raise e\n  File \"/kaggle_simulations/agent/lib/litellm/llms/openai.py\", line 373, in completion\n    response = openai_client.chat.completions.create(*data, timeout=timeout)  # type: ignore\n  File \"/kaggle_simulations/agent/lib/openai/_utils/_utils.py\", line 277, in wrapper\n    return func(args, **kwargs)\n  File \"/kaggle_simulations/agent/lib/openai/resources/chat/completions.py\", line 590, in create\n    return self._post(\n  File \"/kaggle_simulations/agent/lib/openai/_base_client.py\", line 1240, in post\n    return cast(ResponseT, self.request(cast_to, opts, stream=stream, stream_cls=stream_cls))\n  File \"/kaggle_simulati"}]]
---
 # 他のユーザーからのコメント
> ## Rob Mulla
> 
> Hey [@khahuras](https://www.kaggle.com/khahuras) - この投稿に気づきました。Riggingのベースラインを使ってくれて嬉しいです！この問題の根本原因はわかりましたか？
> 
> 
> 
---
> ## waechter
> 
> 質問は2000文字に制限されており、一部のチームはキーワードがリストにあるような質問でその文字数すべてを使用しています...。そのため、テンプレートに以前の質問がすべて含まれている場合、それらを使用するとトークンが不足してしまいます。（推測ですが）
> 
> 
> 
> > ## Kha Voトピック作成者
> > 
> > 私のボットは、そのような質問をすることは許可されていません...
> > 
> > 
> > 
> > > ## waechter
> > > 
> > > エラーが発生したとき、あなたのエージェントはどの役割（推測者または回答者）を担っていましたか？
> > > 
> > > 前のコメントでは、回答者だと想定していました。
> > > 
> > > 
> > > 
---


