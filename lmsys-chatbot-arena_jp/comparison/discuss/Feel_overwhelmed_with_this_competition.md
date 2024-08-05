# 要約 
このKaggleコンペティションのディスカッションは、参加者たちが、特に学生にとって、コンペティションで成功するために必要な計算リソースの不足に苦労していることを示しています。

**主なポイント:**

* **計算リソースの不足:** 参加者は、大規模言語モデル（LLM）をトレーニングするために必要な計算能力が不足しているため、コンペティションで成功するために苦労しています。
* **DeBERTa vs. LLM:** 参加者は、DeBERTaのようなより小さなモデルよりもLLMの方がパフォーマンスが優れている可能性があると考えていますが、LLMのトレーニングには膨大な計算リソースが必要になります。
* **費用:** LLMのトレーニングには、学生にとって高価なクラウドコンピューティングサービスの利用が必要になります。
* **Kaggleの無料GPU:** 参加者は、Kaggleの無料GPUに頼っていますが、それらは限られており、コンペティションで成功するために必要な計算能力を提供するのに十分ではありません。
* **解決策:** 参加者は、クラウドコンピューティングサービスのレンタル、大学や教授からのリソースの利用、またはKaggleがより高性能なハードウェアに投資することを提案しています。

**結論:**

このディスカッションは、Kaggleコンペティションが、特に学生にとって、計算リソースの不足によってますます困難になっていることを示しています。参加者は、コンペティションで成功するために必要なリソースへのアクセスを改善するための解決策を求めています。


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

# Feel overwhelmed with this competition  

**ducnh279** *Thu Jul 04 2024 04:37:33 GMT+0900 (日本標準時)* (13 votes)

Hi everyone,

Unlike other NLP competitions I've participated in, I believe that decoder-only models might outperform DeBERTa in this one. Running experiments with LLMs is very computationally and financially expensive for me, especially in this competition.

- For DeBERTa (large), I can manage to get LB: 0.993 (tuned) with 6-hour training using 2 x T4 on Kaggle

- For LLMs,  I've just run only one experiment with Mistral 7B (4-bit quantized + LoRA) and got LB: 0.991. 

For fine-tuning LLMs, one experiment is very slow and expensive to finish one fold in 15 hours with 1 A10G on Lightning Studios. If there is no special magic to get 0.9 to 0.95. I believe that by tuning (batch size, learning rate, warm-up steps, prompts), trying training tricks to stablize the training and avoid early performance saturation, or simply being able to run more than 1 epoch, I think I could get closer to LB: <= 0.95.

As a student, I find Kaggle competitions increasingly challenging and computationally expensive, particularly due to the limited access to free hardware. Relying on free GPUs from Kaggle and Colab, I often feel constrained and overwhelmed when competing.

Do you think I need to invest big bucks for this competition to pay off? As a broke student, I might have to hit up the Bank of Mom and Dad for a 'strategic investment'  haha😂



---

 # Comments from other users

> ## kagglethebest
> 
> Same feeling. 😂 I am trying to find a way to get nice score by using Deberta Base on Kaggle GPUs. If my trials are not worked, I will give up this competition.
> 
> 
> 
> > ## ducnh279Topic Author
> > 
> > Don't give up [@judith007](https://www.kaggle.com/judith007)! Let's fight until the last minute!
> > 
> > By the way, I recommend trying DeBERTa large and learning how to utilize two GPUs. I achieved a 0.988 score with DeBERTa large, which is the same score as the first public notebook using the 8-bit quantized LLaMA 8B.
> > 
> > 
> > 


---

> ## Valentin Werner
> 
> 
> 
> 
> 
> > ## Valentin Werner
> > 
> > Jokes aside, always prefer training models on hosted rental services rather than buying an expensive GPU. You can first validate on the slow kaggle GPUs / TPU or Google Collab etc. before going to the rental. The math for buying a 3090TI / 4080 / 4090 for Data Science it is not really mathing. I have a 4090 which is great for experiments, but I still cannot scale to the same experiments as the Kaggle TPU on it. 
> > 
> > It feels really bad being gates by compute resources. Stuff you can try out if renting is not an option: Some cloud providers provide research compute for limited time; you can ask your university / professors if they have compute you can do (maybe try to sell it as extra curicular, present your results in the end for some bonus points; my university had a 4x V100 setup with 128GB total that was mostly idling and my professor almost begged me to train some stuff on there so its used when nobody does research); 
> > 
> > 
> > 
> > > ## ducnh279Topic Author
> > > 
> > > Hahaha your meme tells my story! 
> > > 
> > > After this competition, I would learn about TPU training! Thanks SO much for sharing your experience!
> > > 
> > > 
> > > 


