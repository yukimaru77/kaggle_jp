# AとBの両方の応答が[null]の場合

**Takamichi Toda** *2024年5月13日 月曜日 09:43:54 GMT+0900 (日本標準時)* (22票)

データ分析中に、AとBの両方の応答が[null]になっているサンプルを見つけました。

これらのケースのほとんどはwinner_tieなので、MLモデルを使用するのではなく、ルールで処理するのが最適です。

```python
import pandas as pd
train_df = pd.read_csv(f"/kaggle/input/lmsys-chatbot-arena/train.csv")
row = train_df[train_df["id"] == 57180984].iloc[0]
res = row[["response_a", "response_b", "winner_model_a", "winner_model_b", "winner_tie"]].to_dict()
print(res)
# {'response_a': '[null]', 'response_b': '[null]', 'winner_model_a': 0, 'winner_model_b': 0, 'winner_tie': 1}
```

一方、両方が[null]なのに勝者が決まっているケースもあります。

```python
row = train_df[train_df["id"] == 867270727].iloc[0]
res = row[["response_a", "response_b", "winner_model_a", "winner_model_b", "winner_tie"]].to_dict()
print(res)
# {'response_a': '[null]', 'response_b': '[null]', 'winner_model_a': 1, 'winner_model_b': 0, 'winner_tie': 0}
```

これはどのように解釈すべきでしょうか？

|  | サンプル数 | ID |
| --- | --- | --- |
| winner_tie | 12 | 57180984, 249576331, 563620901, 939431975, 1224714333, 1433968841, 1833691834, 2624561104, 3013893052, 3697544388, 3731007975, 3870030183 |
| winner_model_b | 4 | 2369712796, 2542474454, 3044249115, 3174500072 |
| winner_model_a | 3 | 867270727, 2941706797, 3235570281 |

今のところ、両方の[null]データをトレーニングデータから除外するのが良いようです。

---
# 他のユーザーからのコメント

> ## Lisa Dunlapコンペティションホスト
> 
> 両方の応答がnull値である単一の会話は削除しましたが、複数回の会話ではこれらの会話はフィルターしないことにしました。
> 
> データを解釈する際に考慮すべき点は2つあります。(1) Chatbot Arenaのユーザーは、無秩序に投票することを妨げられません。(2) Chatbot Arenaのユーザーは、会話ごとに1回だけ投票します（複数回の会話でも）。
> 
> たとえば、誰かが複数のプロンプトを連続して迅速に送信した場合、またはプラットフォームに何らかのエラーが発生した場合、有効な応答を含む会話にnull応答が導入される可能性があり、その場合、ユーザーは会話全体をどのようにランク付けするかを自分で決めることができます。
> 
> 
> 
> > ## Lisa Dunlapコンペティションホスト
> > 
> > 修正: データセットには、"[null]"値を持つ単一の会話がいくつかあるようです。これは非常にまれにしか発生しないため、トレーニングデータセットに変更を加えることはありません。
> > 
> > 
> > 
> > > ## Takamichi Todaトピック作成者
> > > 
> > > [このスレッド](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/502449)でもこのスレッドで議論されており、ノイズのある問題として興味深い問題設定になるようです。
> > > 
> > > ご回答ありがとうございます。
> > > 
> > > 
> > ## Kaizhao Liang
> > 
> > このエッジケースはテストセットにも存在すると仮定しても安全でしょうか？主に、入力の解析方法から来ています。
> > 
> > 
> > 
> > > ## Lisa Dunlapコンペティションホスト
> > > 
> > > はい、これはテストセットに（非常にまれな）エッジケースとして表示される可能性があります。
> > > 
> > > 
> > > 
---
> ## Valentin Werner
> 
> これらのケースを完全に無視して、予測の後処理にこれらのルールを追加するか、ラベルをタイに修正してトレーニングし、モデルが学習することを期待します。
> 
> 
> 
> > ## Takamichi Todaトピック作成者
> > 
> > ご回答ありがとうございます。
> > 
> > 今のところ、除外してみようと思います。
> > 
> > 
> > 
---

