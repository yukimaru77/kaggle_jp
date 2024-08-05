# 要約 
このディスカッションは、KaggleのLMSYS - Chatbot Arena Human Preference Predictionsコンペティションにおける、生成ヘッダーを使用した予測に関するものです。

**Takamichi Toda**は、LLMの元の訓練から逸脱しない、生成ヘッダー（CausalLM）を使用した予測方法を提案しました。この方法は、プロンプトを調整し、トークンA、B、tieの生成確率を使用し、softmaxで後処理して合計が1になるようにします。Llama3 8Bでこの方法を評価したところ、1.234のスコアを得ました。

**James Day**は、同様の実験を行い、Llama 3 8B Instructでファインチューニングを行い、0.902のCVスコアを得ました。しかし、Gemma 2 9Bではうまく機能しませんでした。

**Valentin Werner**は、モデルが最初にファインチューニングされて"A"、"B"、または"tie"を予測する必要があることを認識していない限り、softmaxを仮定することが問題であると指摘しました。

**ShelterW**は、CVとLBの間に比較的大きな差が生じているのは、追加のプロンプトが原因であると考えています。

**AbaoJiang**は、ゼロショット予測のパフォーマンスはグローバル平均を上回っていないものの、試してみる価値のある興味深いアイデアであると述べています。

**Takamichi Toda**は、SFTとプロンプトチューニングでスコアを1.037に改善したと報告しました。

**ShelterW**は、Llama3-8bをファインチューニングしてLBスコアを0.935に改善したと報告しました。

このディスカッションは、生成ヘッダーを使用した予測方法が、コンペティションで有望な結果を示す可能性があることを示唆しています。しかし、この方法をさらに改善するために、ファインチューニングやプロンプトエンジニアリングなどの技術が必要であることが明らかになりました。


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

# Prediction Using Generation Header

**Takamichi Toda** *Tue Jul 16 2024 16:07:36 GMT+0900 (日本標準時)* (33 votes)

This is still a tried and tested idea and has not yet been successful in my current environment, but I would like to share it.

Currently, from what I can see in public code, the mainstream approach seems to be to base it on Llama or other LLMs and use LoRA to train a classification head. However, LLMs are originally trained to predict the next token, so I think this method is inefficient as it diverges from the original training of the LLM.

My idea is to use the same generative header (CausalLM) as the original LLM.

I adjust the prompts and use the generation probabilities of the tokens A, B and tie.　The predictions are post-processed using softmax so that they sum to one.

Below is a simple sample code:

```
text = """
### Instruction
Which model's answer is appropriate for the prompt?　If both are appropriate, answer `tie`.

### Prompt
{prompt text}

### A
{response A}

### B
{response B}

### Answer
"""

inputs = tokenizer(text)
out = model(inputs)
pred_token_id = tokenizer.encode("A") + tokenizer.encode("B") + tokenizer.encode("tie")
pred = out.logits[0, -1, pred_token_id].softmax(0)

```

Here is the code that evaluates this method using Llama3 8B.

