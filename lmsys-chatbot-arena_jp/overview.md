## LMSYS - Chatbot Arena 人間による好み予測チャレンジ

**現実世界における人間による好みの予測**

### 概要

このコンペティションでは、大規模言語モデル（LLM）を搭載したチャットボット同士を競わせて、どちらの応答がユーザーに好まれるかを予測することが課題です。[Chatbot Arena](https://chat.lmsys.org/)のデータセットが提供され、そこには異なるLLMがユーザーのプロンプトに対して生成した応答が含まれています。

優れた機械学習モデルを開発することで、チャットボットと人間の相互作用を改善し、人間の好みにより的確に対応できるようにします。

### 詳細

大規模言語モデル（LLM）は急速に私たちの生活に入り込んでいますが、LLMとの相互作用を成功させるには、ユーザーに響く応答を返すことが不可欠です。このコンペティションは、現実世界のデータを使ってこの課題に取り組み、LLMの能力と人間の好みのギャップを埋めるまたとない機会を提供します。

本コンペティションでは、Chatbot Arenaから収集された大規模なデータセットを使用します。Chatbot Arenaでは、ユーザーは2つの匿名化されたLLMとチャットし、どちらの応答が好ましいかを選択します。このコンペティションでのあなたのタスクは、このような一対一の対戦において、ユーザーがどちらの応答を好むかを予測することです。

この課題は、人間からのフィードバックによる強化学習（RLHF）における「報酬モデル」または「選好モデル」の概念と一致しています。先行研究では、既存のLLMに対して直接プロンプトを与えて選好予測を行うことには限界があることが分かっています。これらの限界は、最初に提示された応答を好む傾向（順序バイアス）、過度に冗長になる傾向（冗長性バイアス）、自己宣伝を行う傾向（自己強化バイアス）などのバイアスに起因することがよくあります。

ユーザーの好みを効果的に予測できるモデルを構築するために、さまざまな機械学習技術を試すことをお勧めします。皆さんの研究は、個々のユーザーの好みに合わせた応答を返すことができるLLMの開発に役立ち、最終的には、よりユーザーフレンドリーで広く受け入れられるAI搭載の会話システムにつながります。

### 評価

提出物は、予測確率と正解値の間の[対数損失](https://www.kaggle.com/code/metric/log-loss?scriptVersionId=151169978)（"eps=auto"を使用）で評価されます。

## 提出ファイル

テストセットの各IDについて、各ターゲットクラスの確率を予測する必要があります。ファイルにはヘッダーを含め、以下の形式にする必要があります。

```
 id,winner_model_a,winner_model_b,winner_tie
 136060,0.33,0,33,0.33
 211333,0.33,0,33,0.33
 1233961,0.33,0,33,0.33
 etc
```

### スケジュール

- 2024年5月2日 - 開始日
- 2024年7月29日 - 参加登録締め切り。この日までにコンペティションのルールに同意する必要があります。
- 2024年7月29日 - チーム統合締め切り。この日を過ぎると、チームへの参加やチームの統合はできなくなります。
- 2024年8月5日 - 最終提出締め切り。

特に明記されていない限り、すべての締め切りは協定世界時（UTC）の午後11時59分です。コンペティション主催者は、必要に応じてコンテストのスケジュールを変更する権利を留保します。

### 賞金

- 1位 - 25,000ドル
- 2位 - 20,000ドル
- 3位 - 20,000ドル
- 4位 - 20,000ドル
- 5位 - 15,000ドル

### コード要件

### このコンペティションはコードコンペティションです

このコンペティションへの提出は、ノートブックを通じて行う必要があります。コミット後に「提出」ボタンを有効にするには、以下の条件を満たす必要があります。

- CPUノートブック <= 9時間の実行時間
- GPUノートブック <= 9時間の実行時間
- インターネットアクセス無効
- 事前トレーニング済みモデルを含む、自由に公開されている外部データの使用が許可されています。
- 提出ファイルの名前は「submission.csv」にする必要があります。
- 提出の実行時間は、わずかに難読化されています。全く同じ提出を繰り返した場合、スコアを受け取るまでの時間に最大15分のばらつきが生じます。

提出方法の詳細については、[コードコンペティションFAQ](https://www.kaggle.com/docs/competitions#notebooks-only-FAQ)を参照してください。また、提出エラーが発生した場合は、[コードデバッグドキュメント](https://www.kaggle.com/code-competition-debugging)を確認してください。

### 引用

Wei-lin Chiang, Lianmin Zheng, Lisa Dunlap, Joseph E. Gonzalez, Ion Stoica, Paul Mooney, Sohier Dane, Addison Howard, Nate Keating. (2024). LMSYS - Chatbot Arena Human Preference Predictions. Kaggle. https://kaggle.com/competitions/lmsys-chatbot-arena

## コンペティション主催者

LMSYS ORG
[](/organizations/lmsysorg)## 賞金と賞

100,000ドル
アワードポイントとメダル

## 参加者

8,928人の参加者
2,346人の参加者
1,808チーム
39,452件の提出

## タグ

[言語](/competitions?tagIds=2107-Languages)[テキスト会話](/competitions?tagIds=16723-Text+Conversation)[対数損失]()目次すべて折りたたむ[概要](/competitions/lmsys-chatbot-arena/overview/abstract)[説明](/competitions/lmsys-chatbot-arena/overview/description)[評価](/competitions/lmsys-chatbot-arena/overview/evaluation)[タイムライン](/competitions/lmsys-chatbot-arena/overview/timeline)[賞金](/competitions/lmsys-chatbot-arena/overview/prizes)[コード要件](/competitions/lmsys-chatbot-arena/overview/code-requirements)[引用](/competitions/lmsys-chatbot-arena/overview/citation)

