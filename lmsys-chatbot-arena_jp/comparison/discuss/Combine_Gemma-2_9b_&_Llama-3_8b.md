# 要約 
このディスカッションは、KaggleのLMSYS - Chatbot Arena Human Preference Predictionsコンペティションにおける、Gemma-2 9bとLlama-3 8bの2つのモデルを組み合わせたアンサンブル手法について議論しています。

トピック作成者のG John Raoは、2つのモデルを組み合わせることでLBスコアが0.945に達したことを報告しました。他のユーザーは、加重平均、スタッキング、バギングなどの手法を用いてモデルを融合させる方法について質問しました。

Akeryu Ryuuは、同じ手法を試したもののLBスコアが1.15と低かったことを報告しました。Valentin Wernerは、インデックスの整合性やモデルの個別の性能を確認するようアドバイスしました。Akeryu Ryuuは、調査の結果、Gemmaモデルの微調整されたLoRA重みをロードしていなかったことが原因であることが判明しました。

Ravshan Kutkovinは、Gemma-2 9bとLlama-3 8bの組み合わせについて詳しく説明を求めました。G John Raoは、別のユーザーが作成したノートブックを紹介しました。

このディスカッションは、アンサンブル手法を用いたモデル融合の有効性と、その際に発生する可能性のある問題点について示唆しています。また、モデルの性能を向上させるためには、インデックスの整合性やモデルの個別の性能を確認することが重要であることを示しています。


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

# Combine Gemma-2 9b & Llama-3 8b

**G John Rao** *Fri Jul 26 2024 17:50:20 GMT+0900 (日本標準時)* (7 votes)

Hi everyone, 

I have the two highest-scoring LB notebooks together in each device of T4 GPU.

LB: 0.945