---

> ## Cody_Null
> 
> Glad someone else was able to get 7b models like mistral working in 4bit. Mine had a bug but didn’t seem like it was going to beat the llama models anyway :/ I understand your position though. It does feel that way sometime 
> 
> 
> 
> > ## ducnh279Topic Author
> > 
> > Thanks for your understanding! For sure, 7b models quantized in 4-bit will be definitely degraded in performance. You can use scaling law to set up the hyparams and try training techniques before running on the whole training set. Sorry I can't talk more about this before the competition ends.
> > 
> > 
> > 


---

> ## Taimo
> 
> Kaggle is a good starting point for students.
> 
> For educational purposes, Kaggle should remain such a place even though the size of models continues to be big. 
> 
> Google (Alphabet) should invest in more high-spec hardware for Kaggle.
> 
> 
> 
> > ## ducnh279Topic Author
> > 
> > For educational purposes, Kaggle should remain such a place even though the size of models continues to be big.
> > 
> > Agreed! I learned a lot through Kaggle competitions and the sharings from Kagglers! The "large" in models and datasets are not a too big problem with me! I will definitely continue learning and competing.
> > 
> > Google (Alphabet) should invest in more high-spec hardware for Kaggle.
> > 
> > We all hope so! hahaha
> > 
> > 
> > 


---

> ## xiaotingting
> 
> After I became a graduate student, I was fine and could use the server in the lab. But because I had to submit a paper recently and needed to do additional experiments, and there were other people in the lab using the server, I could only use it when they were not using it. If I want to fine-tune a large model, I really need a card. I currently rent two A100 cards to prepare for the experiments here, and each training takes at least two days. It is more cost-effective to rent it for the whole day, about 200 yuan for two cards a day, and it costs more than a thousand yuan to rent it for a week.
> 
> 
> 
> > ## KeShuang Liu
> > 
> > I was interning at the company and they provided me with two A800s, but due to my technical issues, I was unable to achieve good results.
> > 
> > 
> > 


---



</div>
<div class="column-right">

# 日本語訳

# このコンペティションに圧倒されている

**ducnh279** *2024年7月4日 木曜日 04:37:33 GMT+0900 (日本標準時)* (13 votes)
皆さん、こんにちは！

これまで参加してきた他のNLPコンペティションとは異なり、このコンペティションでは、デコーダーのみのモデルがDeBERTaよりも優れた性能を発揮する可能性があると信じています。特にこのコンペティションでは、LLMを使った実験は、私にとって計算量と費用面で非常に負担が大きいです。

- DeBERTa（large）の場合、Kaggleの2 x T4を使って6時間のトレーニングでLB: 0.993（チューニング済み）を達成できます。
- LLMの場合、Mistral 7B（4ビット量子化 + LoRA）で1回だけ実験を行ったところ、LB: 0.991でした。
LLMのファインチューニングでは、Lightning Studiosの1 A10Gを使って1つのフォールドを完了するのに15時間もかかり、1回の実験が非常に遅く、費用がかかります。もし、0.9から0.95に到達するための特別な魔法がなければ、バッチサイズ、学習率、ウォーミングアップステップ、プロンプトのチューニング、トレーニングを安定させ、早期のパフォーマンス飽和を回避するためのトレーニングトリックを試したり、単に1エポック以上を実行したりすることで、LB: <= 0.95に近づけることができると考えています。

学生である私は、特に無料のハードウェアへのアクセスが限られているため、Kaggleコンペティションがますます困難で計算量も増大していると感じています。KaggleとColabの無料GPUに頼っているため、競争する際にしばしば制約を感じ、圧倒されてしまいます。

このコンペティションで大きなお金を投資する必要があると思いますか？お金のない学生として、"戦略的投資"のために親に頼らなければならないかもしれません。😂

---
# 他のユーザーからのコメント

