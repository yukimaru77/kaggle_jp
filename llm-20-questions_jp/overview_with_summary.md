# 要約 
## コンペ「LLM 20 Questions - 言語モデルで挑む「20問ゲーム」」の概要と分かりやすい説明

**概要:**

このコンペでは、**2つの言語モデル(LLM)を協力させて「20の質問」ゲームで競わせる**ことを目指します。  LLMはそれぞれ「質問者」と「回答者」の役割を担い、限られた質問回数で答えを推理します。

**分かりやすい説明:**

例えば、あなたが「質問者LLM」、友達が「回答者LLM」だとします。  

1. お互いに、ある「もの」を頭に思い浮かべます（例：りんご）。
2. あなたは友達に、その「もの」について「はい」か「いいえ」で答えられる質問を20回以内で投げかけます（例：「それは赤い？」「それは食べられる？」）。
3. 友達は、頭に思い浮かべた「もの」に基づいて「はい」か「いいえ」で答えます。
4. あなたは、友達の答えから「もの」を推理し、当てはめます。

このコンペでは、上記のようなやり取りを、**LLM同士で行わせます**。  高性能なLLMは、論理的な質問を組み立て、回答から効率的に情報を絞り込み、少ない質問回数で正解を導き出すでしょう。

**コンペのポイント:**

- **2対2のチーム戦:**  「質問者LLM」と「回答者LLM」のペアで競い合います。
- **限られた質問回数:**  効率的な情報収集と推論が求められます。
- **評価システム:**  対戦結果によって各LLMのスキル評価が変動します。
- **最終評価:**  コンペ期間終了後、未知の単語を用いたゲームで最終的なランキングが決定します。

**このコンペを通して、LLMの以下のような能力が試されます:**

- **演繹的推論:**  与えられた情報から論理的に結論を導き出す能力
- **情報収集能力:**  的を絞った質問によって必要な情報を効率的に集める能力
- **協力:**  「質問者」と「回答者」のLLMが連携して答えを導き出す能力

**賞金:**

- 1位：12,000ドル  
- 2位：10,000ドル  
- 3位：10,000ドル  
- 4位：10,000ドル  
- 5位：8,000ドル 


---
# 用語概説 
機械学習・深層学習初心者がつまずきそうな専門用語の解説：

**コンペティション特有の用語:**

- **エージェント(Agent):** このコンペでは、LLMを搭載した「質問者」と「回答者」を指します。  
- **ボット(Bot):** エージェントと同義です。
- **エピソード(Episode):**  1回の「20の質問」ゲームのことです。
- **スキル評価(Skill Rating):**  各ボットに割り当てられる強さの指標です。ガウス分布(μ, σ2)で表され、μは推定スキル、σは推定の不確実性を示します。
- **検証エピソード(Validation Episode):**  提出したボットが正常に動作するかを確認するためのテストゲームです。
- **アクティブな提出物(Active Submission):**  現在、評価のためにゲームに参加しているボットのことです。
- **非アクティブ化(Deactivated):**  新しいボットが提出され、アクティブな提出物の上限を超えた場合、古いボットは非アクティブ化され、評価のためのゲームに参加しなくなります。

**その他:**

- **ペアエージェント(Paired Agents):**  協力してタスクを実行するエージェントのことです。このコンペでは、「質問者」と「回答者」がペアエージェントとなります。
- **推定スキル(Estimated Skill):**  過去の対戦結果に基づいて計算された、ボットの強さの推定値です。μで表されます。
- **不確実性(Uncertainty):**  推定スキル(μ)の信頼度を示す指標です。σで表され、値が小さいほど信頼度が高いことを意味します。
- **情報量(Information Gain):**  ある事象を観測することで、対象に関する不確実性がどれだけ減少したかを表す量です。このコンペでは、ゲームの結果から得られる情報量に応じて、スキル評価の不確実性(σ)が減少します。


**備考:**

- 上記の説明は、このコンペのルールにおける独自の定義に基づいています。
- 一般的な機械学習・深層学習の用語や概念については、説明を省略しています。

---
## LLM 20 Questions - 言語モデルで挑む「20問ゲーム」

**概要**

このコンペティションでは、誰もが知る「20の質問」ゲームをプレイできる言語モデルの開発に挑戦します。参加チームは2対2の対戦形式で、いち早く答えを導き出すことを競います。

### 説明

「それは動物、植物、それとも鉱物？」「それはパン箱より小さい？」「それは700億パラメータのモデルより小さい？」

「20の質問」は、古くから楽しまれている言葉当てゲームです。プレイヤーは、「はい」または「いいえ」でしか答えられない質問を駆使し、20問以内で答えを導き出します。質問の範囲を徐々に狭め、できるだけ少ない質問で答えにたどり着くことが求められます。

各チームは、質問と解答を推測する「質問者LLM」と、「はい」または「いいえ」で回答する「回答者LLM」の2つのLLMで構成されます。戦略的な質問と回答を通じて、できるだけ少ないラウンドで答えを正しく特定することが目標です。

このコンペティションでは、演繹的推論、的を絞った質問による効率的な情報収集、ペアエージェント間の連携といった、LLMの重要なスキルが評価されます。限られた質問回数で創造性と戦略を駆使する必要がある、制約された環境も特徴です。成功すれば、LLMは単に質問に答えるだけでなく、洞察に満ちた質問をし、論理的な推論を行い、可能性を迅速に絞り込む能力を実証することになります。

### 評価

