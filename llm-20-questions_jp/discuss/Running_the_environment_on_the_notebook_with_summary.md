# 要約 
このディスカッションは、Kaggleの「LLM 20 Questions」コンペティションで、Kaggleノートブックで`kaggle_environments`ライブラリの環境を実行する方法に関するものです。

EduMI95は、ノートブックで環境を実行しようとすると`AttributeError: 'NoneType' object has no attribute 'lower'`というエラーが発生したと報告しました。

jazivxtは、このエラーはノートブックのメモリ制限が原因で、環境がオフラインで動作するために必要なメモリが不足しているため発生すると説明しました。また、`GemmaAgent`クラスの`raise NotImplementedError`がレスポンスの問題の原因であるとも指摘しました。

Lyubomir Klyambarskiは、`kaggle_environments`パッケージを更新することを提案しました。

G John Raoは、`Observation`クラスのコードと、`GemmaQuestionerAgent`と`GemmaAnswererAgent`を初期化してゲームループをシミュレートするコードを共有しました。しかし、このコードでも`NotImplementedError`が発生しました。

RS Turleyは、環境で実行およびデバッグする方法に関するヒントを記載したサンプルノートブックへのリンクを共有しました。

このディスカッションは、Kaggleノートブックで`kaggle_environments`ライブラリの環境を実行する際に発生する可能性のある問題と、それらの問題を解決するための解決策について議論しています。


---
# ノートブックで環境を実行する

**EduMI95** *2024年5月23日 20:07:19 (日本標準時)* (4 votes)

