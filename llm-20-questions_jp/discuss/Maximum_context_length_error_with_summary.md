# 要約 
ディスカッションでは、ユーザー"Kha Vo"が自分のボットで「最大コンテキスト長に関するエラー」が発生したと報告しています。このエラーは、時には8番目の質問や19番目の質問で発生するとのことです。Kha Voは「公共のRiggingモデル」を使用しており、同様の経験をした人がいるか尋ねています。

他のユーザーからのコメントとして、Rob Mullaがこの問題に関心を持ち、根本原因が特定されたかを尋ねています。ユーザー"waechter"は、質問が2000文字に制限されていることから、テンプレートに以前の質問を含むことでトークンが不足する可能性があると指摘しています。Kha Voは、彼のボットがそのような質問を許可していないと応じています。さらに、waechterはエラー発生時にKha Voのエージェントが質問者または回答者として機能しているかを確認しています。

---
# 最大コンテキスト長エラー
**Kha Vo** *2024年6月2日（日）21:42:00 JST* (1票)
不思議なエラーが発生します。時には8番目の質問で、時には19番目の質問で起こります。 
私は公共のRiggingモデルをフォークしたバージョン（ロブ・ムラ）を使用しています。
同じような経験をした方はいませんか？
[[{"duration": 82.005355, "stdout": "vLLM開始\n\n", "stderr": ""}],
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
 [{"duration": 375.321071, "stdout": "\n\u001b[1;31mフィードバックを送信する / ヘルプを得る: [https://github.com/BerriAI/litellm/issues/new\u001b[0m\nLiteLLM.Info:](https://github.com/BerriAI/litellm/issues/new\u001b[0m\nLiteLLM.Info:) このエラーをデバッグする必要がある場合は、`litellm.set_verbose=True'を使用してください。\n\n", "stderr": "OpenAIException - エラーコード: 400 - {'object': 'error', 'message': \"このモデルの最大コンテキスト長は8192トークンです。しかし、メッセージで8231トークンを要求しました。メッセージの長さを減らしてください。\", 'type': 'BadRequestError', 'param': None, 'code': 400}\nトレースバック (最も最近の呼び出しを最後に):\n  ファイル \"/kaggle_simulations/agent/lib/litellm/llms/openai.py\", 行 414, in completion\n    raise e\n  ファイル \"/kaggle_simulations/agent/lib/litellm/llms/openai.py\", 行 373, in completion\n    response = openai_client.chat.completions.create(*data, timeout=timeout)  # type: ignore\n  ファイル \"/kaggle_simulations/agent/lib/openai/_utils/_utils.py\", 行 277, in wrapper\n    return func(args, **kwargs)\n  ファイル \"/kaggle_simulations/agent/lib/openai/resources/chat/completions.py\", 行 590, in create\n    return self._post(\n  ファイル \"/kaggle_simulations/agent/lib/openai/_base_client.py\", 行 124, in post\n    return cast(ResponseT, self.request(cast_to, opts, stream=stream, stream_cls=stream_cls))\n  ファイル \"/kaggle_simulati"}]]

---
 # 他のユーザーからのコメント
> ## Rob Mulla
> 
> こんにちは[@khahuras](https://www.kaggle.com/khahuras) - この投稿に気づきました。私たちのRiggingベースラインを使っていると聞いて嬉しいです！この問題の根本原因は特定できましたか？

---
> ## waechter
> 
> 質問は2000文字に制限されており、チームによっては以前にされたいくつかの質問を含める場合があります。そのため、テンプレートに以前の質問をすべて含めると、プレイしているときにトークンが不足することがあります。（ただの推測ですが）
> 
> > ## Kha Vo トピック作成者
> > 
> > 私のボットにはその種の質問を許可していませんが…
> > 
> > 
> > > ## waechter
> > > 
> > > エラーが発生する際、あなたのエージェントは質問者としてそれとも回答者として機能していますか？
> > > 
> > > 前のコメントでは回答者だと推測しました。
> > > 
> > > >
