# 要約 
## コンペティションディスカッション要約: 人間による好み予測：モデルランキングからモデルルーティングへ

このディスカッションは、Kaggleコンペティション「LMSYS - Chatbot Arena 人間による好み予測チャレンジ」におけるベースラインモデル構築のためのアイデアを共有しています。

**主なポイント:**

* **人間による好み予測:** このコンペティションでは、ユーザーが2つの異なるLLMの応答からどちらを好むかを予測する必要があります。これは、モデルのランキングだけでなく、特定のプロンプトに対してどのモデルが最適かを判断する「モデルルーティング」にも役立ちます。
* **ブラッドリー・テリーアルゴリズム:** このアルゴリズムは、モデルのランキングを推定するために使用できます。各モデルのスコアは、そのモデルが他のモデルに対して勝つ確率に基づいて計算されます。
* **好み予測子:** このディスカッションでは、プロンプトと2つのモデルをインプットとして受け取り、どちらのモデルがユーザーに好まれるかを予測するニューラルネットワークベースの好み予測子を提案しています。
* **アーキテクチャ:** 提案されたアーキテクチャは、プロンプトエンコーダー（BERT、Robertaなど）と好み予測子から構成されます。これらのコンポーネントは独立して、または一緒にトレーニングできます。

**利点:**

* モデルのランキングとルーティングの両方に使用できます。
* ユーザーに最適なモデルを選択し、クエリをルーティングするのに役立ちます。

**今後の発展:**

* さまざまなプロンプトエンコーダーと好み予測子のアーキテクチャを調査する。
* さまざまなモデルのランキングとルーティングの性能を比較する。

**結論:**

このディスカッションは、人間による好み予測のための興味深いアプローチを提案しており、コンペティション参加者にとって有益なベースラインモデル構築のアイデアを提供しています。


---


<style>
.column-left{
  float: left;
  width: 47.5%;
  text-align: left;
}
.column-right{
  float: right;
  width: 47.5%;
  text-align: left;
}
.column-one{
  float: left;
  width: 100%;
  text-align: left;
}
</style>


<div class="column-left">

# original

# Predictive Human Preference: From Model Ranking to Model Routing (Idea for build a baseline)

**KhanhVD** *Fri May 03 2024 17:28:13 GMT+0900 (日本標準時)* (6 votes)

This is [cool blog](https://huyenchip.com/2024/02/28/predictive-human-preference.html) from Chip Huyen about Predictive Human Preference I think it can help for this competition and give some idea to build baseline model

# Bradley-Terry algorithm

Given a history of match outcomes, the Bradley-Terry algorithm finds the model scores that maximize the likelihood of these match outcomes, turning model scoring into a maximum likelihood estimation problem. The input, for each training example, is the models that participate in the match. The output is the outcome of the match. Assuming there’s no draw, the outcome of a match is either 0 (a wins) or 1 (b wins).

[https://huyenchip.com/assets/pics/predictive-preference/3-bradley-terry.png](https://huyenchip.com/assets/pics/predictive-preference/3-bradley-terry.png)

# Predicting Human Preference For Each Prompt

If a ranking algorithm is about figuring out which model is better overall, predictive human preference is about figuring out which model is better for each prompt. If we know in advance that for a particular prompt, GPT-3.5 works just as well as GPT-4, and GPT-3.5 is cheaper, we can route that prompt to GPT-3.5 instead. Or if we know that Mistral-7B works just as well as GPT-4 and Mistral-7B is faster, we can route our query to Mistral-7B instead.

## Experiment setup

We can treat predictive human preference as a binary classification task. Given a match between 2 models, predict which one wins. If the probability of model_a winning is around 0.5, it can be considered a tie. If a Bradley-Terry model takes only (model_a, model_b) as the input, a preference predictor takes (prompt, model_a, model_b) as the input.

[https://huyenchip.com/assets/pics/predictive-preference/4-preference-predictor.png](https://huyenchip.com/assets/pics/predictive-preference/4-preference-predictor.png)

The architecture of my preference predictor looks like this. The model encoder and preference predictor are neural networks that can be trained independently or together. We can use BERT, Roberta, Deberta,.. or other encoder model as my prompt encoder.

[imagehttps://huyenchip.com/assets/pics/predictive-preference/5-predictive-preference-architecture.png](https://huyenchip.com/assets/pics/predictive-preference/5-predictive-preference-architecture.png)





</div>
<div class="column-right">

# 日本語訳

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



</div>