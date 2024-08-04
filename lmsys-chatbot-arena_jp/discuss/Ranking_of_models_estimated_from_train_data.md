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

