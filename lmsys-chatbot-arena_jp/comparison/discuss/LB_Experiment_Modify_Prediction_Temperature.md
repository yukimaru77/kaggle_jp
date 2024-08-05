# 要約 
## ディスカッション要約: 予測温度調整によるLBスコア改善

このディスカッションは、Kaggleコンペティション「LMSYS - Chatbot Arena 人間による好み予測チャレンジ」における予測温度調整によるリーダーボード（LB）スコア改善について議論しています。

**Rich Olson**は、予測の確信度を調整することでLBスコアを向上できるかどうかを検証した実験結果を共有しています。彼は、既存のTF-IDFモデルに温度調整を適用することで、LBスコアをわずかに改善できることを発見しました。温度を下げることで、予測の確信度が上がり、LBスコアが向上しました。

**Takamichi Toda**は、Rich Olsonの実験結果を検証し、自身の検証データでも同様の結果を得たことを報告しています。彼は、温度調整によってLBスコアが改善しただけでなく、検証データにおける温度とスコアの関係がLBの結果と一致することを確認しました。

**結論:** このディスカッションは、予測温度調整がLBスコアを改善する可能性があることを示唆しています。温度調整は、モデルの確信度を調整することで、より正確な予測を生成するのに役立ちます。

**主なポイント:**

* 予測温度調整は、予測の確信度を調整する簡単な方法です。
* 温度を下げると、予測の確信度が上がり、LBスコアが向上する可能性があります。
* 温度調整は、検証データでも有効であることが確認されています。

**今後の展望:**

* 温度調整の最適な値を決定するために、さらなる実験を行う必要があります。
* 温度調整は、他のモデルやデータセットにも適用できる可能性があります。


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

# LB Experiment: Modify Prediction Temperature

**Rich Olson** *Wed May 08 2024 10:31:30 GMT+0900 (日本標準時)* (10 votes)

I just put together a new notebook to see if adjusting the confidence of my predictions can improve LB performance:

[https://www.kaggle.com/code/richolson/lb-experiment-modify-prediction-temperature](https://www.kaggle.com/code/richolson/lb-experiment-modify-prediction-temperature)

The answer seems to be yes (a little).

The model for this notebook is identical to TF-IDF approach I used here:

[https://www.kaggle.com/code/richolson/lmsys-tf-idf-boosted-trees](https://www.kaggle.com/code/richolson/lmsys-tf-idf-boosted-trees) (LB 1.038)

The notebook works by adjusting the "temperature" of predictions.  Raw scores are divided by the temperature factor before being converted to probabilities.

In this case - increasing the temperature moves predictions closer to .33 (decreasing confidence).

Decreasing the temperature moves scores out towards 0 or 1 (increasing confidence).

I did a bunch of submissions.  Here are the resulting LB scores:

| Temp. Adjustment | LB |
| --- | --- |
| 1.3 | 1.044 |
| 1.0 | 1.038 (unchanged - as expected) |
| 0.85 | 1.036 (improved!) |
| 0.7 | 1.036 (improved!) |
| 0.5 | 1.052 |

So - it seems like the existing confidence of my model was close-to-optimal - but not quite.  Based on the clustering of scores - I doubt there is a lot more improvement to be made.

Adjusting the temperature of your predictions is quite easy:

```
#1. get raw logits
y_pred_raw = model.predict(combined_test_tfidf[-test.shape[0]:], raw_score = True)

#2. adjust temperature
adjusted_logits = y_pred_raw / temperature_factor

#3. convert to probs using softmax (from scipy.special)
preds_test = softmax(adjusted_logits, 1)

```

If this is interesting - you should also check out [@valentinwerner](https://www.kaggle.com/valentinwerner)'s notebook on this topic:

[https://www.kaggle.com/code/valentinwerner/log-loss-what-are-good-scores](https://www.kaggle.com/code/valentinwerner/log-loss-what-are-good-scores)

-Rich



---

 # Comments from other users

> ## Takamichi Toda
> 
> Thank you for suggesting this useful post-processing.
> 
> I also tried this post-processing, and the results were very good!!
> 
> When I looked at the relationship between temperature and score in the validation data, I found that it matched well with the LB results.
> 
> | Temp. Adjustment | LB |
> | --- | --- |
> | 0.8 | 1.036 |
> | 0.9 | 1.028 |
> | 1.0 | 1.025 |
> | 1.2 | 1.022 |
> | 1.4 | 1.024 |
> 
> (The vertical axis is logloss)
> 
> The temperature of 1.2, which had the highest score on the LB, was also close to the best in validation.
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

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



</div>