[notebook](https://www.kaggle.com/code/jaejohn/lmsys-combine-gemma-2-9b-llama-3-8b)



---

 # Comments from other users

> ## xiaotingting
> 
> The effect is better after integrating the two models, but is there any way to fuse the two models other than directly adding them together?
> 
> 
> 
> > ## G John RaoTopic Author
> > 
> > You can surely explore weighted averaging, stacking, bagging, etc. I am sure it'll improve the predictions. 
> > 
> > 
> > 


---

> ## Akeryu Ryuu
> 
> I tried this and the results weren't that good, lb of 1.15. And with each submission taking about 8~9 hours each, tuning the submission weights to lb is hard so hopefully you have better luck than me.
> 
> 
> 
> > ## Valentin Werner
> > 
> > Results this bad might indicate that you did not align indices properly. You may want to sort by index before ensembling
> > 
> > 
> > 
> > > ## Akeryu Ryuu
> > > 
> > > Thank you for the advice but I don't really believe that's the problem because I was joining the submissions by id before ensembling. 
> > > 
> > > This is the code I used
> > > 
> > > ```
> > > gemma_sub = pd.read_csv("gemma_submission.csv")
> > > llama_sub = pd.read_csv("llama_submission.csv")
> > > 
> > > merged_submission = pd.merge(gemma_sub, llama_sub, on='id', suffixes=("_1", "_2"))
> > > 
> > > merged_submission["winner_model_a"] = (merged_submission["winner_model_a_1"] + merged_submission["winner_model_a_2"])/2
> > > merged_submission["winner_model_b"] = (merged_submission["winner_model_b_1"] + merged_submission["winner_model_b_2"])/2
> > > merged_submission["winner_tie"] = (merged_submission["winner_tie_1"] + merged_submission["winner_tie_2"])/2
> > > 
> > > final_submission = merged_submission[["id", "winner_model_a", "winner_model_b", "winner_tie"]]
> > > 
> > > ```
> > > 
> > > 
> > > 
> > > ## Valentin Werner
> > > 
> > > Did you validate individual performance of these models? Have you maybe mixed up the input format you used for training with another input format? Or maybe you have mixed up the IDs during inference?
> > > 
> > > Mathematically it is EXTREMELY unlike that two models that perform below / at .950 together go to 1.15. In general, to achieve 1.1x your models need to be overconfident in wrong labels.
> > > 
> > > 
> > > 
> > > ## Akeryu Ryuu
> > > 
> > > Thanks to your comment, I decided to double-check my setup. After about half an hour of searching, I discovered that I hadn't loaded the fine-tuned LoRA weights for the Gemma model. It turns out I missed those two lines while copying the code. So, a big thank you for pointing this out.
> > > 
> > > 
> > > 


---

> ## Ravshan Kutkovin
> 
> Can you explain more about Combine Gemma-2 9b & Llama-3 8b?
> 
> 
> 
> > ## G John RaoTopic Author
> > 
> > Another user did a good job explaining everything, here: [https://www.kaggle.com/code/nabojyotipandey/dual-model-inference-gemma2-9b-llama3-8b](https://www.kaggle.com/code/nabojyotipandey/dual-model-inference-gemma2-9b-llama3-8b)
> > 
> > 
> > 


---



</div>
<div class="column-right">

# 日本語訳

# Gemma-2 9b と Llama-3 8b の組み合わせ

**G John Rao** *2024年7月26日 17:50:20 (日本標準時)* (7票)

皆さん、こんにちは！

T4 GPU の各デバイスで、最も高い LB スコアを持つ 2 つのノートブックを組み合わせました。

LB: 0.945

[ノートブック](https://www.kaggle.com/code/jaejohn/lmsys-combine-gemma-2-9b-llama-3-8b)

---

# 他のユーザーからのコメント

> ## xiaotingting
> 
> 2 つのモデルを統合したことで効果は向上しましたが、直接加算する以外の方法で 2 つのモデルを融合させる方法はありますか？
> 
> 
> 
> > ## G John Rao (トピック作成者)
> > 
> > 加重平均、スタッキング、バギングなどを試すことができます。予測が改善されると思います。
> > 
> > 
> > 
---
> ## Akeryu Ryuu
> 
> この方法を試してみましたが、結果はあまり良くありませんでした。LB は 1.15 でした。また、各提出に約 8～9 時間かかるため、LB に対して提出の重みを調整するのは難しいです。うまくいけば、私よりも良い結果が得られることを願っています。
> 
> 
> 
> > ## Valentin Werner
> > 
> > このような悪い結果は、インデックスを正しく揃えていないことが原因かもしれません。アンサンブル化する前にインデックスでソートすることを検討してください。
> > 
> > 
> > 
> > > ## Akeryu Ryuu
> > > 
> > > 助言ありがとうございます。しかし、アンサンブル化する前に ID で提出を結合していたので、それが問題だとは思いません。
> > > 
> > > 使用したコードは次のとおりです。
> > > 
> > > ```
> > > gemma_sub = pd.read_csv("gemma_submission.csv")
> > > llama_sub = pd.read_csv("llama_submission.csv")
> > > 
> > > merged_submission = pd.merge(gemma_sub, llama_sub, on='id', suffixes=("_1", "_2"))
> > > 
> > > merged_submission["winner_model_a"] = (merged_submission["winner_model_a_1"] + merged_submission["winner_model_a_2"])/2
> > > merged_submission["winner_model_b"] = (merged_submission["winner_model_b_1"] + merged_submission["winner_model_b_2"])/2
> > > merged_submission["winner_tie"] = (merged_submission["winner_tie_1"] + merged_submission["winner_tie_2"])/2
> > > 
> > > final_submission = merged_submission[["id", "winner_model_a", "winner_model_b", "winner_tie"]]
> > > 
> > > ```
> > > 
> > > 
> > > 
> > > ## Valentin Werner
> > > 
> > > これらのモデルの個別の性能を検証しましたか？トレーニングで使用した入力形式を別の入力形式と混同している可能性はありますか？あるいは、推論中に ID を混同している可能性はありますか？
> > > 
> > > 数学的に考えると、0.950 未満または 0.950 である 2 つのモデルが 1.15 になることは非常にありえません。一般的に、1.1 倍にするには、モデルが間違ったラベルに対して過度に自信を持つ必要があります。
> > > 
> > > 
> > > 
> > > ## Akeryu Ryuu
> > > 
> > > あなたのコメントのおかげで、セットアップを再確認することにしました。約 30 分の調査の後、Gemma モデルの微調整された LoRA 重みをロードしていなかったことに気づきました。コードをコピーする際に、その 2 行を見落としていたようです。そのため、指摘していただきありがとうございます。
> > > 
> > > 
> > > 
---
> ## Ravshan Kutkovin
> 
> Gemma-2 9b と Llama-3 8b の組み合わせについて詳しく説明していただけますか？
> 
> 
> 
> > ## G John Rao (トピック作成者)
> > 
> > 別のユーザーが、ここで詳しく説明しています。[https://www.kaggle.com/code/nabojyotipandey/dual-model-inference-gemma2-9b-llama3-8b](https://www.kaggle.com/code/nabojyotipandey/dual-model-inference-gemma2-9b-llama3-8b)
> > 
> > 
> > 
---



</div>