[https://www.kaggle.com/code/takamichitoda/lmsys-zeroshot-prediction](https://www.kaggle.com/code/takamichitoda/lmsys-zeroshot-prediction)

Llama3 has not undergone any special fine-tuning and is used as loaded from the Kaggle model. The evaluation data uses 1/5 of the competition data, which is equivalent to my current validation strategy (correlates well with the public leaderboard).

As a result, we obtained a score of 1.234. It was surprising to me that I could achieve such a result with ZeroShot.

Currently, I am performing SFT on the competition data and adjusting the prompts. However, models that learn classification headers still score better.

Are there others working on a similar approach?



---

 # Comments from other users

> ## James Day
> 
> I tried a similar experiment, primarily because I was hoping to take advantage of training and inference libraries for causal language models that are faster and more memory efficient than the HuggingFace transformers library, namely unsloth and vLLM. However, I actually finetuned the LLMs, as opposed to just doing zero shot inference like [@takamichitoda](https://www.kaggle.com/takamichitoda)'s initial experiment.
> 
> I got 0.902 (CV) with Llama 3 8B Instruct doing next token prediction, which is almost as good as I've been getting with "normal" Llama 3 based classification models. However, the same approach did not work well with Gemma 2 9B (0.990 CV 🤮), possibly due to Gemma's tied embeddings. My CV scores are pretty consistently ~0.03 lower than the corresponding LB scores, so those results translate to ~0.93 & 1.02 LB, which isn't good enough for me to bother submitting.
> 
> 
> 
> > ## Takamichi TodaTopic Author
> > 
> > Thank you for sharing
> > 
> > 0.9 is a great score for me ;)
> > 
> > By the way, I would like to know if possible, what kind of prompt did you use to perform finetuning?
> > 
> > I am using trl's SFTTrainer and learning only output with DataCollatorForCompletionOnlyLM.
> > 
> > 
> > 
> > > ## James Day
> > > 
> > > I used prompts like:
> > > 
> > > ```
> > > Which one of the chatbots below did a better job responding to the user request? Or were they tied?
> > > 
> > > ~~~~~~~~~~ CONVERSATION WITH BOT A ~~~~~~~~~~
> > > 
> > > ### User: "{initial prompt}"
> > > 
> > > ### Bot A Response: "{initial response}"
> > > 
> > > ### User: "{maybe a follow up prompt if available - I included as many conversation turns as will fit in a 3k token context window, discarding the first part of each conversation if necessary}"
> > > 
> > > ### Bot A Response: "{follow up response}"
> > > 
> > > ~~~~~~~~~~ CONVERSATION WITH BOT B ~~~~~~~~~~
> > > 
> > > ### User: "{...}"
> > > 
> > > ### Bot B Response: "{...}"
> > > 
> > > ### User: "{...}"
> > > 
> > > ### Bot B Response: "{...}"
> > > 
> > > ### BEST RESPONSE:
> > > 
> > > ```
> > > 
> > > It was then trained to output " A", " B", or " Tie". The spaces were part of the response tokens.
> > > 
> > > 
> > > 
> > ## Valentin Werner
> > 
> > Do you have the CV discrepancy only for this experiment or for all your models? We did several experiments where it is way below 0.01 in difference, and some where its similar to yours
> > 
> > 
> > 
> > > ## James Day
> > > 
> > > All experiments.
> > > 
> > > Also, I was oversimplifying for the sake of being able to do the math in my head. A more precise estimate of what 0.902 CV translates to on the leaderboard would be 0.902*0.890 + 0.125 = 0.928. The CV-LB correlation data that is based on is included below.
> > > 
> > > 
> > > 
> > > ## ShelterW
> > > 
> > > I think it is your extra prompts that cause the relatively big difference between CV and LB.
> > > 
> > > By the way, do you use qlora or lora to finetune llm？
> > > 
> > > 
> > > 
> > > ## James Day
> > > 
> > > I use qlora.
> > > 
> > > As for the difference between my CV & LB scores, I doubt it has anything to do with the use of external training datasets not provided by the competition organizers (which I assume is what you meant by "extra prompts"), primarily because I did not observe any significant deviations from the preexisting trendline when adding extra data. I think a more likely explanation is that the data provided by the competition organizers isn't perfectly representative of their test data. For example, they may have partitioned their data based on the date on which each conversation occurred, thereby causing the test data to contain responses from new models that aren't present in the training data (or my cross validation data for that matter).
> > > 
> > > Also, one consequence of the trendline having a slope < 1 is that the discrepancies tend to get bigger as CV & LB scores improve. Extrapolating to a ridiculous extent, a model with perfect accuracy in cross validation (CV 0) would likely score ~0.125 on the leaderboard, which is a huge score discrepancy.
> > > 
> > > 
> > > 


---

> ## AbaoJiang
> 
> Hi [@takamichitoda](https://www.kaggle.com/takamichitoda),
> 
> As you mentioned, the performance of Zeroshot prediction is 1.234, which doesn't surpass the score of 1.098 by predicting the global mean.
> 
> However, it's still an interesting idea to try. Thanks for your sharing!
> 
> 
> 
> > ## Valentin Werner
> > 
> > I think the issue is in the softmax assumption without training the models first. The model has basically no intent to predict "A", "B" or "tie" whatsoever, if it not finetuned to realize it should do so. Therefore, the logits are also pretty much nonesense. 
> > 
> > This simple baseline experiment they did does not speak at all for whether their actual experiment will work or how well it will perform.
> > 
> > To me, at first glance I do not see any benefit over the seq class approach directly, as you still probably need to disable the autoregressive generation etc. But it definetly is an interesting idea
> > 
> > 
> > 
> > ## Takamichi TodaTopic Author
> > 
> > I was able to improve the score to 1.037 with SFT and Prompt Tuning. Although the classification header is still better, I intend to continue verification.
> > 
> > 
> > 
> > > ## ShelterW
> > > 
> > > I used SFT to finetune the llama3-8b and improved the LB score to 0.935 [here](https://www.kaggle.com/code/shelterw/training-llama3-8b-4-bit-qlora-sft), welcome to refer to and make suggestions.
> > > 
> > > 
> > > 


---



</div>
<div class="column-right">

# 日本語訳

# 生成ヘッダーを使用した予測
**Takamichi Toda** *2024年7月16日 火曜日 16:07:36 GMT+0900 (日本標準時)* (33票)

これはまだ試行錯誤中のアイデアであり、現在の環境ではまだ成功していませんが、共有したいと思います。

現在、公開されているコードからわかる限り、主流のアプローチはLlamaやその他のLLMをベースにしてLoRAで分類ヘッドを訓練することのようです。しかし、LLMはもともと次のトークンを予測するように訓練されているため、この方法はLLMの元の訓練から逸脱しているため、非効率的だと思います。

私のアイデアは、元のLLMと同じ生成ヘッダー（CausalLM）を使用することです。

プロンプトを調整し、トークンA、B、tieの生成確率を使用します。予測はsoftmaxを使用して後処理され、合計が1になるようにします。

以下は簡単なサンプルコードです。

```
text = """
### Instruction
Which model's answer is appropriate for the prompt?　If both are appropriate, answer `tie`.
### Prompt
{prompt text}
### A
{response A}
### B
{response B}
### Answer
"""
inputs = tokenizer(text)
out = model(inputs)
pred_token_id = tokenizer.encode("A") + tokenizer.encode("B") + tokenizer.encode("tie")
pred = out.logits[0, -1, pred_token_id].softmax(0)
```

これは、Llama3 8Bを使用してこの方法を評価するコードです。
[https://www.kaggle.com/code/takamichitoda/lmsys-zeroshot-prediction](https://www.kaggle.com/code/takamichitoda/lmsys-zeroshot-prediction)

Llama3は特別なファインチューニングを受けておらず、Kaggleモデルからロードされたまま使用されています。評価データはコンペティションデータの1/5を使用しており、これは現在の検証戦略（パブリックリーダーボードとよく相関しています）に相当します。

その結果、1.234のスコアを得ました。ZeroShotでこのような結果を得ることができるとは驚きでした。

現在、コンペティションデータでSFTを実行し、プロンプトを調整しています。しかし、分類ヘッドを学習するモデルの方がまだスコアが良いです。

同様のアプローチに取り組んでいる人はいますか？

---
# 他のユーザーからのコメント
> ## James Day
> 
> 私は同様の実験を試みました。主な理由は、HuggingFace transformersライブラリよりも高速でメモリ効率の高い、因果言語モデルの訓練と推論ライブラリ（unslothやvLLMなど）を活用したいと思ったからです。しかし、[@takamichitoda](https://www.kaggle.com/takamichitoda)の初期の実験のようにゼロショット推論を行うのではなく、実際にはLLMをファインチューニングしました。
> 
> Llama 3 8B Instructで次のトークン予測を行い、0.902（CV）を取得しました。これは、私が「通常の」Llama 3ベースの分類モデルで得ているスコアとほぼ同じです。しかし、同じアプローチはGemma 2 9B（0.990 CV 🤮）ではうまく機能しませんでした。これは、Gemmaのタイド埋め込みが原因である可能性があります。私のCVスコアは、対応するLBスコアよりも常に約0.03低いため、これらの結果はLBで約0.93と1.02になります。これは、提出するほど良くありません。
> 
> 
> 
> > ## Takamichi Todaトピック作成者
> > 
> > 共有していただきありがとうございます。
> > 
> > 0.9は私にとって素晴らしいスコアです ;)
> > 
> > ところで、可能であれば、ファインチューニングにどのようなプロンプトを使用したか教えていただけますか？
> > 
> > 私はtrlのSFTTrainerを使用しており、DataCollatorForCompletionOnlyLMを使用して出力のみを学習しています。
> > 
> > 
> > > ## James Day
> > > 
> > > 次のようなプロンプトを使用しました。
> > > 
> > > ```
> > > 以下のチャットボットのどちらが、ユーザーのリクエストへの応答をより適切に行いましたか？それとも同等でしたか？
> > > 
> > > ~~~~~~~~~~ BOT Aとの会話 ~~~~~~~~~~
> > > 
> > > ### ユーザー: "{初期プロンプト}"
> > > 
> > > ### BOT Aの応答: "{初期応答}"
> > > 
> > > ### ユーザー: "{フォローアッププロンプトがある場合は、3kトークンのコンテキストウィンドウに収まる会話ターンをできるだけ多く含め、必要に応じて各会話の最初の部分を破棄します}"
> > > 
> > > ### BOT Aの応答: "{フォローアップ応答}"
> > > 
> > > ~~~~~~~~~~ BOT Bとの会話 ~~~~~~~~~~
> > > 
> > > ### ユーザー: "{...}"
> > > 
> > > ### BOT Bの応答: "{...}"
> > > 
> > > ### ユーザー: "{...}"
> > > 
> > > ### BOT Bの応答: "{...}"
> > > 
> > > ### 最良の応答:
> > > 
> > > ```
> > > 
> > > これは、" A"、" B"、または" Tie"を出力するように訓練されました。スペースは応答トークンの一部でした。
> > > 
> > > 
> > > 
> > ## Valentin Werner
> > 
> > この実験のみ、またはすべてのモデルでCVのずれが発生していますか？私たちは、ずれが0.01をはるかに下回る実験をいくつか行い、あなたのものと同様のずれが発生する実験もいくつか行いました。
> > 
> > 
> > > ## James Day
> > > 
> > > すべての実験です。
> > > 
> > > また、頭の中で計算できるようにするために、単純化していました。リーダーボードで0.902 CVがどの程度になるかのより正確な推定値は、0.902*0.890 + 0.125 = 0.928です。この推定値は、以下のCV-LB相関データに基づいています。
> > > 
> > > 
> > > 
> > > ## ShelterW
> > > 
> > > 私は、CVとLBの間に比較的大きな差が生じているのは、追加のプロンプトが原因だと思います。
> > > 
> > > ところで、LLMのファインチューニングにqloraまたはloraを使用していますか？
> > > 
> > > 
> > > 
> > > ## James Day
> > > 
> > > qloraを使用しています。
> > > 
> > > CVとLBのスコアの差については、コンペティション主催者によって提供されていない外部訓練データの使用（「追加のプロンプト」の意味だと思います）が原因であるとは考えていません。これは、追加データを追加しても、既存のトレンドラインから有意な偏差が観察されなかったためです。より可能性の高い説明は、コンペティション主催者によって提供されたデータが、彼らのテストデータと完全に一致していないということです。たとえば、彼らは各会話が行われた日付に基づいてデータを分割している可能性があり、その結果、テストデータには、訓練データ（または私の交差検証データ）には存在しない新しいモデルからの応答が含まれることになります。
> > > 
> > > また、トレンドラインの傾きが1未満であることの1つの結果は、CVとLBのスコアが向上するにつれて、ずれが大きくなる傾向があるということです。ばかげたまでに外挿すると、交差検証で完全な精度を持つモデル（CV 0）は、リーダーボードで約0.125のスコアになる可能性があり、これは非常に大きなスコアずれです。
> > > 
> > > 
> > > 
---
> ## AbaoJiang
> 
> [@takamichitoda](https://www.kaggle.com/takamichitoda)さん、こんにちは。
> 
> あなたが言及したように、ゼロショット予測のパフォーマンスは1.234であり、グローバル平均を予測することによる1.098のスコアを上回っていません。
> 
> しかし、それでも試してみる価値のある興味深いアイデアです。共有していただきありがとうございます！
> 
> 
> 
> > ## Valentin Werner
> > 
> > 私は、モデルを最初に訓練せずにsoftmaxを仮定することが問題だと思います。モデルは、最初にファインチューニングされて、"A"、"B"、または"tie"を予測する必要があることを認識していない限り、"A"、"B"、または"tie"を予測する意図はほとんどありません。そのため、ロジットもほとんどナンセンスです。
> > 
> > 彼らが行ったこの単純なベースライン実験は、実際の実験が機能するかどうか、またはどの程度うまく機能するのかについて、何も語っていません。
> > 
> > 私にとって、一見したところ、シーケンス分類アプローチよりもメリットは見られません。なぜなら、おそらく自動回帰生成などを無効にする必要があるからです。しかし、間違いなく興味深いアイデアです。
> > 
> > 
> > > ## Takamichi Todaトピック作成者
> > > 
> > > SFTとプロンプトチューニングでスコアを1.037に改善することができました。分類ヘッドの方がまだ優れていますが、検証を続けるつもりです。
> > > 
> > > 
> > > > ## ShelterW
> > > > 
> > > > Llama3-8bをファインチューニングするためにSFTを使用し、LBスコアを0.935に改善しました。[こちら](https://www.kaggle.com/code/shelterw/training-llama3-8b-4-bit-qlora-sft)を参照して、ご意見をお寄せください。
> > > > 
> > > > 
> > > > 
---




</div>