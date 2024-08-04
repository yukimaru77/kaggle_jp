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