各チームは毎日、最大5つのエージェント（ボット）をコンペティションに提出できます。各提出物は、リーダーボード上で同様のスキル評価を持つ他のボットと対戦し、ゲームをプレイします。時間の経過とともに、勝利すればスキル評価は上がり、敗北すれば下がり、引き分けなら横ばいになります。

このコンペティションは、2対2の協力形式で行われます。提出したボットは、ランダムに選ばれた同程度のスキルを持つボットとペアになり、別のペアと対戦します。各ペアでは、一方のボットが質問者、もう一方が回答者にランダムに割り当てられます。ペアとして勝敗が決まるため、協力し合うことが重要です。

提出されたすべてのボットは、コンペティション終了までゲームをプレイし続けます。新しいボットほど、より頻繁にプレイするように選択されます。アクティブな提出物が3つに達すると、古い提出物は非アクティブ化されます。リーダーボードには、最もスコアの高いボットのみが表示されますが、提出ページでは、すべての提出物の進捗状況を追跡できます。

各提出物には、ガウス分布N(μ,σ2)でモデル化された推定スキル評価があります。μは推定スキル、σはその推定の不確実性を表し、時間の経過とともに減少していきます。

提出物をアップロードすると、まず検証エピソードが実行されます。このエピソードでは、提出物がそれ自身の複製と対戦し、正常に動作することを確認します。エピソードが失敗した場合、提出物はエラーとしてマークされ、原因を特定するためにエージェントログをダウンロードできます。そうでない場合は、μ0=600で提出物が初期化され、継続的な評価のためのプールに参加します。このとき、アクティブなエージェントの総数が3つを超える場合は、古いエージェントが非アクティブ化されます。

### ランキングシステム

エピソードが終了すると、そのエピソードに参加したすべてのボットの評価推定値が更新されます。一方のボットペアが勝利した場合、そのペアのμは増加し、対戦相手のμは減少します。結果が引き分けだった場合は、μ値はそれぞれの平均値に近づきます。更新の大きさは、以前のμ値に基づく予想結果からの偏差、および各ボットの不確実性σに比例します。また、結果によって得られた情報量に比例して、σ項も減少します。ボットがエピソードで勝利または敗北したスコアは、スキル評価の更新には影響しません。

### 最終評価

2024年8月13日の提出締め切り時点で、提出物はロックされます。2024年8月13日から8月27日までは、公開されていない新しい単語のセットに対してエピソードを実行し続けます。この期間中、リーダーボードの対象となるのは、アクティブな3つの提出物のみです。この期間の終了時に、リーダーボードが確定します。

### タイムライン

- 2024年5月15日 - 開始日
- 2024年8月6日 - 参加締め切り。この日までにコンペティションルールに同意する必要があります。
- 2024年8月6日 - チーム統合締め切り。この日を過ぎると、チームへの参加や統合はできなくなります。
- 2024年8月13日 - 最終提出締め切り
- 2024年8月13日～8月27日 - 最終ゲームの実施予定期間
- 2024年8月28日 - 受賞者の発表

特に明記されていない限り、すべての締め切りは、対応する日の協定世界時（UTC）午後11時59分です。コンペティション主催者は、必要と deem it necessary.

### 賞金

- 1位：12,000ドル
- 2位：10,000ドル
- 3位：10,000ドル
- 4位：10,000ドル
- 5位：8,000ドル

### 20の質問ルール

ゲームはラウンド制で行われ、合計20ラウンドです。各ラウンドの開始時に、2人の質問者はそれぞれターゲットワードを推測しようとして質問を提出し、次にターゲットワードが何であるかについての推測を提出します。

いずれかの質問者がそのラウンドでターゲットワードを正しく推測した場合、そのチームはすぐにゲームに勝利します。両方の質問者が同じラウンドで正しく推測した場合、そのラウンドは引き分けになります。

どちらの質問者も正しく推測しない場合、ゲームは次のラウンドに進みます。2人の回答者はそれぞれ、「はい」または「いいえ」のいずれかで、チームの質問者からの質問に答えます。この情報を使用して、質問者は次のラウンドで新しい質問と推測を提出します。

このプロセスは、合計20ラウンドまで繰り返されます。20ラウンド後もどちらのチームも単語を推測できなかった場合、ゲームは引き分けになります。目標は、各チームの質問者が、回答エージェントによって提供された情報に基づいて、できるだけ少ないラウンドでターゲットワードを推測することです。

## タイムアウト、制限、ペナルティ

- 質問は2000文字までに制限されています
- 推測は100文字までに制限されています
- タイムアウト
    - エージェントは1ラウンドあたり60秒の回答時間を与えられます
    - エージェントはゲームを通して使用できる追加の300秒の超過時間を持ちます
    - エージェントがタイムアウトになると、ゲームは終了します
- 回答エージェントが「はい」または「いいえ」以外で回答した場合、ゲームは終了し、その試合は負けとなります。

## 技術仕様

- ディスク容量：100GB
- RAM：16GB
- GPU：1 T4 GPU

### 引用

Zoe Mongan, Luke Sernau, Will Lifferth, Bovard Doerschuk-Tiberi, Ryan Holbrook, Will Cukierski, Addison Howard. (2024). LLM 20 Questions. Kaggle. https://kaggle.com/competitions/llm-20-questions

## コンペティション主催者

Kaggle

## 賞金と賞品

- 賞金総額：50,000ドル
- アワードポイントとメダル

## 参加状況

- 参加者数：6,079人
- チーム数：721チーム
- 提出回数：1,496回

## タグ

- テキスト
- 自然言語処理
- カスタム指標