## LMSYS - Chatbot Arena 人間による好み予測チャレンジ

### データセットの説明

このコンペティションで使用するデータセットは、[Chatbot Arena](https://chat.lmsys.org/)におけるユーザーインタラクションを記録したものです。各インタラクションにおいて、評価者は2つの異なる大規模言語モデルに対して1つ以上のプロンプトを入力し、どちらのモデルがより満足のいく応答を生成したかを評価します。このコンペティションの目標は、評価者の好みを予測し、与えられたプロンプトと応答のペアが勝者として選択される確率を決定することです。

これは[コードコンペティション](https://www.kaggle.com/competitions/lmsys-chatbot-arena/overview/code-requirements)であることにご注意ください。提出物が評価される際、このサンプルテストデータは完全なテストセットに置き換えられます。学習データには55,000行のデータが含まれており、テストセットには約25,000行のデータが含まれていると予想されます。

### ファイル

**train.csv**

* id: 各行の一意の識別子
* model_[a/b]: モデル_[a/b]の識別子。train.csvにのみ含まれ、test.csvには含まれません。
* prompt: 両方のモデルへの入力として与えられたプロンプト
* response_[a/b]: 与えられたプロンプトに対するモデル_[a/b]からの応答
* winner_model_[a/b/tie]: 評価者の選択を示すバイナリ列。正解となるターゲット列です。

**test.csv**

* id
* prompt
* response_[a/b]

**sample_submission.csv** 正しい形式の提出ファイル

* id
* winner_model_[a/b/tie]: テストセットから予測されたもの

**注:** このコンペティションのデータセットには、冒涜的、下品、または攻撃的とみなされる可能性のあるテキストが含まれています。

### ファイル

3つのファイル

### サイズ

184.19 MB

### 種類

CSV

### ライセンス

[Attribution-NonCommercial 4.0 International (CC BY-NC 4.0)](https://creativecommons.org/licenses/by-nc/4.0/)

### sample_submission.csv (237 B)

get_appfullscreenchevron_right現在、新規参加者は許可されていません。コンペティション終了後、ルールに同意し、データを確認できるようになります。

### データエクスプローラー

184.19 MB

* calendar_view_weeksample_submission.csv
* calendar_view_weektest.csv
* calendar_view_weektrain.csv

### 概要

arrow_rightfolder3つのファイル

arrow_rightcalendar_view_week17列

get_appすべてダウンロードnavigate_nextminimizekaggle competitions download -c lmsys-chatbot-arenacontent_copyhelpデータをダウンロードtext_snippet

## メタデータ

### ライセンス

[Attribution-NonCommercial 4.0 International (CC BY-NC 4.0)](https://creativecommons.org/licenses/by-nc/4.0/)

