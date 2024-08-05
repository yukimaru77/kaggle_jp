# 要約 
このディスカッションは、KaggleのLMSYS - Chatbot Arena Human Preference Predictionsコンペティションにおける後処理の有効性について議論しています。

**Nicole**は、後処理を試みたものの効果がなかったと述べています。

**Valentin Werner**は、後処理が効果がない理由を説明しています。モデルはすでに自己較正されており、予測値は実際の確率に近いため、後処理によって損失が増加する可能性が高いと主張しています。彼は、過信は致命傷であり、高信頼度の誤分類に対しては高いペナルティが課せられるため、モデルの予測値を調整すると損失が増加する可能性が高いと説明しています。

**Lorry Zou**は、対数損失のクリッピングを試みたものの、結果は同じだったと述べています。

**結論として、このディスカッションでは、後処理はLMSYS - Chatbot Arena Human Preference Predictionsコンペティションでは効果がない可能性が高いことが示唆されています。** モデルはすでに自己較正されており、後処理によって損失が増加する可能性が高いからです。


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

# Does post-processing apply to this competition?

**Nicole** *Wed Jul 24 2024 08:12:23 GMT+0900 (日本標準時)* (0 votes)

I tried to use some post-processing to deal with my prediction, but the effect was not good. Did you have any improvement in post-processing?



---

 # Comments from other users

> ## Valentin Werner
> 
> I tried some post processing early in the competition, which did also not work well for me. I think the intuition is that the model is basically already caibrating itself, meaning if it says "0.4" as highest probability, it will be right around 40% of the time. And 80% will be right around 80% of the time. 
> 
> If you now say 0.4 is not really confident, and that should be 0.33 , you will increase the loss in ~6 out of 10 cases (because the loss is lower if your predict 40% and it actually the right prediction).
> 
> I prepared this little code snippet to demonstrate this: 
> 
> ```
> from sklearn.metrics import log_loss
> 
> y_true = [[1,0,0]] * 4 + [[0,1,0]] * 3 + [[0,0,1]] * 3
> y_pred = [[0.4, 0.3, 0.3]] * 10
> print("raw log_loss:", log_loss(y_true, y_pred))
> # raw log_loss: 1.0888999753452235
> 
> y_true = [[1,0,0]] * 4 + [[0,1,0]] * 3 + [[0,0,1]] * 3
> y_pred = [[0.334, 0.333, 0.333]] * 10
> print("post processed (overconfident) log_loss):", log_loss(y_true, y_pred))
> # post processed (overconfident) log_loss): 1.0984133878031905
> 
> ```
> 
> Further, overconvidence is a killer. If you set a 0.8 (probably right in 80% of cases), to a 0.9, you will have a much higher loss in those 20% of cases, where you are now overconfident. You are penalized way higher for high-confidence wrong classifications.
> 
> I prepared this little code snippet to demonstrate this: 
> 
> ```
> from sklearn.metrics import log_loss
> 
> y_true = [[1,0,0]] * 2 + [[0,1,0]] * 8
> y_pred = [[0.1, 0.8, 0.05]] * 10
> print("raw log_loss:", log_loss(y_true, y_pred))
> # raw log_loss: 0.5877385652626266
> 
> y_true = [[1,0,0]] * 2 + [[0,1,0]] * 8
> y_pred = [[0.075, 0.90, 0.025]] * 10
> print("post processed (overconfident) log_loss):", log_loss(y_true, y_pred))
> # post processed (overconfident) log_loss): 0.6023418456154264
> 
> ```
> 
> I might be missing something in my intuition, but assuming your model is well calibrated, doing correction will more likely harm than fix anything.
> 
> 
> 
> > ## NicoleTopic Author
> > 
> > Totally agree with you
> > 
> > 
> > 


---

> ## Lorry Zou
> 
> I tried log-loss clipping, got same results.
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# このコンペティションで後処理は有効でしょうか？
**Nicole** *2024年7月24日 水曜日 08:12:23 GMT+0900 (日本標準時)* (0票)
予測値を扱うために後処理を試みましたが、効果はありませんでした。後処理で改善された方はいますか？
---
# 他のユーザーからのコメント
> ## Valentin Werner
> 
> コンペティションの初期に後処理を試しましたが、うまくいきませんでした。私の考えでは、モデルは基本的にすでに自己較正しているということです。つまり、モデルが「0.4」を最高確率として出力した場合、約40%の確率で正しくなります。そして、80%は、約80%の確率で正しくなります。
> 
> ここで、0.4はあまり自信がないので、0.33にするという処理を行うと、約10回中6回は損失が増加します（予測値が40%で実際にも正しい予測の場合、損失は低いため）。
> 
> このことを示すために、簡単なコードスニペットを用意しました。
> 
> ```
> from sklearn.metrics import log_loss
> 
> y_true = [[1,0,0]] * 4 + [[0,1,0]] * 3 + [[0,0,1]] * 3
> y_pred = [[0.4, 0.3, 0.3]] * 10
> print("raw log_loss:", log_loss(y_true, y_pred))
> # raw log_loss: 1.0888999753452235
> 
> y_true = [[1,0,0]] * 4 + [[0,1,0]] * 3 + [[0,0,1]] * 3
> y_pred = [[0.334, 0.333, 0.333]] * 10
> print("post processed (overconfident) log_loss):", log_loss(y_true, y_pred))
> # post processed (overconfident) log_loss): 1.0984133878031905
> 
> ```
> 
> さらに、過信は致命傷です。0.8（おそらく80%の確率で正しい）を0.9に設定すると、過信している20%のケースで損失が大幅に増加します。高信頼度の誤分類に対しては、はるかに高いペナルティが課せられます。
> 
> このことを示すために、簡単なコードスニペットを用意しました。
> 
> ```
> from sklearn.metrics import log_loss
> 
> y_true = [[1,0,0]] * 2 + [[0,1,0]] * 8
> y_pred = [[0.1, 0.8, 0.05]] * 10
> print("raw log_loss:", log_loss(y_true, y_pred))
> # raw log_loss: 0.5877385652626266
> 
> y_true = [[1,0,0]] * 2 + [[0,1,0]] * 8
> y_pred = [[0.075, 0.90, 0.025]] * 10
> print("post processed (overconfident) log_loss):", log_loss(y_true, y_pred))
> # post processed (overconfident) log_loss): 0.6023418456154264
> 
> ```
> 
> 私の直感に何か欠陥があるのかもしれませんが、モデルが適切に較正されていると仮定すると、修正を行うと、修正よりも悪化する可能性が高くなります。
> 
> 
> 
> > ## NicoleTopic Author
> > 
> > 同意します。
> > 
> > 
> > 
---
> ## Lorry Zou
> 
> 対数損失のクリッピングを試しましたが、結果は同じでした。
> 
> 
> 
---



</div>