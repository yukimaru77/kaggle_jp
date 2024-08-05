# エピソードの欠落/エラーが全体に発生しています。
**Dominique Nocito** *2024年6月18日 火曜日 22:49:17 JST* (0票)
エピソードが見つからず、全員がエラーを出しているゲームが増えているようです。エピソードリプレイを読み込めません: 55104943。
原因となる何かが私の検証ランの一つにも影響を与えたと考えています。この場合のリプレイには以下のエラーがあります。 {'error': 'string index out of range', 'trace': 'Traceback (most recent call last):\n  File "/opt/conda/lib/python3.10/site-packages/kaggle_environments/main.py", line 254, in action_handler\n    return action_run(args)\n  File "/opt/conda/lib/python3.10/site-packages/kaggle_environments/main.py", line 170, in action_run\n    env.run(args.agents)\n  File "/opt/conda/lib/python3.10/site-packages/kaggle_environments/core.py", line 268, in run\n    self.step(actions, logs)\n  File "/opt/conda/lib/python3.10/site-packages/kaggle_environments/core.py", line 232, in step\n    self.state = self.__run_interpreter(action_state, logs)\n  File "/opt/conda/lib/python3.10/site-packages/kaggle_environments/core.py", line 605, in __run_interpreter\n    raise e\n  File "/opt/conda/lib/python3.10/site-packages/kaggle_environments/core.py", line 583, in __run_interpreter\n    new_state = structify(self.interpreter(\n  File "/opt/conda/lib/python3.10/site-packages/kaggle_environments/envs/llm_20_questions/llm_20_questions.py", line 206, in interpreter\n    [one_guessed, one_bad_guess] = guesser_action(active1, inactive1, step)\n  File "/opt/conda/lib/python3.10/site-packages/kaggle_environments/envs/llm_20_questions/llm_20_questions.py", line 123, in guesser_action\n    if active.action and keyword_guessed(active.action):\n  File "/opt/conda/lib/python3.10/site-packages/kaggle_environments/envs/llm_20_questions/llm_20_questions.py", line 298, in keyword_guessed\n    if compare_words(guess, keyword):\n  File "/opt/conda/lib/python3.10/site-packages/kaggle_environments/envs/llm_20_questions/llm_20_questions.py", line 287, in compare_words\n    if a[-1] == "s" and a[:-1] == b:\nIndexError: string index out of range\n'}

---
# 他のユーザーからのコメント
> ## Bovard Doerschuk-Tiberi
> 
> 問題は解決されるはずです。
> 
> 
---
> ## Bovard Doerschuk-Tiberi
> 
> 報告ありがとうございます！すぐに修正します。
> 
> ---