> ## kagglethebest
> 
> 同じ気持ちです。😂 KaggleのGPUを使ってDeberta Baseで良いスコアを出す方法を探しています。もし試行がうまくいかなかったら、このコンペティションは諦めます。
> 
> 
> 
> > ## ducnh279トピック作成者
> > 
> > 諦めないでください [@judith007](https://www.kaggle.com/judith007)! 最後まで戦いましょう！
> > 
> > ちなみに、DeBERTa largeを試して、2つのGPUの使い方を学ぶことをお勧めします。DeBERTa largeで0.988のスコアを達成しましたが、これは8ビット量子化されたLLaMA 8Bを使った最初の公開ノートブックと同じスコアです。
> > 
> > 
> > 
---
> ## Valentin Werner
> 
> 
> 
> 
> 
> > ## Valentin Werner
> > 
> > 冗談はさておき、高価なGPUを購入するよりも、ホストされたレンタルサービスでモデルをトレーニングすることを常に優先してください。レンタルに移行する前に、まずKaggleのGPU / TPUやGoogle Collabなどでゆっくりと検証することができます。データサイエンスのために3090TI / 4080 / 4090を購入する計算は、実際にはうまくいきません。私は4090を持っていますが、実験には最適ですが、それでもKaggleのTPUと同じ実験にはスケールできません。
> > 
> > 計算リソースによって制限されるのは、本当に気分が悪いです。レンタルができない場合に試せること：一部のクラウドプロバイダーは、期間限定でリサーチ用のコンピューティングを提供しています。大学や教授に、利用できるコンピューティングがあるかどうか尋ねてみてください（もしかしたら、課外活動として売り込み、結果を最後に発表してボーナス点を獲得できるかもしれません。私の大学には、ほとんどアイドル状態の4x V100セットアップ（合計128GB）があり、教授はほとんど私にお願いして、誰も研究をしていないときに何かをトレーニングするように頼んでいました）。
> > 
> > 
> > 
> > > ## ducnh279トピック作成者
> > > 
> > > あなたのミームは私の物語を語っています！
> > > 
> > > このコンペティションが終わったら、TPUトレーニングについて学びます！経験を共有してくれて本当にありがとう！
> > > 
> > > 
> > > 
---
> ## Cody_Null
> 
> 他の誰かがMistralのような7Bモデルを4ビットで動作させることができたのは嬉しいです。私のモデルにはバグがありましたが、それでもLLamaモデルを上回ることはなさそうでした。でも、あなたの立場はよく分かります。時々そう感じます。
> 
> 
> 
> > ## ducnh279トピック作成者
> > 
> > ご理解ありがとうございます！確かに、4ビットで量子化された7Bモデルは、パフォーマンスが確実に低下します。スケーリング則を使ってハイパラムを設定し、トレーニングテクニックを試してから、トレーニングセット全体で実行することができます。コンペティションが終わるまでは、これ以上は話せません。
> > 
> > 
> > 
---
> ## Taimo
> 
> Kaggleは学生にとって良い出発点です。
> 
> モデルのサイズが大きくなり続けても、教育目的のために、Kaggleはそういう場所であり続けるべきです。
> 
> Google（Alphabet）は、Kaggleのためにより高性能なハードウェアに投資すべきです。
> 
> 
> 
> > ## ducnh279トピック作成者
> > 
> > 教育目的のために、Kaggleはモデルのサイズが大きくなり続けても、そういう場所であり続けるべきです。
> > 
> > 同意です！KaggleコンペティションとKagglersからの共有を通して、多くのことを学びました！"large"というモデルとデータセットは、私にとってそれほど大きな問題ではありません！これからも学び続け、競争を続けていきます。
> > 
> > Google（Alphabet）は、Kaggleのためにより高性能なハードウェアに投資すべきです。
> > 
> > みんなそう願っています！hahaha
> > 
> > 
> > 
---
> ## xiaotingting
> 
> 大学院生になってからは、ラボのサーバーを使えて問題ありませんでした。しかし、最近論文を提出する必要があり、追加の実験を行う必要があったため、ラボの他のメンバーがサーバーを使っていたため、彼らが使っていないときしか使えませんでした。大きなモデルをファインチューニングしたい場合は、本当にカードが必要です。現在、この実験の準備のために2枚のA100カードをレンタルしており、トレーニングにはそれぞれ少なくとも2日かかります。1日中レンタルする方が費用対効果が高く、2枚のカードで1日約200元、1週間レンタルすると1000元以上かかります。
> 
> 
> 
> > ## KeShuang Liu
> > 
> > 私は会社でインターンをしていて、2枚のA800を提供されましたが、技術的な問題のため、良い結果を得ることができませんでした。
> > 
> > 
> > 
---



</div>