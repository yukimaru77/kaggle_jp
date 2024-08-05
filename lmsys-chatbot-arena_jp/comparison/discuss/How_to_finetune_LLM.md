# 要約 
このディスカッションは、KaggleのLMSYS - Chatbot Arena Human Preference PredictionsコンペティションにおけるLLMのファインチューニング方法に関するものです。

投稿者は、LLM初心者であり、コンペティションのシナリオに合わせてモデルをファインチューニングする方法を探しています。特に、DPOとLlama-Factoryのような方法が適しているのかを知りたいようです。

他のユーザーからのコメントでは、以下の情報が提供されています。

* Staru09は、QLORAを用いたカスタムデータセットでのLLMファインチューニングに関する記事を紹介しています。
* Nikhil Narayanは、他のファインチューニング方法に関するリソースを求めています。
* Staru09は、計算リソースが問題になる場合は、llamaedgeやwasmedgeなどのツールを試すことを提案しています。また、PEFT、LORA、QLORAなどの手法と組み合わせ、8ビットまたは16ビットにダウンサイズしてファインチューニングすることも提案しています。
* Lorry Zouは、YouTubeにLLM、特にLlama 3のファインチューニング方法を解説した動画がたくさんあることを指摘しています。
* YingxiZhangは、YouTubeから多くのことを学んだとコメントしています。

このディスカッションは、LLMのファインチューニング方法に関する有益な情報とリソースを提供しています。特に、初心者にとって、具体的なツールや手法に関する情報が役立つでしょう。


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

# How to finetune LLM? 

**bao** *Tue Jun 25 2024 18:26:28 GMT+0900 (日本標準時)* (0 votes)

I am a beginner in LLM and would like to get started. Could you please explain how to fine-tune the model for this scenario? Is it done using methods like DPO with LLama-Factory?



---

 # Comments from other users

> ## Staru09
> 
> You can check this [https://dassum.medium.com/fine-tune-large-language-model-llm-on-a-custom-dataset-with-qlora-fb60abdeba07](https://dassum.medium.com/fine-tune-large-language-model-llm-on-a-custom-dataset-with-qlora-fb60abdeba07)
> 
> 
> 
> > ## Nikhil Narayan
> > 
> > Well do you have resources about any other way to do this
> > 
> > 
> > 
> > > ## Staru09
> > > 
> > > Resources as in computation or something else. If computation is an issue then you can try using tools like llamaedge or wasmedge. They are very good frameworks to work with but you should know Rust otherwise you can use PEFT, or converting into lower bit like 8 or 16 to fine-tune along with LORA, QLORA etc.
> > > 
> > > 
> > > 


---

> ## Lorry Zou
> 
> There are plenty of great videos on YouTube teaching you how to fine-tune LLM and Llama 3 specifically.
> 
> 
> 
> > ## YingxiZhang
> > 
> > Indeed, there are a lot of resources on YouTube and I've learned a lot.😀
> > 
> > 
> > 


---



</div>
<div class="column-right">

# 日本語訳

# LLMのファインチューニング方法について

**bao** *2024年6月25日 火曜日 18:26:28 JST* (0票)

LLM初心者です。このシナリオに合わせてモデルをファインチューニングする方法を教えてください。DPOとLlama-Factoryのような方法で実行されますか？

---
# 他のユーザーからのコメント

> ## Staru09
> 
> この記事が参考になるかもしれません。[https://dassum.medium.com/fine-tune-large-language-model-llm-on-a-custom-dataset-with-qlora-fb60abdeba07](https://dassum.medium.com/fine-tune-large-language-model-llm-on-a-custom-dataset-with-qlora-fb60abdeba07)
> 
> 
> 
> > ## Nikhil Narayan
> > 
> > 他の方法でこれを行うためのリソースはありますか？
> > 
> > 
> > > ## Staru09
> > > 
> > > リソースとは、計算リソースのことですか？それとも何か別のものですか？計算リソースが問題になる場合は、llamaedgeやwasmedgeなどのツールを試すことができます。これらは非常に優れたフレームワークですが、Rustを知らなければPEFTを使用するか、LORA、QLORAなどと合わせて8ビットまたは16ビットにダウンサイズしてファインチューニングすることができます。
> > > 
> > > 
> > > 
---
> ## Lorry Zou
> 
> YouTubeには、LLMと特にLlama 3のファインチューニング方法を解説した素晴らしい動画がたくさんあります。
> 
> 
> 
> > ## YingxiZhang
> > 
> > 確かに、YouTubeにはたくさんのリソースがあり、私はそこから多くを学びました。😀
> > 
> > 
> > 
--- 



</div>