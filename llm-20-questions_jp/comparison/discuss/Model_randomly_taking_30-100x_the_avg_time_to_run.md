# 要約 
ディスカッションでは、ユーザー「OminousDude」が自分のモデルが平均的な処理時間の30〜100倍の時間を無作為に消費するエラーについて尋ねています。彼の実行は通常4〜6秒で終わるため、同じ問題を経験している他のユーザーを探しています。

他のユーザーからのコメントには、いくつかの可能性が指摘されています。特に「Sumo」は、Hugging Faceモデルが全ての重みをGPUに載せていないことや、モデルが停止トークンに達していないことが原因として挙げられています。また、モデルの再試行メカニズムが影響を及ぼしている可能性も示唆されています。

一方、「Matthew S Farmer」はこのような問題についての経験がないと述べています。

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

# Model randomly taking 30-100x the avg time to run

**OminousDude** *Fri Jun 28 2024 22:55:45 GMT+0900 (日本標準時)* (0 votes)

I am currently getting a lot of errors like this:

Why is this happening most of my runs take only about 4 to 6 seconds. Has anyone else had this error? Thanks in advance!



---

 # Comments from other users

> ## Sumo
> 
> not sure how relevant our experiences are, but we found a couple cases that can lead into this issue
> 
> - huggingface model offloading some weights to the CPU instead of putting them all on GPU,there's a flag to disable this behaviour
> 
> - model not reaching its stop token:
> the model is a base model rather than a chat or an instruct model, these model just go on forever
> the model is used behind some library with its internal retry mechanism (looking at you dspy), these libraries tend to prompt the model over and over until it got the right structure from the model, and this leads to some cryptic time variances
> 
> looking at your times there's a massive jump, which might hint you're making some conditional switching? like switching between hard-coded questions to an actual llm? If that's the case it's probably where to check first
> 
> 
> 
> > ## OminousDudeTopic Author
> > 
> > Thank you very much!
> > 
> > 
> > 


---

> ## Matthew S Farmer
> 
> Haven't seen this in mine. 
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# モデルが平均の30〜100倍の時間を無作為に消費している
**OminousDude** *2024年6月28日（金）22:55:45 GMT+0900 (日本標準時)* (0票)
現在、こういったエラーがたくさん発生しています。この原因は何でしょうか？私の実行のほとんどは約4〜6秒で済んでいます。誰か同じエラーが出た方はいませんか？事前に感謝します！

---
 # 他のユーザーからのコメント
> ## Sumo
> 
> 我々の経験がどれほど関連性があるかわかりませんが、この問題につながるケースがいくつかあります。
> 
> - huggingfaceモデルがすべての重みをGPUに置かず、一部をCPUにオフロードしている場合。この動作を無効にするフラグがあります。
> 
> - モデルが停止トークンに達していない:
> モデルがベースモデルで、チャットモデルや指示型モデルでない場合、これらのモデルは永遠に続いてしまいます。
> また、ライブラリの背後で使用されているモデルが、内部の再試行メカニズムを持っていると、（あなたのことを見ているdspy）これらのライブラリは、モデルから正しい構造を得るまで何度もモデルにプロンプトを送ることになります。そのため、一部の時間の変動がわかりにくくなります。
> 
> あなたの時間を見ていると、大きなジャンプがあります。これはハードコードされた質問から実際のLLMへの条件切り替えを行っていることを示唆しているかもしれません。その場合、まずはそこを確認することをお勧めします。
> 
> 
> > ## OminousDude トピック作成者
> > 
> > ありがとうございます！
> > 
> > 
> > 
---
> ## Matthew S Farmer
> 
> 私の方ではこのようなことを見たことはありません。
> 
> 
---


</div>