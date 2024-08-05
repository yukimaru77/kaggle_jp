# 要約 
コンペのディスカッションでは、参加者がKaggleの「20の質問」競技用に環境をノートブックで実行する際に直面した問題について議論しています。EduMI95は、kaggle_environmentsライブラリを使用してエージェントを実行する際に遭遇したエラーについて説明しました。このエラーは、回答がNoneTypeとして返されることに起因しています。

ディスカッションでは、他の参加者から以下のようなアドバイスが提供されました：
- jazivxtはメモリ制限が原因でエラーが発生すると指摘し、1つのエージェントを使用する場合には問題ないと述べました。また、クラス`GemmaAgent`の実装に関する変更点を共有しました。
- Lyubomir Klyambarskiは、kaggle_environmentsパッケージのアップデートを提案しました。
- G John Raoは、エージェントの初期化方法と関連するエラーについて自身の試行を共有しましたが、まだ修正が必要なエラーがあると報告しました。
- 最後に、RS TurleyはKaggle環境内で実行しデバッグする方法についての例のノートブックを作成したことを発表しました。

全体として、参加者間でエラーの詳細、解決策、コードの変更点が活発に共有されており、協力して問題解決に向けた意見交換が行われています。

---
# ノートブックで環境を実行する
**EduMI95** *2024年5月23日 20:07:19 GMT+0900 (日本標準時)* (4票)
kaggle_environmentsライブラリの環境を、ノートブック（kaggleもしくは自分のマシン上）で実行できた方はいらっしゃいますか？ノートブックのコード[https://www.kaggle.com/code/jazivxt/llm20q-gemma-2b-it](https://www.kaggle.com/code/jazivxt/llm20q-gemma-2b-it)を実行し、最後にさまざまなエージェントでテストするためにコードを変更してみたところ、次のようなエラーが出ました：
```
from kaggle_environments import make
env = make("llm_20_questions")
# コードを実行
%run submission/main.py
env.run([get_agent('questioner'), get_agent('answerer'), get_agent('questioner'), get_agent('answerer')])
env.render(mode="ipython")
```
以下のエラーが表示されます：
```
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
> 環境はオフラインで動作しており、4つのエージェントに十分なメモリがあれば正常に動きますが、ノートブックでは15GBのメモリ制限があるためエラーが出ます。ただし、提出時には1つのエージェントしか使用していないため、問題なく動作します。レスポンスに関する問題は、クラス`GemmaAgent`の最後に`raise NotImplementedError`があるため発生しています。私のスクリプトでの変更を確認してください。
> 
> > ## EduMI95 (トピック作成者)
> > 
> > 完璧です！ありがとうございます！
> > 
> > > 

---
> ## Lyubomir Klyambarski
> 
> `kaggle_environments`パッケージを更新してください。
> 
> !pip install 'kaggle_environments>=1.14.8'
> 
> ---
> ## G John Rao
> 
> 以下を試しましたが、まだ修正すべきエラーがあります。何かアイデアを得られるかもしれません。
> 
> ```
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
> ```
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
> # ゲームの初期状態を定義
> questions = []  # 質問を保持するリスト
> answers = []    # 回答を保持するリスト
> turnType = 'ask'  # 初期ターンタイプ ('ask'または'guess'は質問者、'answer'は回答者)
> keyword = 'France'  # 回答者用の例のキーワード
> category = 'country'  # 回答者用の例のカテゴリ
> 
> # ゲームループをシミュレート
> for _ in range(20):  # 20ターンまたはキーワードが正しく推測されるまでプレイ
>     obs = Observation(questions, answers, turnType, keyword, category)
> 
>     if obs.turnType == 'ask':
>         # 質問者のターンで質問を行う
>         question = questioner(obs)
>         print(f"質問者: {question}")
>         questions.append(question)
> 
>         # 回答者のターンで質問に回答
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
>         # 質問者のターンでキーワードを予想
>         guess = questioner(obs)
>         print(f"質問者が予想: {guess}")
> 
>         if guess.lower() == keyword.lower():
>             print("質問者が正しいキーワードを予想しました！")
>             break
>         else:
>             print("不正解です。プレイを続けます。")
>             turnType = 'ask'
> 
>     # 早期にゲームを終了させるシミュレーション
>     if len(questions) >= 20:
>         print("最大ターン数に達しました。")
>         break
> 
> ```
> 
> 出力:
> 
> ```
> モデルの初期化
> response='はい、最初の質問をどうぞ: キーワードは食べ物ですか？'
> 質問者: はい、最初の質問をどうぞ: キーワードは食べ物ですか？
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
> ---> 23     self._start_session(obs)  # 指定した観測で新しいセッションを開始
>      24     prompt = str(self.formatter)  # フォーマッターからプロンプトを生成
>      25     response = self._call_llm(prompt)  # モデルのレスポンスを取得
> 
> Cell In[8], line 31, line で、GemmaAgent._start_session(self, obs)
> ---> 31     raise NotImplementedError
> 
> NotImplementedError: 
> 
> ```
> kaggleの環境でコードがどのように実行されているのかはまだ理解できていません。探求すべきGitHubリポジトリのリンクもあります。
> 
> こちら -> [https://github.com/Kaggle/kaggle-environments](https://github.com/Kaggle/kaggle-environments)
> 
> ---
> ## RS Turley
> 
> はい、環境内で実行しデバッグする方法についての例のノートブックを作成しました。
> 
> [https://www.kaggle.com/code/rturley/run-llm-20-questions-in-a-notebook](https://www.kaggle.com/code/rturley/run-llm-20-questions-in-a-notebook)
