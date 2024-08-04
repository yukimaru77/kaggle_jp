# 要約 
このディスカッションは、KaggleのLMSYS - Chatbot Arena Human Preference Predictionsコンペティションにおける提出物のスコア計算エラーに関するものです。

ユーザーのXinは、GEMMAを使って提出した際にスコアが正しく計算されない問題に遭遇しました。他のユーザーは、この問題の原因は、提出されたsubmission.csvファイルの行数が、テストデータの行数と一致しないことにあると指摘しました。

Xinは、submission.csvファイルの行数をテストデータの行数と比較するコードを追加することで、問題を解決しました。しかし、なぜユーティリティスクリプトであるlmsys_script.pyが異なる長さを出力するのかという疑問が残りました。

最終的に、Xinはユーティリティスクリプトの使用をやめ、GPUを解放することで問題を解決しました。

このディスカッションは、コンペティション参加者が直面する可能性のある問題と、その解決策について貴重な情報を提供しています。特に、提出物のスコア計算エラーは、コンペティション参加者にとってよくある問題であり、このディスカッションは、その問題を解決するためのヒントを提供しています。


---
# 提出のスコア計算エラー

**Xin** *2024年8月2日 金曜日 04:32:13 GMT+0900 (日本標準時)* (0票)
GEMMAを使っていて、この問題に遭遇した人はいますか？入力だけ変更したのですが。
ありがとうございます！
---
# 他のユーザーからのコメント
> ## 表示名の入力
> 
> これは多くの理由で発生する可能性がありますが、最も一般的な原因は、出力されたsubmission.csvファイルの行数が、すべての隠されたテストデータで再実行した後、test.csvの行数と一致しないことです。
> 
> 
> 
> > ## XinTopic Author
> > 
> > ありがとうございます！
> > 
> > 次のコードを使用しました。
> > 
> > ```
> > !python /kaggle/usr/lib/lmsys_script/lmsys_script.py
> > import pandas as pd
> > lmsys_with_metadata = pd.read_csv("/kaggle/working/lmsys_with_metadata.csv")
> > !rm /kaggle/working/lmsys_with_metadata.csv
> > test_df = pd.read_csv("/kaggle/input/lmsys-chatbot-arena/test.csv")
> > if len(test_df) != len(lmsys_with_metadata):
> >     1/0
> > 
> > ```
> > 
> > これにより、ノートブックが例外をスローし、あなたの指摘が正しいことが証明されました。
> > 
> > なぜlmsys_script.py（ユーティリティスクリプトとして）は、submission.csvを提出した後、異なる長さを出力するのでしょうか？
> > 
> > lmsys_script.pyの中身：
> > 
> > df = pd.read_csv("/kaggle/input/lmsys-chatbot-arena/test.csv")
> > 
> > 
> > 
> > > ## XinTopic Author
> > > 
> > > lmsys_script.py（ユーティリティスクリプトとして）は、submission.csvを提出する前に、train.csvとtest.csvを使用して同じ長さを出力します。
> > > 
> > > 
> > > 
> > > ## XinTopic Author
> > > 
> > > 結局、ユーティリティスクリプトの方法を放棄してGPUを解放したところ、問題は解決しました。
> > > 
> > > 
> > > 
---
