# Missing episodes/ errors across the board.

**Dominique Nocito** *Tue Jun 18 2024 22:49:17 GMT+0900 (日本標準時)* (0 votes)

I'm seeing a lot more games where everyone seems to error out and the episode can't be found. Unable to load episode replay:55104943.

I think whatever might have caused this has also effected one of my validation runs, the replay in this case has the following error. {'error': 'string index out of range', 'trace': 'Traceback (most recent call last):\n  File "/opt/conda/lib/python3.10/site-packages/kaggle_environments/main.py", line 254, in action_handler\n    return action_run(args)\n  File "/opt/conda/lib/python3.10/site-packages/kaggle_environments/main.py", line 170, in action_run\n    env.run(args.agents)\n  File "/opt/conda/lib/python3.10/site-packages/kaggle_environments/core.py", line 268, in run\n    self.step(actions, logs)\n  File "/opt/conda/lib/python3.10/site-packages/kaggle_environments/core.py", line 232, in step\n    self.state = self.__run_interpreter(action_state, logs)\n  File "/opt/conda/lib/python3.10/site-packages/kaggle_environments/core.py", line 605, in __run_interpreter\n    raise e\n  File "/opt/conda/lib/python3.10/site-packages/kaggle_environments/core.py", line 583, in __run_interpreter\n    new_state = structify(self.interpreter(\n  File "/opt/conda/lib/python3.10/site-packages/kaggle_environments/envs/llm_20_questions/llm_20_questions.py", line 206, in interpreter\n    [one_guessed, one_bad_guess] = guesser_action(active1, inactive1, step)\n  File "/opt/conda/lib/python3.10/site-packages/kaggle_environments/envs/llm_20_questions/llm_20_questions.py", line 123, in guesser_action\n    if active.action and keyword_guessed(active.action):\n  File "/opt/conda/lib/python3.10/site-packages/kaggle_environments/envs/llm_20_questions/llm_20_questions.py", line 298, in keyword_guessed\n    if compare_words(guess, keyword):\n  File "/opt/conda/lib/python3.10/site-packages/kaggle_environments/envs/llm_20_questions/llm_20_questions.py", line 287, in compare_words\n    if a[-1] == "s" and a[:-1] == b:\nIndexError: string index out of range\n'}



---

 # Comments from other users

> ## Bovard Doerschuk-Tiberi
> 
> Should be resolved now
> 
> 
> 


---

> ## Bovard Doerschuk-Tiberi
> 
> Thanks for reporting! I'll get that fixed shortly
> 
> 
> 


---
