# 要約 
## ディスカッション要約

このディスカッションは、KaggleのLMSYS - Chatbot Arena Human Preference Predictionsコンペティションにおける、トレーニングデータからモデル名を推定するという話題についてです。

**takaito**は、トレーニングデータからモデル名を推定し、その結果を共有しました。gpt4が最も頻繁に選択される傾向にあることを発見し、モデル名だけで約1.04のスコアを獲得できる可能性があると述べています。

**他のユーザー**からのコメントは、以下の通りです。

* **Fritz Cremer**は、Geminiのようなモデルは特定の言葉で回答を始める傾向があり、それがモデルの予測を容易にする可能性があると指摘しました。
* **JunHua Liao**は、トレーニングデータとテストデータのモデルタイプの分布に大きな違いがある可能性があることを懸念しました。
* **Kishan Vavdara**は、gpt4が頻繁に勝つことに同意しました。
* **Heroseo**は、llama-3もあればもっと面白くなると述べました。
* **Lisa Dunlap**（コンテスト主催者）は、モデルそのものを予測するタスクは非常に興味深いものであり、将来的にこのテーマに関する別のコンテストを開催する可能性があると述べました。
* **tanaka**は、lmsys.org自体で既に同様の分析が行われており、eloランキングに反映されていることを指摘しました。
* **Easter Bunny**は、この話題についてさらに詳しく調べる価値があると述べました。

**結論**として、このディスカッションは、コンペティション参加者がトレーニングデータからモデル名を推定し、その情報を予測に活用できる可能性について議論しています。また、モデルの出力特性やeloランキングなどの関連情報も共有されています。


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

# Ranking of models estimated from train data.

**takaito** *Fri May 03 2024 16:08:51 GMT+0900 (日本標準時)* (34 votes)

I overlooked the fact that there is no model name in the test data.

I have estimated which model to choose from train data.

Since I have estimated for all model pair combinations, I'll share it. [notebook](https://www.kaggle.com/code/takaito/lmsys-model-name-catboostclassifier/notebook)

gpt4 tends to be selected more often.

If the model can be predicted 100% from the output, it is possible to score around 1.04 based on the name of the model alone. (This is an expectation based on the CV score at the time of the training.)

['gpt-4-1106-preview', 'gpt-4-0314', 'gpt-4-0125-preview', 'claude-1', 'gpt-4-0613', 'gpt-3.5-turbo-0314', 'claude-instant-1', 'gpt-3.5-turbo-0613', 'claude-2.0', 'claude-2.1', 'mistral-medium', 'vicuna-33b', 'llama-2-70b-chat', 'mixtral-8x7b-instruct-v0.1', 'wizardlm-70b', 'vicuna-13b', 'yi-34b-chat', 'qwen1.5-72b-chat', 'wizardlm-13b', 'starling-lm-7b-alpha', 'guanaco-33b', 'mpt-30b-chat', 'llama-2-13b-chat', 'gemini-pro-dev-api', 'koala-13b', 'gpt-3.5-turbo-1106', 'gemini-pro', 'zephyr-7b-beta', 'tulu-2-dpo-70b', 'gpt-3.5-turbo-0125', 'palm-2', 'pplx-70b-online', 'vicuna-7b', 'openchat-3.5', 'llama-2-7b-chat', 'openhermes-2.5-mistral-7b', 'nous-hermes-2-mixtral-8x7b-dpo', 'solar-10.7b-instruct-v1.0', 'zephyr-7b-alpha', 'codellama-34b-instruct', 'llama2-70b-steerlm-chat', 'dolphin-2.2.1-mistral-7b', 'openchat-3.5-0106', 'falcon-180b-chat', 'mistral-7b-instruct-v0.2', 'qwen1.5-7b-chat', 'deepseek-llm-67b-chat', 'gpt4all-13b-snoozy', 'pplx-7b-online', 'stripedhyena-nous-7b', 'mpt-7b-chat', 'mistral-7b-instruct', 'qwen-14b-chat', 'alpaca-13b', 'RWKV-4-Raven-14B', 'qwen1.5-4b-chat', 'oasst-pythia-12b', 'chatglm-6b', 'fastchat-t5-3b', 'stablelm-tuned-alpha-7b', 'chatglm3-6b', 'llama-13b', 'dolly-v2-12b', 'chatglm2-6b']

I hope this will be of some help!!



---

 # Comments from other users

> ## Fritz Cremer
> 
> This is interesting, since some models like Gemini, annoyingly often starts answers with "Absolutely! …" or "You're right! …". This should make predicting the model quite easy.
> 
> 
> 
> > ## takaitoTopic Author
> > 
> > Thanks for your comment.
> > 
> > As you commented, each model has its own output characteristics.
> > 
> > I think it is possible to predict rough models.
> > 
> > The predicted model name could be used for the features.
> > 
> > 
> > 
> > > ## JunHua Liao
> > > 
> > > Good idea. But I don't know if there is a significant difference between the distribution of model types in the training set and the test set, as there is no model type given for the test dataset.
> > > 
> > > 
> > > 


---

> ## Kishan Vavdara
> 
> 
> 
> Yes! gpt4 wins more often! 
> 
> 
> 


---

> ## Heroseo
> 
> oh, it is really instresting. 
> 
> It's a different story, but it would be more fun if there was llama-3 as well.
> 
> 
> 
> > ## Lisa DunlapCompetition Host
> > 
> > Agreed! The task of just predicting the model itself if quite interesting , perhaps there could be another competition about this in the future…
> > 
> > 
> > 
> > > ## Lisa DunlapCompetition Host
> > > 
> > > Especially if you can describe in language what are the defining characteristics of the model
> > > 
> > > 
> > > 


