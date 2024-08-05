# 要約 
このディスカッションは、Mistral-NeMo 12B のリリースに関するものです。このモデルは、Gemma2 9B および Llama3 8B を凌駕し、128K のコンテキストウィンドウ、100 以上の言語に対応する多言語モデル、FP8 での量子化対応トレーニング、Apache 2.0 ライセンスなどの特徴を持っています。

しかし、ユーザーからのコメントでは、transformers ライブラリでのファインチューニングに問題があることが指摘されています。James Day は、ファインチューニングが壊れている可能性があり、修正がすぐにリリースされる予定であると述べています。Lorry Zou は、インストラクトモデルをファインチューニングした結果、Gemma2 9b に匹敵するレベルには達していないと報告しています。Valentin Werner は、これは James が言及したバグが原因である可能性があると指摘しています。Eisuke Mizutani は、最新の transformers をインストールすることでエラーなしでトレーニングを実行できたものの、結果は Llama3 よりも悪かったと報告しています。

他のユーザーは、コードの実装が難しいことや、コンペティションの残り 5 週間で新しいモデルが続々とリリースされていることを指摘しています。Valentin Werner は、GenAI の盛り上がりは、モデリング技術ではなく、企業がたまたま高品質なモデルをリリースしたという偶然の産物である可能性があると述べています。

全体的に、このディスカッションは、Mistral-NeMo 12B のリリースとそのパフォーマンスに関する初期のフィードバックを提供しています。ユーザーは、モデルの潜在的な問題点や、コンペティションにおける GenAI の進化について議論しています。


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

# Mistral-NeMo release

**Ashwani** *Fri Jul 19 2024 01:09:26 GMT+0900 (日本標準時)* (22 votes)

Mistral-NeMo 12B released 

- Outperforms Gemma2 9B and Llama3 8B

- 128K context window

- Multilingual in 100+ languages: excels in European, Asian & Indian languages

- Quantization-Aware Training at FP8

- Apache 2.0 license

