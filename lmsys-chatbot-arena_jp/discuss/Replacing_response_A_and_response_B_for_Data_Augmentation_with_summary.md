# 要約 
このディスカッションは、KaggleのLMSYS - Chatbot Arena Human Preference Predictionsコンペティションにおけるデータ拡張に関するものです。

**Takamichi Toda**さんは、応答Aと応答Bを入れ替えることでデータ拡張を試みましたが、ローカルとパブリックの両方でスコアが悪化したと報告しています。

**Lisa Dunlap**さんは、この現象は「位置バイアス」と呼ばれるもので、人間とLLMの両方で最初の提示された回答を好む傾向があることを指摘しています。

**Valentin Werner**さんは、応答AとBを入れ替えるだけではモデルが新しい価値を学習しない可能性があると指摘し、データ拡張の割合やタイラベルの扱い方について質問しています。

**Takamichi Toda**さんは、100%のサンプルで拡張し、DeBERTaを使用してモデルにどの文がAでどの文がBかを認識させる実験を行いましたが、効果はあまりなかったと答えています。また、タイラベルはそのままにしており、学習率も調整したと述べています。

**Valentin Werner**さんは、100%の拡張は2エポックトレーニングしているようなものであり、学習率スケジューリングなどのパラメータも調整する必要があると指摘しています。

**結論**

このディスカッションでは、応答AとBを入れ替えるデータ拡張が効果的ではない可能性が示唆されています。位置バイアスの存在やデータ拡張の割合、タイラベルの扱い方、学習率などのパラメータ調整の重要性が議論されています。


---
# 応答Aと応答Bの入れ替えによるデータ拡張

**Takamichi Toda** *2024年6月5日 水曜日 09:29:20 GMT+0900 (日本標準時)* (2票)

公開されているコードでは、多くの場合、応答Aと応答Bから特徴量を作成し、それらを使用して分類器をトレーニングしています。応答Aと応答B、および勝者ラベルを入れ替えることで、簡単なデータ拡張を実現できるのではないかと考えました。

しかし、うまくいきません。

|  | ローカル | パブリック |
| --- | --- | --- |
| ベースライン | 0.997 | 1.012 |
| A/Bを入れ替えて拡張 | 1.011 | 1.025 |

私のCV戦略は、単純な1つのホールドアウトであり、これまでのところパブリックLBとよく相関しています（[参照](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/500031#2824772)）。

応答がAかBかは、重要な特徴量である可能性があります。応答がAかBかによって評価にバイアスがかかるというスレッドを見たことがありますが、消えてしまったようです（おそらく[ここ](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/507091)）。

---
# 他のユーザーからのコメント

> ## Lisa Dunlapコンペティションホスト
> 
> 役に立つかどうかはわかりませんが、位置バイアスは人間とLLMの両方で知られている現象です。どちらも、最初に提示された回答を好みます。この現象がどの程度蔓延しているかについては、[LLMを審査者として用いた論文](https://arxiv.org/abs/2306.05685)で詳しく説明しています。
> 
> 
> 
---
> ## Valentin Werner
> 
> 単に入れ替えるだけでは、モデルが学習する新しい価値は生まれないと思います。代わりに、これらの行を2回トレーニングしているようなものです。
> 
> 質問:
> 
> 1) どの程度のサンプルで拡張していますか？10〜20%しか拡張していない場合は、モデルを過剰適合させたり、これらのサンプルについて過度に学習させているだけです。100%のサンプルで拡張して、モデルに応答AまたはBが実際には重要ではないことを学習させるという議論があるかもしれません（現実を反映していない可能性がありますが）。
> 
> 2) タイの場合も入れ替えていますか（タイラベルはそのままにしていますか）？そうでない場合は、クラスの不均衡が生じ、タイが予測される可能性が低くなります。
> 
> 
> 
> > ## Takamichi Todaトピック作成者
> > 
> > コメントありがとうございます。
> > 
> > 1)
> > 
> > 100%です。ちなみに、DeBERTaを使用しており、特別なトークンを追加することでモデルにどの文がAでどの文がBかを認識させる実験を行いました。しかし、効果はあまりありませんでした（わずかな改善のみ）。
> > 
> > 2)
> > 
> > 入れ替えても、「タイ」のラベルは「タイ」のままです。
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > 100%の場合、基本的に1回の価格で2エポックトレーニングしているようなものです。これは、lrスケジューリングなどに影響を与えます。
> > > 
> > > 実験でパラメータ（ウォームアップ比やエポックなど）も調整しましたか？
> > > 
> > > 
> > > ## Takamichi Todaトピック作成者
> > > 
> > > おっしゃる通りかもしれません。
> > > 
> > > 学習率には3つの異なるパターンを試しました（小さい方が良い）。
> > > 
> > > 
> > > 
---
