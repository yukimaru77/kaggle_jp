# 要約 
このディスカッションは、Kaggleコンペティション「LMSYS - Chatbot Arena 人間による好み予測チャレンジ」における適切なモデルの選択について議論しています。

KeShuang Liuさんは、ファインチューニング中に検証損失が1付近で振動し始めたため、最も低い損失のポイントを選択して提出すべきか、それとも最終結果を提出すべきか質問しています。

Valentin Wernerさんは、トレーニング損失ではなく検証損失に基づいてモデルを選択すべきだと回答しています。トレーニング損失はモデルが未知のデータに対してどのように予測できるかを表すものではないため、検証損失を最小化するモデルを選択すべきだと説明しています。また、検証損失で過剰適合する可能性があるため、リーダーボードの提出を「テストセット」として使用して検証損失を検証することを提案しています。

Casmir Sunnyさんは、最も低い検証損失を持つチェックポイントに対応するモデルを提出することを推奨しています。しかし、Valentin Wernerさんは、検証データのサブセットのみを使用する場合、このアプローチを盲目的に従うことで、検証データで過剰適合する可能性があると反論しています。

Yi-Fu Chenさんは、トレーニング損失と検証損失の違いについて説明しています。トレーニング損失はトレーニング中に計算された最後の損失であり、検証損失は検証データセット全体の平均損失であるため、検証損失はより滑らかで、トレーニング損失はよりぎくしゃくしている可能性があると説明しています。

このディスカッションから、適切なモデルを選択するには、検証損失を最小化するモデルを選択し、リーダーボードの提出を「テストセット」として使用して検証損失を検証することが重要であることがわかります。また、トレーニング損失と検証損失の違いを理解することも重要です。


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

# How to choose a suitable model

**KeShuang Liu** *Wed Jul 24 2024 13:48:06 GMT+0900 (日本標準時)* (0 votes)

When I was fine-tuning, log_dass started oscillating around 1. Do I need to choose a point with the lowest loss to submit, or do I submit the final result



---

 # Comments from other users

> ## Valentin Werner
> 
> This looks like a training loss, right? Your validation loss should be more stable. 
> 
> Selecting a model should never be done based on training loss, as training loss does not represent the way the model can predict on unseen data. From my experience, it is either best to train with CV to find best parameters and then do a full train for a fixed length, that worked best for all the CV models OR you train a single model, use a validation set and submit that single model.
> 
> You would then select the model / parameter which minimizes the validation loss. Note, that you can still overfit on validation loss, as you might take a specific point of the epoch which has the lowest validation loss. Small differences in validation loss do not necessarily reflect capability of the model on new data. So, it is fine to you the leaderboard submissions as "test set", which basically validates your validation loss. If your model has a lower validation loss and leaderboard score (which is loss in this case), this is a promising model.
> 
> Hope this helps you out!
> 
> 
> 
> > ## KeShuang LiuTopic Author
> > 
> > Thank you very much. I just checked and confirmed that this is indeed a training loss rather than a validation set loss. I will use the validation set loss to select the model and also try to use the training method you mentioned. Thank you for your reply
> > 
> > 
> > 


---

> ## Casmir Sunny
> 
> I will suggest that you submit the model corresponding to the checkpoint with the lowest validation loss rather than the final model. This approach ensures you are submitting the most generalizable and best-performing version of your model.
> 
> 
> 
> > ## Valentin Werner
> > 
> > This does not have to be the case. You can definetly overfit on validation data by blindly following this approach, particularly when only using a smaller subset of data as validation data. It also makes sense to compare validation loss with training loss, and decide from there. 
> > 
> > 
> > 


---

> ## Yi-Fu Chen
> 
> About Trainer
> 
> My understanding is that "Training Loss" is the last loss calculated during training, and there is no average, while "Validation Loss" is the average loss of the entire Validation dataset.
> 
> So "Validation Loss" may be smoother and "Training Loss" may be jumpier.
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# 適切なモデルの選び方

**KeShuang Liu** *2024年7月24日 水曜日 13:48:06 GMT+0900 (日本標準時)* (0票)
ファインチューニング中に、log_dassが1付近で振動し始めました。最も低い損失のポイントを選択して提出する必要がありますか、それとも最終結果を提出する必要がありますか？
---
# 他のユーザーからのコメント
> ## Valentin Werner
> 
> これはトレーニング損失ですよね？検証損失はもっと安定しているはずです。
> 
> モデルの選択は、トレーニング損失に基づいて行うべきではありません。トレーニング損失は、モデルが未知のデータに対してどのように予測できるかを表すものではないからです。私の経験では、CVを使って最適なパラメータを見つけてから、すべてのCVモデルで最も効果的だった固定の長さで完全なトレーニングを行うか、単一のモデルをトレーニングし、検証セットを使ってその単一のモデルを提出するのが最適です。
> 
> その後、検証損失を最小化するモデル/パラメータを選択します。ただし、検証損失で過剰適合する可能性があることに注意してください。これは、最も低い検証損失を持つエポックの特定のポイントを選択する可能性があるためです。検証損失のわずかな違いは、必ずしも新しいデータに対するモデルの能力を反映するものではありません。そのため、リーダーボードの提出を「テストセット」として使用して、検証損失を検証することができます。モデルの検証損失とリーダーボードスコア（この場合は損失）が低い場合は、有望なモデルです。
> 
> お役に立てれば幸いです！
> 
> 
> 
> > ## KeShuang Liuトピック作成者
> > 
> > どうもありがとうございます。確認したところ、これは確かに検証セット損失ではなく、トレーニング損失でした。検証セット損失を使ってモデルを選択し、あなたが言及したトレーニング方法も試してみます。ご回答ありがとうございます。
> > 
> > 
> > 
---
> ## Casmir Sunny
> 
> 最も低い検証損失を持つチェックポイントに対応するモデルを提出することをお勧めします。これは、最も汎用性が高く、パフォーマンスの高いモデルバージョンを提出していることを保証します。
> 
> 
> 
> > ## Valentin Werner
> > 
> > 必ずしもそうではありません。特に検証データのサブセットのみを使用する場合、このアプローチを盲目的に従うことで、検証データで過剰適合する可能性があります。トレーニング損失と検証損失を比較して、そこから判断することも理にかなっています。
> > 
> > 
> > 
---
> ## Yi-Fu Chen
> 
> トレーナーについて
> 
> 私の理解では、「トレーニング損失」はトレーニング中に計算された最後の損失であり、平均はありません。「検証損失」は、検証データセット全体の平均損失です。
> 
> したがって、「検証損失」はより滑らかで、「トレーニング損失」はよりぎくしゃくしている可能性があります。
> 
> 
> 
---


</div>