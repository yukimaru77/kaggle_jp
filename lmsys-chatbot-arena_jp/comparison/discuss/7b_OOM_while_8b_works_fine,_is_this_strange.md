# 要約 
このディスカッションは、Kaggleのコンペティション参加者が、Mistral 7BモデルとLlama 3 8Bモデルを比較した際に遭遇したOOMエラーに関するものです。

Cody_Nullは、8ビットに量子化されたMistral 7BモデルではOOMエラーが発生するのに、同じく8ビットに量子化されたLlama 3 8Bモデルでは発生しないことに疑問を抱きました。彼は、モデルのサイズやアーキテクチャの違いが原因ではないかと推測しました。

Valentin Wernerは、モデルのサイズや隠れ層のサイズが原因ではないことを指摘し、Kaggleのインフラストラクチャが原因である可能性を指摘しました。彼は、新しい環境でモデルを読み込むことを推奨しました。

Cody_Nullは、自分が間違ったスレッドに投稿していたことに気づき、問題の原因がBitsAndBytesの設定にあることを発見しました。彼は、コードの最初の部分ではOOMエラーが発生し、後の部分では正常に動作することを明らかにしました。

Valentin Wernerは、Cody_Nullのミスを面白がりつつも、彼の投稿が役に立ったことを認めました。

このディスカッションは、コンペティション参加者が遭遇する可能性のある技術的な問題を共有し、解決策を見つけるための場として役立っています。また、参加者同士の交流を促進し、コミュニティの結束を強める役割も果たしています。


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

# 7b OOM while 8b works fine, is this strange?

**Cody_Null** *Wed Jun 26 2024 05:48:42 GMT+0900 (日本標準時)* (7 votes)

I am trying to compare the performance of different base models, for example we can compare base mistral 7B model quantized to 8bit and compare this to the llama 3 8B model also quantized to 8bit. I am noticing I get OOM errors for the 7B model (and others) but not the llama3 8b? I understand they can have different architectures with different memory requirements and that their size is not fully dependent on the number of parameters but just to be sure does anyone else find this strange? 



---

 # Comments from other users

> ## Valentin Werner
> 
> It cannot be due to size - Mistral 7b 8 bit takes 6.87 GB,  Llama 3 8B 8 bit takes 7.05 GB (see: [https://huggingface.co/spaces/hf-accelerate/model-memory-usage)](https://huggingface.co/spaces/hf-accelerate/model-memory-usage)). From what I can see they also have the same hidden sizes and dimensions, so embeddings for Mistral should not take more RAM than for Llama
> 
> Are you getting the error while loading? This might be due to kaggle infrastructure. For fair comparisons you should always load from a freshly restarted environment (as torch.cuda.empty_cache has not the same effect from my experience)
> 
> 
> 
> > ## Cody_NullTopic Author
> > 
> > Glad I am not crazy, I will circle back and try it again today just to double check I have not made some silly mistake. I will update this if I find anything.
> > 
> > 
> > 


---

> ## Cody_NullTopic Author
> 
> Just now realized I totally put this in the wrong thread: 
> 
> Update: I have found the reason. The top here causes an OOM error while the bottom works fine.
> 
> `
> 
> BitsAndBytes configuration
> 
> bnb_config =  BitsAndBytesConfig(
> 
>     load_in_8bit=True,
> 
>     bnb_8bit_compute_dtype=torch.float16,
> 
>     bnb_8bit_use_double_quant=False)
> 
> bnb_config = BitsAndBytesConfig(
> 
>     load_in_8bit=True,
> 
>     bnb_8bit_quant_type="nf8",
> 
>     bnb_8bit_use_double_quant=True,
> 
>     bnb_8bit_compute_dtype=torch.bfloat16)
> 
> `
> 
> 
> 
> > ## Valentin Werner
> > 
> > I was wondering lol 
> > 
> > still got 4 upvotes on the other one 😉
> > 
> > 
> > 
> > > ## Cody_NullTopic Author
> > > 
> > > lol as long as it is useful I guess haha figured I might as well let this side be complete. 
> > > 
> > > 
> > > 


---



</div>
<div class="column-right">

# 日本語訳

# 7B モデルでOOMエラーが発生するのに、8B モデルは正常に動作するのはなぜ？

**Cody_Null** *2024年6月26日 水曜日 05:48:42 GMT+0900 (日本標準時)* (7票)

異なるベースモデルのパフォーマンスを比較しようとしています。例えば、8ビットに量子化されたMistral 7Bモデルと、同じく8ビットに量子化されたLlama 3 8Bモデルを比較します。7Bモデル（と他のモデル）ではOOMエラーが発生しますが、Llama 3 8Bでは発生しません。これらのモデルは異なるアーキテクチャを持ち、メモリ要件も異なることは理解していますし、サイズがパラメータ数に完全に依存するわけではないことも理解しています。しかし、念のため、他にこの現象を奇妙に感じる人はいませんか？

---
# 他のユーザーからのコメント

> ## Valentin Werner
> 
> サイズが原因ではありません。Mistral 7b 8ビットは6.87 GB、Llama 3 8B 8ビットは7.05 GBです（参照: [https://huggingface.co/spaces/hf-accelerate/model-memory-usage](https://huggingface.co/spaces/hf-accelerate/model-memory-usage)）。私の知る限り、両モデルは隠れ層のサイズと次元も同一なので、Mistralの埋め込みがLlamaよりも多くのRAMを消費することはありません。
> 
> モデルの読み込み中にエラーが発生していますか？これはKaggleのインフラストラクチャが原因かもしれません。公平な比較を行うには、常に新しく再起動した環境からモデルを読み込む必要があります（私の経験では、torch.cuda.empty_cacheは同じ効果をもたらしません）。
> 
> 
> 
> > ## Cody_Nullトピック作成者
> > 
> > 狂ってなくてよかった。今日改めて確認して、自分がどこかで愚かなミスをしていないか確認してみます。何か発見したら、このスレッドを更新します。
> > 
> > 
> > 
---
> ## Cody_Nullトピック作成者
> 
> 今気づきましたが、完全に間違ったスレッドに投稿していました。
> 
> 更新: 原因がわかりました。以下のコードの上部がOOMエラーを引き起こし、下部が正常に動作します。
> 
> `
> 
> BitsAndBytesの設定
> 
> bnb_config =  BitsAndBytesConfig(
> 
>     load_in_8bit=True,
> 
>     bnb_8bit_compute_dtype=torch.float16,
> 
>     bnb_8bit_use_double_quant=False)
> 
> bnb_config = BitsAndBytesConfig(
> 
>     load_in_8bit=True,
> 
>     bnb_8bit_quant_type="nf8",
> 
>     bnb_8bit_use_double_quant=True,
> 
>     bnb_8bit_compute_dtype=torch.bfloat16)
> 
> `
> 
> 
> 
> > ## Valentin Werner
> > 
> > わかりました笑
> > 
> > でも、もう4つのいいねをもらっちゃいましたね😉
> > 
> > 
> > 
> > > ## Cody_Nullトピック作成者
> > > 
> > > 役に立てばいいんですけどね笑。このスレッドもちゃんと完成させようと思って。
> > > 
> > > 
> > > 
---



</div>