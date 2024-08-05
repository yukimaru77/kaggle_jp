# 要約 
このディスカッションは、KaggleのLMSYS - Chatbot Arena Human Preference Predictionsコンペティションにおける推論時間に関するものです。

投稿者は、テストデータが約25,000行あり、9時間のランタイム制限では推論時間が1.3秒以下になるため、大型言語モデル（LLM）の使用が困難ではないかと懸念しています。

他のユーザーからのコメントでは、DeBERTa-v3-large、Mistral 7B、Llama 3 8BなどのLLMを用いた推論時間の報告や、データのバッチ処理による高速化の提案、DeBERTa-v3-baseを用いた1時間以内の推論を実現したノートブックの共有など、様々な意見や情報が共有されています。

結論として、このディスカッションは、コンペティションにおけるLLMの使用可能性と推論時間の最適化について議論しており、参加者にとって有益な情報交換の場となっています。


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

# Less than 1.3 seconds per inference?

**Rishiraj Acharya** *Fri May 03 2024 14:21:19 GMT+0900 (日本標準時)* (17 votes)

There are approximately 25000 rows in test data and 9 hours runtime translates to less than 1.3 seconds per inference. Does this make usage of Large Language Models obsolete for this competition? I might not know of any LLM that runs this fast but I'm open to learning.



---

 # Comments from other users

> ## Raja Biswas
> 
> For my subs, the inference runtimes were as below (T4 x2):
> 
> - deberta-v3-large (~1.5hrs)
> 
> - mistral 7b (~4hr)
> 
> - llama3 8b (~4hr)
> 
> Max sequence length used: 1.8k
> 
> 
> 


---

> ## Siddhantoon
> 
> You can even batch process the data, why run every row sequentially.
> 
> 
> 


---

> ## Fritz Cremer
> 
> I published a deberta-v3-base notebook which predicts in under an hour. I think even deberta-v3-large should be no problem:
> 
> [https://www.kaggle.com/code/fritzcremer/lmsys-deberta-v3-base-baseline](https://www.kaggle.com/code/fritzcremer/lmsys-deberta-v3-base-baseline)
> 
> 
> 


---

> ## Angela
> 
> You are right. It seems that it is unable to utilize prompt engineering for LLM in this competition. 
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# 推論時間1.3秒以下？

**Rishiraj Acharya** *2024年5月3日 金曜日 14:21:19 日本標準時* (17票)

テストデータは約25,000行あり、9時間のランタイムは推論あたり1.3秒未満になります。これは、このコンペティションで大型言語モデルの使用を無効にするのでしょうか？私はこれほど高速に動作するLLMを知りませんが、学ぶことに意欲的です。
---
# 他のユーザーからのコメント
> ## Raja Biswas
> 
> 私の提出では、推論時間は以下の通りでした（T4 x2）：
> 
> - deberta-v3-large（約1.5時間）
> 
> - mistral 7b（約4時間）
> 
> - llama3 8b（約4時間）
> 
> 使用された最大シーケンス長：1.8k
> 
> 
> 
---
> ## Siddhantoon
> 
> データをバッチ処理することもできます。なぜすべての行を順番に実行するのですか？
> 
> 
> 
---
> ## Fritz Cremer
> 
> 私は1時間以内に予測するdeberta-v3-baseのノートブックを公開しました。deberta-v3-largeでも問題ないと思います。
> 
> [https://www.kaggle.com/code/fritzcremer/lmsys-deberta-v3-base-baseline](https://www.kaggle.com/code/fritzcremer/lmsys-deberta-v3-base-baseline)
> 
> 
> 
---
> ## Angela
> 
> あなたは正しいです。このコンペティションでは、LLMのプ rompt エンジニアリングを利用できないようです。
> 
> 
> 
---



</div>