Blog: [https://mistral.ai/news/mistral-nemo/](https://mistral.ai/news/mistral-nemo/)

HF Weights (Base): [https://huggingface.co/mistralai/Mistral-Nemo-Base-2407](https://huggingface.co/mistralai/Mistral-Nemo-Base-2407)

HF Weights (Instruct): [https://huggingface.co/mistralai/Mistral-Nemo-Instruct-2407](https://huggingface.co/mistralai/Mistral-Nemo-Instruct-2407)



---

 # Comments from other users

> ## James Day
> 
> FYI, it appears finetuning for Mistral-NeMo is currently broken in the transformers library (see [https://huggingface.co/mistralai/Mistral-Nemo-Instruct-2407/discussions/6](https://huggingface.co/mistralai/Mistral-Nemo-Instruct-2407/discussions/6)). A fix should be released soon ([https://github.com/huggingface/transformers/pull/32065](https://github.com/huggingface/transformers/pull/32065)).
> 
> As usual, I'm inclined to wait at least a couple days for bugs to be discovered and fixed before attempting to use any new model 😉.
> 
> 
> 


---

> ## Lorry Zou
> 
> I just fune-tuned the instruct model yesterday, seems like it's not even on par with Gemma2 9b…Weird
> 
> 
> 
> > ## Valentin Werner
> > 
> > Might be the bugs James mentioned. These bugs are not always not always black and white, as in they raise Exceptions. Could also be that a different attention mechanism is used, which the model was not trained on or such (not sure if that is actually a thing and if it would cause an Exception, but you probably get the gist)
> > 
> > 
> > 
> > ## Eisuke Mizutani
> > 
> > I installed the latest transformers from source and could run training without error.
> > 
> > But as Lorry Zou mentioned, the result was not so good (even worse than llama3 in my case).
> > 
> > 
> > 


---

> ## EISLab_hwlee
> 
> It's very difficult to implement the code…
> 
> 
> 


---

> ## Valentin Werner
> 
> Release Season going hard in the last 5 weeks of the competition 🚀
> 
> 
> 
> > ## Psi
> > 
> > Thankfully, only three weeks left :)
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > It's quite funny with the GenAI Hype. You may have a breakthrough in the NLP competitions not by modelling techniques, but by sheer coincidence, having companies like H2O, Google or Mistral (& NVIDIA) release some high quality models. Not so long ago, we used to train Mistral-7B for peak performance - now it seems like a 3rd choice model.
> > > 
> > > 
> > > 


---

> ## gentle bird
> 
> new model. who is trying this?
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# Mistral-NeMo のリリース

**Ashwani** *2024年7月19日 金曜日 01:09:26 GMT+0900 (日本標準時)* (22票)

Mistral-NeMo 12B がリリースされました。

- Gemma2 9B および Llama3 8B を凌駕します。
- 128K のコンテキストウィンドウ。
- 100 以上の言語に対応する多言語モデル: ヨーロッパ語、アジア語、インド語に優れています。
- FP8 での量子化対応トレーニング。
- Apache 2.0 ライセンス。

ブログ: [https://mistral.ai/news/mistral-nemo/](https://mistral.ai/news/mistral-nemo/)

HF ウェイト (ベース): [https://huggingface.co/mistralai/Mistral-Nemo-Base-2407](https://huggingface.co/mistralai/Mistral-Nemo-Base-2407)

HF ウェイト (インストラクト): [https://huggingface.co/mistralai/Mistral-Nemo-Instruct-2407](https://huggingface.co/mistralai/Mistral-Nemo-Instruct-2407)

---

# 他のユーザーからのコメント

> ## James Day
> 
> FYI、Mistral-NeMo のファインチューニングは現在、transformers ライブラリで壊れているようです（[https://huggingface.co/mistralai/Mistral-Nemo-Instruct-2407/discussions/6](https://huggingface.co/mistralai/Mistral-Nemo-Instruct-2407/discussions/6) を参照）。修正はすぐにリリースされる予定です ([https://github.com/huggingface/transformers/pull/32065](https://github.com/huggingface/transformers/pull/32065))。
> 
> いつものように、新しいモデルを使用する前に、少なくとも数日間はバグが発見されて修正されるのを待ちたいと思います 😉。
> 
> 
> 
---
> ## Lorry Zou
> 
> 昨日、インストラクトモデルをファインチューニングしたのですが、Gemma2 9b に匹敵するレベルには達していません…奇妙です。
> 
> 
> 
> > ## Valentin Werner
> > 
> > James が言及したバグかもしれません。これらのバグは、常に明確なものではなく、例外を発生させることもあります。モデルがトレーニングされていない、または異なるアテンションメカニズムが使用されている可能性もあります（それが実際に存在するのか、例外が発生するのかはわかりませんが、要点は理解できると思います）。
> > 
> > 
> > 
> > ## Eisuke Mizutani
> > 
> > ソースから最新の transformers をインストールして、エラーなしでトレーニングを実行できました。
> > 
> > しかし、Lorry Zou が言及したように、結果はあまり良くありませんでした（私の場合、llama3 よりも悪かったです）。
> > 
> > 
> > 
---
> ## EISLab_hwlee
> 
> コードの実装が非常に難しいです…
> 
> 
> 
---
> ## Valentin Werner
> 
> コンペティションの残り 5 週間で、リリースシーズンが本格化しています 🚀
> 
> 
> 
> > ## Psi
> > 
> > 幸い、あと 3 週間しかありません :)
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > GenAI の盛り上がりは面白いですね。NLP コンペティションでのブレークスルーは、モデリング技術ではなく、H2O、Google、Mistral（& NVIDIA）などの企業がたまたま高品質なモデルをリリースしたという偶然の産物かもしれません。それほど昔には、Mistral-7B をトレーニングして最高のパフォーマンスを出していましたが、今では 3 番目の選択肢のモデルのように思えます。
> > > 
> > > 
> > > 
---
> ## gentle bird
> 
> 新しいモデルですね。誰が試していますか？
> 
> 
> 
---



</div>