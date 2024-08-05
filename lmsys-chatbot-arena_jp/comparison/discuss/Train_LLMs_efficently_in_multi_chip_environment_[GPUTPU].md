# 要約 
このディスカッションは、Simon Veitner氏が、複数のGPU/TPUチップでLLMを効率的にトレーニングするためのカスタマイズ可能なノートブックを共有したものです。このノートブックは、FSDPとTP技術を用いており、Kaggle LLMサイエンス試験の1位ソリューションから着想を得ています。ノートブックのスコアは現状ではあまり良くありませんが、前処理やモデリングなどを調整することで簡単に改善できるとされています。 


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

# Train LLMs efficently in multi chip environment [GPU/TPU]

**Simon Veitner** *Wed May 29 2024 16:24:01 GMT+0900 (日本標準時)* (4 votes)

Hello guys,

I shared a customizable notebook that let's you train LLMs with FSDP and potentially TP technique on multiple GPU/TPU chips.

The architecture was inspired by [first place solution in LLM science exam.](https://www.kaggle.com/competitions/kaggle-llm-science-exam/discussion/446422)

Note that the score of the notebook is rather bad but can be easily improved by adjusting preproccesing/modelling etc etc.

[See the notebook here](https://www.kaggle.com/code/simonveitner/fsdp-with-scalax)





</div>
<div class="column-right">

# 日本語訳

# 複数チップ環境（GPU/TPU）でLLMを効率的にトレーニングする

**Simon Veitner** *2024年5月29日 水曜日 16:24:01 GMT+0900 (日本標準時)* (4票)

皆さん、こんにちは！

FSDPとTP技術を使って、複数のGPU/TPUチップでLLMをトレーニングできるカスタマイズ可能なノートブックを共有しました。

このアーキテクチャは、[LLMサイエンス試験の1位ソリューション](https://www.kaggle.com/competitions/kaggle-llm-science-exam/discussion/446422)から着想を得ています。

ノートブックのスコアはあまり良くありませんが、前処理やモデリングなどを調整することで簡単に改善できます。

[ノートブックはこちら](https://www.kaggle.com/code/simonveitner/fsdp-with-scalax)をご覧ください。 



</div>