# 要約 
ディスカッションの要約は以下の通りです。

ユーザー「ivan」は、最近のミストラルAIハッカソンで提供されたAPIを利用して、新しいデータセット「Q20LLM」を作成したと発表しました。このデータセットには78,000以上の質問が含まれ、一般的な質問から具体的な質問までの対話形式のデータが収録されています。ivanは、これまでそのような対話形式のデータセットが存在しなかったと指摘しており、LLMを用いて対話を構築する試みについて述べています。また、このデータセットを使用して「指示に従う」モデルのファインチューニングを試みたが、成功しなかったと報告し、モデルが訓練中に見た質問の数だけ質問を生成しようとする傾向があることを明らかにしました。

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

# New Q20LLM dataset with >78k questions

**ivan** *Tue May 28 2024 02:34:18 GMT+0900 (日本標準時)* (3 votes)

Hi, recently on [Mistral AI hackathon](https://x.com/MistralAILabs/status/1788970688172245256) I've build a new dataset [Q20LLM](https://huggingface.co/datasets/cvmistralparis/Q20LLM) using provided APIs from [Mistral API](https://docs.mistral.ai/api/) and [Groq Cloud](https://docs.mistral.ai/api/).

AFAIK there is no dataset with dialog questions from general to specific. I tried to build such dialogs with LLMs. I also tried to fine-tune "instruction following" model on this dataset, but no success. The model tends to ask as many questions as it saw during training.





</div>
<div class="column-right">

# 日本語訳

# 新しいQ20LLMデータセットが登場、78,000以上の質問を収録
**ivan** *2024年5月28日 02:34:18 GMT+0900 (日本標準時)* (3票)
こんにちは、最近[ミストラルAIハッカソン](https://x.com/MistralAILabs/status/1788970688172245256)で提供されたAPIを利用して、新しいデータセット[Q20LLM](https://huggingface.co/datasets/cvmistralparis/Q20LLM)を作成しました。APIは[Mistral API](https://docs.mistral.ai/api/)と[Groq Cloud](https://docs.mistral.ai/api/)から提供されました。
私の知る限り、一般的な質問から具体的な質問までの対話形式のデータセットは存在ません。このような対話をLLMを使って構築しようと試みました。また、このデータセットを使って「指示に従う」モデルのファインチューニングも試みましたが、成功しませんでした。モデルは、訓練中に見た質問の数だけ質問をしようとする傾向があります。


</div>