# 要約 
## ディスカッション要約

Rich Olson氏は、Debertaによる特徴抽出とLGBMを用いたノートブックを共有しました。このノートブックは、リーダーボードで1.030のスコアを達成しています。

ノートブックでは、Debertaで特徴抽出を行い、LGBMでトレーニングと推論を行っています。P100での実行時間は約3時間で、そのほとんどはDebertaによる特徴抽出に費やされています。

Deberta-baseを使用しており、より小さなモデルを使用すれば実行時間を短縮できる可能性があります。

注意点は、Debertaモデルは1,000〜5,000個のプロンプトではうまく動作せず、10,000個以上のサンプルでトレーニングを開始したところ、ようやく収束し始めたことです。Debertaモデルが何も出力していない場合は、より多くのデータを試してみることを推奨しています。

関連するキッチンスインクノートブックも公開しており、現在のスコアは[https://www.kaggle.com/code/richolson/deberta-tf-idf-word2vec](https://www.kaggle.com/code/richolson/deberta-tf-idf-word2vec)で確認できます。


---
# Deberta -> LGBM [1.30 LB]
**Rich Olson** *Sat May 11 2024 10:04:01 GMT+0900 (日本標準時)* (3 votes)

Debertaによる特徴抽出とLGBMを用いたノートブックを共有しました。

[https://www.kaggle.com/code/richolson/deberta](https://www.kaggle.com/code/richolson/deberta)

リーダーボードでのスコアは1.030です。

トレーニングと提出を同じ実行で実施しています。P100での実行時間は約3時間です。そのほとんどはDebertaによる特徴抽出に費やされ、LGBMのトレーニングと推論は比較的速いです。

提出には、テストデータに対しても特徴抽出を行う必要があるため、約90分追加で時間がかかります。

Deberta-baseを使用しています（おそらく、より小さなモデルを使用すれば実行時間が短縮されるでしょう）。

1点注意として、通常は1,000〜5,000個のプロンプトで簡単なテストを実行して、正常に動作しているかどうかを確認します。TF-IDFでは、この程度のデータでも結果が得られました。しかし、Debertaでは、なぜか全く結果が出ませんでした。

10,000個以上のサンプルでトレーニングを開始したところ、ようやく収束し始めました。

つまり、Debertaモデルが何も出力していない場合は、より多くのデータを試してみることをお勧めします。

関連するキッチンスインクノートブックも公開しており、現在のスコアは次のとおりです。

[https://www.kaggle.com/code/richolson/deberta-tf-idf-word2vec](https://www.kaggle.com/code/richolson/deberta-tf-idf-word2vec)