---

> ## tanaka
> 
> Yeah, this kind of analytics is already done in lmsys.org itself and calculated to elo ranking. You can see current lmsys's ranking in lmsys leaderboard.
> 
> old elo ranking (2023-12-7?)
> 
> current elo ranking (2024-5-27)
> 
> Refs:
> 
> - [https://lmsys.org/blog/2023-12-07-leaderboard/](https://lmsys.org/blog/2023-12-07-leaderboard/)
> 
> 
> 


---

> ## Easter Bunny
> 
> Worth delving into this
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# 訓練データから推定したモデルのランキング

**takaito** *2024年5月3日 16:08:51 (日本標準時)* (34票)

テストデータにモデル名がないことに気づいていませんでした。
訓練データからどのモデルを選択するかを推定しました。
すべてのモデルペアの組み合わせを推定したので、共有します。[ノートブック](https://www.kaggle.com/code/takaito/lmsys-model-name-catboostclassifier/notebook)
gpt4はより頻繁に選択される傾向があります。
モデルが出力から100%予測できれば、モデル名だけで約1.04のスコアを獲得できます。（これは、トレーニング時のCVスコアに基づいた期待値です。）
['gpt-4-1106-preview', 'gpt-4-0314', 'gpt-4-0125-preview', 'claude-1', 'gpt-4-0613', 'gpt-3.5-turbo-0314', 'claude-instant-1', 'gpt-3.5-turbo-0613', 'claude-2.0', 'claude-2.1', 'mistral-medium', 'vicuna-33b', 'llama-2-70b-chat', 'mixtral-8x7b-instruct-v0.1', 'wizardlm-70b', 'vicuna-13b', 'yi-34b-chat', 'qwen1.5-72b-chat', 'wizardlm-13b', 'starling-lm-7b-alpha', 'guanaco-33b', 'mpt-30b-chat', 'llama-2-13b-chat', 'gemini-pro-dev-api', 'koala-13b', 'gpt-3.5-turbo-1106', 'gemini-pro', 'zephyr-7b-beta', 'tulu-2-dpo-70b', 'gpt-3.5-turbo-0125', 'palm-2', 'pplx-70b-online', 'vicuna-7b', 'openchat-3.5', 'llama-2-7b-chat', 'openhermes-2.5-mistral-7b', 'nous-hermes-2-mixtral-8x7b-dpo', 'solar-10.7b-instruct-v1.0', 'zephyr-7b-alpha', 'codellama-34b-instruct', 'llama2-70b-steerlm-chat', 'dolphin-2.2.1-mistral-7b', 'openchat-3.5-0106', 'falcon-180b-chat', 'mistral-7b-instruct-v0.2', 'qwen1.5-7b-chat', 'deepseek-llm-67b-chat', 'gpt4all-13b-snoozy', 'pplx-7b-online', 'stripedhyena-nous-7b', 'mpt-7b-chat', 'mistral-7b-instruct', 'qwen-14b-chat', 'alpaca-13b', 'RWKV-4-Raven-14B', 'qwen1.5-4b-chat', 'oasst-pythia-12b', 'chatglm-6b', 'fastchat-t5-3b', 'stablelm-tuned-alpha-7b', 'chatglm3-6b', 'llama-13b', 'dolly-v2-12b', 'chatglm2-6b']
これは少しは役に立つことを願っています！
---
# 他のユーザーからのコメント
> ## Fritz Cremer
> 
> これは興味深いですね。Geminiのようなモデルは、しばしば「もちろんです！…」や「その通りです！…」といった言葉で回答を始めることがありますが、これはモデルの予測を非常に簡単にするはずです。
> 
> 
> 
> > ## takaitoトピック作成者
> > 
> > コメントありがとうございます。
> > 
> > あなたがコメントしたように、各モデルには独自の出力特性があります。
> > 
> > 大まかなモデルを予測することは可能だと思います。
> > 
> > 予測されたモデル名は、特徴として使用できます。
> > 
> > 
> > > ## JunHua Liao
> > > 
> > > 良いアイデアですね。しかし、テストデータセットにはモデルタイプが与えられていないため、トレーニングセットとテストセットのモデルタイプの分布に大きな違いがあるかどうかはわかりません。
> > > 
> > > 
> > > 
---
> ## Kishan Vavdara
> 
> 
> 
> はい！gpt4はより頻繁に勝ちます！
> 
> 
> 
---
> ## Heroseo
> 
> おお、これは本当に興味深いですね。
> 
> 別の話ですが、llama-3もあればもっと面白くなるでしょう。
> 
> 
> 
> > ## Lisa Dunlapコンテスト主催者
> > 
> > 同意します！モデルそのものを予測するタスクは非常に興味深いものです。将来的には、このテーマに関する別のコンテストを開催できるかもしれません…
> > 
> > 
> > > ## Lisa Dunlapコンテスト主催者
> > > 
> > > 特に、モデルの定義的な特徴を言語で説明できる場合
> > > 
> > > 
> > > 
---
> ## tanaka
> 
> ええ、この種の分析はすでにlmsys.org自体で行われており、eloランキングに計算されています。lmsysのリーダーボードで現在のlmsysのランキングを見ることができます。
> 
> 古いeloランキング（2023-12-7？）
> 
> 現在のeloランキング（2024-5-27）
> 
> 参照：
> 
> - [https://lmsys.org/blog/2023-12-07-leaderboard/](https://lmsys.org/blog/2023-12-07-leaderboard/)
> 
> 
> 
---
> ## Easter Bunny
> 
> これについて詳しく調べる価値があります。
> 
> 
> 
---



</div>