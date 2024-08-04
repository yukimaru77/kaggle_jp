# 人間による好み予測：モデルランキングからモデルルーティングへ（ベースライン構築のアイデア）
**KhanhVD** *2024年5月3日 金曜日 17:28:13 GMT+0900 (日本標準時)* (6 votes)

これは、Chip Huyen による [興味深いブログ](https://huyenchip.com/2024/02/28/predictive-human-preference.html) で、人間による好み予測について書かれています。このコンペティションに役立ち、ベースラインモデルを構築するためのアイデアを提供してくれると思います。

# ブラッドリー・テリーアルゴリズム
ブラッドリー・テリーアルゴリズムは、マッチの結果の履歴が与えられると、これらのマッチの結果の尤度を最大化するモデルスコアを見つけます。これにより、モデルスコアリングが最尤推定問題になります。各トレーニング例に対する入力は、マッチに参加するモデルです。出力はマッチの結果です。引き分けがないと仮定すると、マッチの結果は 0（a が勝ち）または 1（b が勝ち）のいずれかになります。

[https://huyenchip.com/assets/pics/predictive-preference/3-bradley-terry.png](https://huyenchip.com/assets/pics/predictive-preference/3-bradley-terry.png)

# 各プロンプトに対する人間による好みの予測
ランキングアルゴリズムがどのモデルが全体的に優れているかを判断することである場合、人間による好み予測は、どのモデルが各プロンプトに対して優れているかを判断することです。特定のプロンプトに対して GPT-3.5 が GPT-4 と同じように機能し、GPT-3.5 が安価であることが事前にわかっている場合、そのプロンプトを GPT-3.5 にルーティングできます。あるいは、Mistral-7B が GPT-4 と同じように機能し、Mistral-7B が高速であることがわかっている場合、クエリを Mistral-7B にルーティングできます。

## 実験設定
人間による好み予測をバイナリ分類タスクとして扱うことができます。2 つのモデル間のマッチが与えられると、どちらが勝つかを予測します。モデル a が勝つ確率が約 0.5 の場合、引き分けと見なすことができます。ブラッドリー・テリーモデルが (model_a, model_b) のみを入力として受け取る場合、好み予測子は (prompt, model_a, model_b) を入力として受け取ります。

[https://huyenchip.com/assets/pics/predictive-preference/4-preference-predictor.png](https://huyenchip.com/assets/pics/predictive-preference/4-preference-predictor.png)

私の好み予測子のアーキテクチャは次のようになります。モデルエンコーダーと好み予測子は、独立してまたは一緒にトレーニングできるニューラルネットワークです。BERT、Roberta、Deberta、... またはその他のエンコーダーモデルをプロンプトエンコーダーとして使用できます。

[imagehttps://huyenchip.com/assets/pics/predictive-preference/5-predictive-preference-architecture.png](https://huyenchip.com/assets/pics/predictive-preference/5-predictive-preference-architecture.png)

> これは興味深いアイデアです！ブラッドリー・テリーアルゴリズムは、モデルのランキングを推定するための良い出発点になる可能性があります。プロンプトエンコーダーとして BERT や Roberta などの事前トレーニング済みモデルを使用することも、このタスクに役立つ可能性があります。

> このアプローチの利点は、モデルのランキングとルーティングの両方に使用できることです。これは、モデルの選択と、ユーザーに最適なモデルへのクエリルーティングの両方に役立ちます。

> このアイデアをさらに発展させるために、さまざまなプロンプトエンコーダーと好み予測子のアーキテクチャを調査し、さまざまなモデルのランキングとルーティングの性能を比較することをお勧めします。

> このコンペティションでこのアプローチを試して、結果を共有することを楽しみにしています！

