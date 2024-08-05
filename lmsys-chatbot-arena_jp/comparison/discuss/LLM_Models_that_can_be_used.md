# 要約 
このKaggleコンペティションのディスカッションは、参加者が使用しているLLMモデルとそのパフォーマンスについて議論しています。

**主なポイント:**

* **superferg**は、Llama3-8B、Gemma2-9Bなどのモデルを試した結果を共有し、Gemma2-9Bが異常な結果を示したことを報告しました。
* **Valentin Werner**は、Gemma2-9Bが新しいモデルであり、パフォーマンスが優れていることを指摘しました。
* **Cody_Null**は、Gemma2-9BをHugging FaceからKaggleに引っ張ってきたかどうかを尋ねました。
* **s111mple**は、ファインチューニングされたモデルがうまく機能しないかどうかを尋ねました。
* **xiaotingting**は、検証セットのインデックスがパブリックスコアと正の相関関係にあることを指摘しました。
* **lllleeeo**は、ファインチューニングに必要なパラメータ数の決定方法について質問しました。
* **Mr.T**は、Gemma2-9Bの推論方法について質問しました。
* **EISLab_hwlee**は、Gemma2-27B-instructモデルのパフォーマンスについて質問しました。
* **hn**は、Gemma2の推論結果が不十分だった原因について質問しました。
* **Mukatai**は、Gemma2のファインチューニングにおけるスコアの違いについて質問しました。
* **Femca7**は、結果が事前トレーニング済みモデルかファインチューニング済みモデルかについて質問しました。
* **yechenzhi1**は、Instructモデルがベースモデルよりも優れているかどうかを尋ねました。

**結論:**

このディスカッションは、参加者がコンペティションで使用するLLMモデルについて、さまざまな質問や意見を共有しています。特に、Gemma2-9Bモデルのパフォーマンスとファインチューニングに関する議論が活発に行われています。参加者は、モデルの選択、推論方法、ファインチューニングなど、さまざまな側面について情報交換し、互いに学び合っています。


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

# LLM Models that can be used

**superferg** *Sat Jul 06 2024 21:28:26 GMT+0900 (日本標準時)* (26 votes)

May I ask which models everyone has tried? I tried the following model，Randomly select 20% of the samples as the validation set.：

| Model | Local Validation | Public Leaderboard |
| --- | --- | --- |
| Llama3-8B-instruct | 0.9419 | 0.954 |
| Llama3-8B | 0.9818 | 0.987 |
| Gemma2-9B-instruct | 0.9262 | 1.206 |
| Gemma2-9B | 0.9499 | 1.299 |

Gemma2-9B has obtained abnormal results, I guess it might be a problem with the inference. Does anyone have similar problems?

UPDATE:

With the [new public notebook](https://www.kaggle.com/code/emiz6413/inference-gemma-2-9b-4-bit-qlora), the correct results were obtained.

| Model | Local Validation | Public Leaderboard |
| --- | --- | --- |
| Llama3-8B-instruct | 0.9419 | 0.954 |
| Llama3-8B | 0.9818 | 0.987 |
| Gemma2-9B-instruct | 0.9262 | 0.930 |
| Gemma2-9B | 0.9499 | TODO… |


---

 # Comments from other users

> ## Valentin Werner
> 
> gonna leave this one here 😉
> 
> 
> 
> > ## superfergTopic Author
> > 
> > The current local validation set is 0.91X, I still can't migrate to LB. LoL
> > 
> > 
> > 
> > ## SAY WHAT
> > 
> > so funny！！！
> > 
> > 
> > 


---

> ## Valentin Werner
> 
> Gemma2-9B came out recently. The 9B makes it even harder to train, but it tops the performance benchmarks among these models
> 
> 
> 
> > ## Cody_Null
> > 
> > Were you able to pull the gemma2-9B into kaggle from huggingface or are you using the Gemma 2 · gemma-2-9b-pt · V1 on kaggle models? 
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > We pulled gemma2-9b from huggingface into kaggle.
> > > 
> > > 
> > > 
> > ## s111mple
> > 
> > Finetuned model donnot get fine results~ Have you tried it?
> > 
> > 
> > 


---

> ## xiaotingting
> 
> It seems that the validation set index is positively correlated with the public score, and there is still room for further improvement of the index.
> 
> 
> 


---

> ## Xiot1206
> 
> thanks for providing these key information
> 
> 
> 


---

> ## lllleeeo
> 
> As an nlp newbie, I'd like to ask a possibly stupid question, how did you determine how many parameters you needed to use to participate in the fine-tuning, did you try them one by one? How much is generally best based on experience, is it different for different models, I observed that the public laptop fine-tuning in liama 8b only used 0.02% of the parameters is this too little?
> 
> 
> 
> > ## superfergTopic Author
> > 
> > If there is not enough computing power, using the Lora fine-tuning method may be the only choice.
> > 
> > 
> > 
> > > ## lllleeeo
> > > 
> > > Thanks for your reply! I've rented an A100 and a 4090 and want to do some experiments in parallel, I'm wondering if I can try more parameters based on that computing power, but I'm not sure how much I should start trying.
> > > 
> > > 
> > > 
> > > ## superfergTopic Author
> > > 
> > > The first step can try the top-level public notebook.
> > > 
> > > 
> > > 
> > > ## lllleeeo
> > > 
> > > Thank you it works！
> > > 
> > > 
> > > 


---

> ## Mr.T
> 
> How do you load gemma 2-9b during inference?
> 
> 
> 
> > ## superfergTopic Author
> > 
> > Please refer to the notebook below：
> > 
> > [https://www.kaggle.com/code/emiz6413/inference-gemma-2-9b-4-bit-qlora](https://www.kaggle.com/code/emiz6413/inference-gemma-2-9b-4-bit-qlora)
> > 
> > 
> > 


---

> ## EISLab_hwlee
> 
> Can the Gemma2-27B-instruct model perform better?
> 
> 
> 
> > ## EISLab_hwlee
> > 
> > As a result of the experiment, it was observed that the performance was poor.
> > 
> > 
> > 
> > > ## superfergTopic Author
> > > 
> > > I still can't complete the reasoning of 27B within 9 hours, theoretically, 27B should achieve better results.
> > > 
> > > 
> > > 
> > > ## EISLab_hwlee
> > > 
> > > I also failed to submit it.
> > > 
> > > However, in training, the loss did not fall below 1.0, and the evaluation loss did not fall below 1.0.
> > > 
> > > 
> > > 


---

> ## hn
> 
> Just curious, what was the missing piece that lead to your poor inference results from Gemma2? I see that you mentioned it’s fixed with the public notebook 
> 
> 
> 
> > ## superfergTopic Author
> > 
> > I don't have enough time to figure out the reason, but you can analyze the reason by comparing the following two notebooks.
> > 
> > [https://www.kaggle.com/code/emiz6413/llama-3-8b-38-faster-inference](https://www.kaggle.com/code/emiz6413/llama-3-8b-38-faster-inference)
> > 
> > [https://www.kaggle.com/code/emiz6413/inference-gemma-2-9b-4-bit-qlora](https://www.kaggle.com/code/emiz6413/inference-gemma-2-9b-4-bit-qlora)
> > 
> > 
> > 


---

> ## Mukatai
> 
> In a recent public notebook, a score of 0.941 was recorded with fine-tuning of Gemma2, but this table shows a score of 0.930 with Gemma2-9B-instruct. Is there any difference?
> 
> 
> 
> > ## superfergTopic Author
> > 
> > I am using my own training script, so there should be some differences, I can make it public after the competition ends.
> > 
> > 
> > 
> > > ## Mukatai
> > > 
> > > Thank you. Is Gemma's training conducted on Kaggle? With a public notebook, training on a single dataset exceeds the 30-hour weekly limit
> > > 
> > > 
> > > 


---

> ## Femca7
> 
> May I ask the results you get is from pre-trained or finetuned model ?
> 
> 
> 
> > ## superfergTopic Author
> > 
> > You can see the details in the table I provided, those with an 'instruct' suffix are fine-tuned models.
> > 
> > 
> > 


---

> ## yechenzhi1
> 
> May I ask if Instruct model is better than the base model? I have only tried Instruct model.
> 
> 
> 
> > ## superfergTopic Author
> > 
> > According to my local testing, Llama3-8B instruct is better than Llama3-8B. But perhaps the appropriate hyperparameters for  Llama3-8B have not been found.
> > 
> > 
> > 
> > ## ducnh279
> > 
> > I also had a similar question in the early days when I started with fine-tuning decoder-only models for text classification! 
> > 
> > I asked [@rasbtn](https://www.kaggle.com/rasbtn) (a prominent researcher/educator) on Twitter! He replied:
> > 
> > I also conducted some experiments, and the results indicate that using instruction-tuned versions often gives better performance and faster convergence compared to the base model.
> > 
> > 
> > 
> > > ## yechenzhi1
> > > 
> > > Thanks! That's really helpful!
> > > 
> > > 
> > > 


---



</div>
<div class="column-right">

# 日本語訳

# 使用可能なLLMモデル

**superferg** *2024年7月6日 土曜日 21:28:26 JST* (26票)

皆さん、どのモデルを試しましたか？私は以下のモデルを試しました。サンプルの20%をランダムに選択して検証セットとして使用しました。

| モデル | ローカル検証 | パブリックリーダーボード |
|---|---|---|
| Llama3-8B-instruct | 0.9419 | 0.954 |
| Llama3-8B | 0.9818 | 0.987 |
| Gemma2-9B-instruct | 0.9262 | 1.206 |
| Gemma2-9B | 0.9499 | 1.299 |

Gemma2-9Bは異常な結果を得ています。推論に問題があるのかもしれません。同様の問題を抱えている人はいますか？

**更新:**

[新しいパブリックノートブック](https://www.kaggle.com/code/emiz6413/inference-gemma-2-9b-4-bit-qlora)を使用すると、正しい結果が得られました。

| モデル | ローカル検証 | パブリックリーダーボード |
|---|---|---|
| Llama3-8B-instruct | 0.9419 | 0.954 |
| Llama3-8B | 0.9818 | 0.987 |
| Gemma2-9B-instruct | 0.9262 | 0.930 |
| Gemma2-9B | 0.9499 | TODO… |

---
# 他のユーザーからのコメント

> ## Valentin Werner
> 
> これだけはお伝えしておきます 😉
> 
> 
> 
> > ## superfergトピック作成者
> > 
> > 現在のローカル検証セットは0.91Xです。まだLBに移行できません。LoL
> > 
> > 
> > 
> > ## SAY WHAT
> > 
> > 面白いですね！！！
> > 
> > 
> > 
---
> ## Valentin Werner
> 
> Gemma2-9Bは最近登場しました。9Bはトレーニングをさらに難しくしますが、これらのモデルの中でパフォーマンスベンチマークでトップに立っています。
> 
> 
> 
> > ## Cody_Null
> > 
> > Gemma2-9BをHugging FaceからKaggleに引っ張ってくることができましたか？それともKaggleモデルのGemma 2 · gemma-2-9b-pt · V1を使用していますか？
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > Gemma2-9BをHugging FaceからKaggleに引っ張ってきました。
> > > 
> > > 
> > > 
> > ## s111mple
> > 
> > ファインチューニングされたモデルは良い結果が得られません。試しましたか？
> > 
> > 
> > 
---
> ## xiaotingting
> 
> 検証セットのインデックスはパブリックスコアと正の相関関係にあるようで、インデックスをさらに改善する余地があります。
> 
> 
> 
---
> ## Xiot1206
> 
> この重要な情報を提供していただきありがとうございます。
> 
> 
> 
---
> ## lllleeeo
> 
> NLP初心者なので、もしかしたらばかげた質問かもしれませんが、ファインチューニングに参加するために必要なパラメータ数をどのように決定しましたか？一つずつ試しましたか？経験に基づいて一般的にどれくらいが最適ですか？モデルによって異なりますか？私はLlama 8bのパブリックラップトップのファインチューニングでパラメータの0.02%しか使用していないことに気づきましたが、これは少なすぎませんか？
> 
> 
> 
> > ## superfergトピック作成者
> > 
> > 十分なコンピューティングパワーがない場合は、LoRAファインチューニング方法を使用するしかないかもしれません。
> > 
> > 
> > 
> > > ## lllleeeo
> > > 
> > > 返信ありがとうございます！A100と4090をレンタルして、並行して実験を行いたいのですが、そのコンピューティングパワーに基づいてより多くのパラメータを試せるかどうかが気になっています。しかし、どのくらいから試すべきか分かりません。
> > > 
> > > 
> > > 
> > > ## superfergトピック作成者
> > > 
> > > 最初はトップレベルのパブリックノートブックを試すことができます。
> > > 
> > > 
> > > 
> > > ## lllleeeo
> > > 
> > > ありがとうございます！うまくいきました！
> > > 
> > > 
> > > 
---
> ## Mr.T
> 
> 推論中にGemma 2-9bをどのようにロードしますか？
> 
> 
> 
> > ## superfergトピック作成者
> > 
> > 以下のノートブックを参照してください。
> > 
> > [https://www.kaggle.com/code/emiz6413/inference-gemma-2-9b-4-bit-qlora](https://www.kaggle.com/code/emiz6413/inference-gemma-2-9b-4-bit-qlora)
> > 
> > 
> > 
---
> ## EISLab_hwlee
> 
> Gemma2-27B-instructモデルはパフォーマンスが向上しますか？
> 
> 
> 
> > ## EISLab_hwlee
> > 
> > 実験の結果、パフォーマンスが低いことが分かりました。
> > 
> > 
> > 
> > > ## superfergトピック作成者
> > > 
> > > 9時間以内に27Bの推論を完了することができません。理論的には、27Bはより良い結果を達成するはずです。
> > > 
> > > 
> > > 
> > > ## EISLab_hwlee
> > > 
> > > 私も提出できませんでした。
> > > 
> > > しかし、トレーニングでは損失が1.0を下回らず、評価損失も1.0を下回りませんでした。
> > > 
> > > 
> > > 
---
> ## hn
> 
> 単なる好奇心ですが、Gemma2の推論結果が不十分だった原因は何でしたか？パブリックノートブックで修正されたと書いてありました。
> 
> 
> 
> > ## superfergトピック作成者
> > 
> > 時間がないので理由は分かりませんが、以下の2つのノートブックを比較することで原因を分析できます。
> > 
> > [https://www.kaggle.com/code/emiz6413/llama-3-8b-38-faster-inference](https://www.kaggle.com/code/emiz6413/llama-3-8b-38-faster-inference)
> > 
> > [https://www.kaggle.com/code/emiz6413/inference-gemma-2-9b-4-bit-qlora](https://www.kaggle.com/code/emiz6413/inference-gemma-2-9b-4-bit-qlora)
> > 
> > 
> > 
---
> ## Mukatai
> 
> 最近のパブリックノートブックでは、Gemma2のファインチューニングで0.941のスコアが記録されていますが、この表ではGemma2-9B-instructで0.930のスコアが表示されています。違いはありますか？
> 
> 
> 
> > ## superfergトピック作成者
> > 
> > 私は独自のトレーニングスクリプトを使用しているので、多少の違いがあるはずです。コンペティション終了後に公開できます。
> > 
> > 
> > 
> > > ## Mukatai
> > > 
> > > ありがとうございます。GemmaのトレーニングはKaggleで行われていますか？パブリックノートブックでは、単一のデータセットでのトレーニングは週ごとの30時間の制限を超えてしまいます。
> > > 
> > > 
> > > 
---
> ## Femca7
> 
> 取得した結果は、事前トレーニング済みモデルですか？それともファインチューニング済みモデルですか？
> 
> 
> 
> > ## superfergトピック作成者
> > 
> > 提供した表に詳細が記載されています。'instruct'というサフィックスが付いているものは、ファインチューニング済みモデルです。
> > 
> > 
> > 
---
> ## yechenzhi1
> 
> Instructモデルはベースモデルよりも優れているのでしょうか？私はInstructモデルしか試していません。
> 
> 
> 
> > ## superfergトピック作成者
> > 
> > ローカルテストによると、Llama3-8B instructはLlama3-8Bよりも優れています。しかし、Llama3-8Bに適したハイパーパラメータが見つかっていないのかもしれません。
> > 
> > 
> > 
> > ## ducnh279
> > 
> > テキスト分類のためにデコーダーのみのモデルのファインチューニングを始めたばかりの頃、私も同様の質問をしました！
> > 
> > Twitterで[@rasbtn](https://www.kaggle.com/rasbtn)（著名な研究者/教育者）に質問しました！彼はこう答えました。
> > 
> > 私もいくつかの実験を行い、その結果、インストラクションチューニングされたバージョンを使用すると、ベースモデルと比較してパフォーマンスが向上し、収束が速くなることがよくあります。
> > 
> > 
> > 
> > > ## yechenzhi1
> > > 
> > > ありがとうございます！とても役に立ちます！
> > > 
> > > 
> > > 
---



</div>