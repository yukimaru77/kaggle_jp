# LB実験：予測温度の調整

**Rich Olson** *2024年5月8日 水曜日 10:31:30 JST* (10票)

予測の確信度を調整することで、LBの性能を向上できるかどうかを調べるために、新しいノートブックを作成しました。

[https://www.kaggle.com/code/richolson/lb-experiment-modify-prediction-temperature](https://www.kaggle.com/code/richolson/lb-experiment-modify-prediction-temperature)

答えは「イエス（少し）」のようです。

このノートブックのモデルは、ここで使用したTF-IDFアプローチと同じです。

[https://www.kaggle.com/code/richolson/lmsys-tf-idf-boosted-trees](https://www.kaggle.com/code/richolson/lmsys-tf-idf-boosted-trees) (LB 1.038)

このノートブックは、予測の「温度」を調整することで機能します。生のスコアは、確率に変換される前に温度係数で割られます。

この場合、温度を上げると予測は0.33に近づき（確信度が低下）、温度を下げるとスコアは0または1に近づきます（確信度が上昇）。

私はたくさんの提出を行いました。結果は以下のとおりです。

| 温度調整 | LB |
| --- | --- |
| 1.3 | 1.044 |
| 1.0 | 1.038 (予想通り変化なし) |
| 0.85 | 1.036 (改善!) |
| 0.7 | 1.036 (改善!) |
| 0.5 | 1.052 |

したがって、私のモデルの既存の確信度はほぼ最適でしたが、完全ではありませんでした。スコアの集まりから判断すると、これ以上の改善は期待できません。

予測の温度を調整するのは非常に簡単です。

```
#1. 生のロジットを取得
y_pred_raw = model.predict(combined_test_tfidf[-test.shape[0]:], raw_score = True)
#2. 温度を調整
adjusted_logits = y_pred_raw / temperature_factor
#3. ソフトマックス（scipy.specialから）を使用して確率に変換
preds_test = softmax(adjusted_logits, 1)
```

興味があれば、このトピックに関する[@valentinwerner](https://www.kaggle.com/valentinwerner)のノートブックも確認してください。

[https://www.kaggle.com/code/valentinwerner/log-loss-what-are-good-scores](https://www.kaggle.com/code/valentinwerner/log-loss-what-are-good-scores)

-Rich
---
 # 他のユーザーからのコメント
> ## Takamichi Toda
> 
> この有用な後処理を提案していただきありがとうございます。
> 
>私もこの後処理を試してみたところ、結果は非常に良好でした!!
> 
> 検証データにおける温度とスコアの関係を見ると、LBの結果とよく一致していました。
> 
> | 温度調整 | LB |
> | --- | --- |
> | 0.8 | 1.036 |
> | 0.9 | 1.028 |
> | 1.0 | 1.025 |
> | 1.2 | 1.022 |
> | 1.4 | 1.024 |
> 
> (縦軸は対数損失)
> 
> LBで最も高いスコアだった温度1.2は、検証でもほぼ最良でした。
> 
> 
> 
---