Kaggleのノートブック（Kaggleまたは自分のマシン）でkaggle_environmentsライブラリの環境を実行できた人はいますか？私は、ノートブックコード[https://www.kaggle.com/code/jazivxt/llm20q-gemma-2b-it](https://www.kaggle.com/code/jazivxt/llm20q-gemma-2b-it)を実行しようとしましたが、さまざまなエージェントでテストするためにコードの最後を変更しました。

```python
from kaggle_environments import make
env = make("llm_20_questions")
# コードを実行
%run submission/main.py
env.run([get_agent('questioner'), get_agent('answerer'), get_agent('questioner'), get_agent('answerer')])
env.render(mode="ipython")
```

そして、次のエラーが発生しました。

```python
File /opt/conda/lib/python3.10/site-packages/kaggle_environments/envs/llm_20_questions/llm_20_questions.py:123, in interpreter(state, env)
    121 active1.observation.category = category
    122 response = active1.action
--> 123 if response.lower().__contains__("yes"):
    124     response = "yes"
    125 elif response.lower().__contains__("no"):
AttributeError: 'NoneType' object has no attribute 'lower'
```

---
# 他のユーザーからのコメント

> ## jazivxt
> 
> 4つのエージェントに必要なメモリがあれば、環境はオフラインで動作します。ノートブックでは15GBのメモリ制限のためエラーが発生しますが、提出時には1つのエージェントしか使用していないため、正常に動作します。レスポンスの問題は、GemmaAgentクラスの最後のraise NotImplementedErrorにあります。私のスクリプトの変更を確認してください。
> 
> 
> 
> > ## EduMI95トピック作成者
> > 
> > 完璧です！ありがとう！
> > 
> > 
> > 
---
> ## Lyubomir Klyambarski
> 
> kaggle_environmentsパッケージを更新してください。
> 
> !pip install 'kaggle_environments>=1.14.8'
> 
> 
> 
---
> ## G John Rao
> 
> 次のコードを試しましたが、まだ修正されていないエラーがあります。アイデアを得るのに役立つかもしれません。
> 
> ```python
> class Observation:
>     def __init__(self, questions, answers, turnType, keyword=None, category=None):
>         self.questions = questions
>         self.answers = answers
>         self.turnType = turnType
>         self.keyword = keyword
>         self.category = category
> 
> ```
> 
> ```python
> # エージェントを初期化
> questioner = GemmaQuestionerAgent(
>     device='cpu',  # 'cpu'を使用
>     system_prompt=system_prompt,
>     few_shot_examples=few_shot_examples,
> )
> 
> answerer = GemmaAnswererAgent(
>     device='cpu',  # 'cpu'を使用
>     system_prompt=system_prompt,
>     few_shot_examples=few_shot_examples,
> )
> 
> # 初期のゲーム状態を定義
> questions = []  # 質問を保持するリスト
> answers = []    # 回答を保持するリスト
> turnType = 'ask'  # 初期のターンタイプ（質問者には'ask'または'guess'、回答者には'answer'）
> keyword = 'France'  # 回答者のためのキーワードの例
> category = 'country'  # 回答者のためのカテゴリの例
> 
> # ゲームループをシミュレート
> for _ in range(20):  # 20ターンプレイするか、キーワードが正しく推測されるまで
>     obs = Observation(questions, answers, turnType, keyword, category)
> 
>     if obs.turnType == 'ask':
>         # 質問者の質問をするターン
>         question = questioner(obs)
>         print(f"質問者: {question}")
>         questions.append(question)
> 
>         # 回答者の質問に答えるターン
>         turnType = 'answer'
>         obs = Observation(questions, answers, turnType, keyword, category)
>         answer = answerer(obs)
>         print(f"回答者: {answer}")
>         answers.append(answer)
> 
>         # 質問者のターンに戻る
>         turnType = 'ask'
> 
>     elif obs.turnType == 'guess':
>         # 質問者のキーワードを推測するターン
>         guess = questioner(obs)
>         print(f"質問者の推測: {guess}")
> 
>         if guess.lower() == keyword.lower():
>             print("質問者は正しいキーワードを推測しました！")
>             break
>         else:
>             print("推測が間違っています。プレイを続行します。")
>             turnType = 'ask'
> 
>     # 早めに停止したい場合は、ゲームの終了をシミュレート
>     if len(questions) >= 20:
>         print("最大ターン数に達しました。")
>         break
> 
> ```
> 
> 出力:
> 
> ```
> モデルを初期化しています
> response='Sure, please ask your first question: Is the keyword a food?'
> 質問者: Sure, please ask your first question: Is the keyword a food?
> 
> ```
> 
> エラー:
> 
> ```
> NotImplementedError                       Traceback (most recent call last)
> Cell In[16], line 34
>      32 turnType = 'answer'
>      33 obs = Observation(questions, answers, turnType, keyword, category)
> ---> 34 answer = answerer(obs)
>      35 print(f"回答者: {answer}")
>      36 answers.append(answer)
> 
> Cell In[8], line 23, in GemmaAgent.__call__(self, obs, *args)
>      22 def __call__(self, obs, *args):
> ---> 23     self._start_session(obs)  # 与えられた観測値で新しいセッションを開始
>      24     prompt = str(self.formatter)  # フォーマッターからプロンプトを生成
>      25     response = self._call_llm(prompt)  # モデルの応答を取得
> 
> Cell In[8], line 31, in GemmaAgent._start_session(self, obs)
>      30 def _start_session(self, obs: dict):
> ---> 31     raise NotImplementedError
> 
> NotImplementedError: 
> 
> ```
> 
> Kaggle環境がどのようにコードを実行するのか理解できません。まだ調べていないGitHubリポジトリへのリンクがあります。
> 
> ここに -> [https://github.com/Kaggle/kaggle-environments](https://github.com/Kaggle/kaggle-environments)
> 
> 
> 
---
> ## RS Turley
> 
> はい、環境で実行およびデバッグする方法に関するヒントを記載したサンプルノートブックを作成しました。
> 
> [https://www.kaggle.com/code/rturley/run-llm-20-questions-in-a-notebook](https://www.kaggle.com/code/rturley/run-llm-20-questions-in-a-notebook)
> 
> 
> 
---


