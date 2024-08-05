# 要約 
このディスカッションでは、参加者の**Matthew S Farmer**がKaggle環境におけるモデルの読み込みについての問題を共有しています。彼は、ローカルでモデルを保存し提出する際のバリデーションフェーズで繰り返し失敗していると述べ、具体的にはモデル、重み、トークナイザーを含むtarballを作成したがうまくいかないとのことです。また、スタートノートブックでの指示に従いGemmaを使用しているが、他のLLMも試したいと考えています。しかし、Kaggleのゲーム環境に関するドキュメントが見つからず、具体的な手順が分からないようです。

他の参加者からは、Kaggleのフォーラムの既存の指示を示すコメントがあり、別のユーザーが読み込みコードの一部を見せるよう求めています。このやり取りは、モデルの実装に関する具体的な助けを求める一般的な内容が中心となっています。

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

# Help with loading model into kaggle environments

**Matthew S Farmer** *Thu Jun 27 2024 11:22:36 GMT+0900 (日本標準時)* (0 votes)

Hey all, 

I've tried way too many times to save a model locally and get it to be accepted during the validation phase after submission. Any tips?

Model, weights, tokenizer are all part of the submission tarball along with my submission file but I continue to fail validation. I've already been using Gemma as shown in the started notebook but I would like to try other LLMs. I've loaded HF snapshots, cloned git repos, copied steps from public code, but no luck. 

Is there documentation about the kaggle game environment that I'm missing? 

Thanks for any assistance. 

Cheers!



---

 # Comments from other users

> ## Chris Deotte
> 
> Hi. I explain the procedure [here](https://www.kaggle.com/competitions/llm-20-questions/discussion/513759)
> 
> 
> 
> > ## Matthew S FarmerTopic Author
> > 
> > Thanks, Chris. 
> > 
> > 
> > 


---

> ## Gnidnatsuot
> 
> maybe show part of your code for loading?
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# モデルのKaggle環境への読み込みについてのヘルプ
**Matthew S Farmer** *2024年6月27日 11:22:36 (日本標準時)* (0票)
皆さん、こんにちは。  
ローカルでモデルを保存して、提出時のバリデーションフェーズで受け入れられるようにするのに、何度も試してみたのですが、うまくいきません。何かコツはありますか？  
モデル、重み、トークナイザーはすべて提出用のtarballに含まれているのですが、バリデーションに失敗し続けています。スタートノートブックに示されているようにGemmaを使っていましたが、他のLLMも試してみたいです。HFのスナップショットを読み込んだり、Gitリポジトリをクローンしたり、公開されたコードのステップをコピーしたりしましたが、全くダメです。  
Kaggleのゲーム環境に関するドキュメントが見当たらないのですが、何か見落としているものがあるのでしょうか？  
どんな助けでも感謝します。  
よろしくお願いします！

---
# コメント
> ## Chris Deotte  
> こんにちは。手順については[こちら](https://www.kaggle.com/competitions/llm-20-questions/discussion/513759)で説明しています。

> > ## Matthew S Farmer (トピック作成者)  
> > ありがとう、クリス。  
> > 

---
> ## Gnidnatsuot  
> 読み込みのコードの一部を見せてもらえますか？  
> 


</div>