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

