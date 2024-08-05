# 要約 
このディスカッションは、LMSYS - Chatbot Arena 人間による好み予測チャレンジにおけるモデルのトレーニング言語に関するものです。

投稿者は、テストデータが英語のみなのか、それとも複数の言語を含むのかを質問しています。

Valentin Wernerは、トレーニングデータには英語以外のサンプルも含まれていることを回答しています。ただし、サンプル数は少ないとのことです。また、LlamaやGemmaなどのLLMは複数の言語を扱うことができるため、トレーニング言語を英語のみに限定することは時間の無駄になる可能性があると述べています。 


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

# Should we train our model just for English or for multiple languages ? 

**AlphaTT30** *Sun Jul 14 2024 21:51:33 GMT+0900 (日本標準時)* (0 votes)

Can the test data contain multiple languages or just English? 



---

 # Comments from other users

> ## Valentin Werner
> 
> The training data does include non-english samples. Even languages with non-latin alphabet (e.g., asian languages and russian). However, the amount of samples seem to be quite low. Keep in mind that many models are able to "speak" multile languages inherently, so if you are using LLMs like Llama or Gemma, you are probably wasting time on this filter.
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# モデルを英語のみでトレーニングすべきか、それとも複数の言語でトレーニングすべきか？
**AlphaTT30** *2024年7月14日 21:51:33 (日本標準時)* (0 votes)
テストデータは複数の言語を含む可能性がありますか、それとも英語のみですか？
---
# 他のユーザーからのコメント
> ## Valentin Werner
> 
> トレーニングデータには英語以外のサンプルも含まれています。ラテン文字以外のアルファベットを使用する言語（例えば、アジア言語やロシア語）も含まれています。ただし、サンプル数はかなり少ないようです。多くのモデルは本質的に複数の言語を「話す」ことができるため、LlamaやGemmaなどのLLMを使用している場合は、このフィルターに時間を無駄にする可能性があります。
> 
> 
> 
--- 



</div>