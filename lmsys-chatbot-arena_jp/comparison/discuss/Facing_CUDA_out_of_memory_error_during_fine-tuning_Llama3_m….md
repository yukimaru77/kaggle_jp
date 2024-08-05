# 要約 
このディスカッションは、KaggleユーザーのTabassum_Novaさんが、Llama3モデルのファインチューニング中に「CUDA out of memory」エラーが発生したという問題について、解決策を求めているものです。

Tabassum_Novaさんは、他のユーザーの提案に従い、`gradient_checkpointing`を有効にしたことで、トレーニングを開始することができました。しかし、トレーニングに時間がかかるため、Kaggleノートブック以外の方法でモデルをトレーニングする方法を質問しました。

他のユーザーからは、Vastai、Runpod、Google CloudなどのクラウドホストプラットフォームでGPUインスタンスをレンタルする方法や、Colab Proを使用する方法が提案されました。また、LoRA設定の`rank`を減らすことや、`max_length`を減らすことなども提案されました。

Tabassum_Novaさんは、これらの提案を試したものの、エラーは解決されず、トレーニング速度も遅いという問題を抱えています。TPUを使用すれば、このような問題は発生しない可能性があるという意見もありました。

最終的に、Tabassum_Novaさんはトレーニングの問題を解決したものの、トレーニング速度を上げるための解決策を求めています。


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

# Facing "CUDA out of memory" error during fine-tuning Llama3 model

**Tabassum_Nova** *Fri May 31 2024 18:06:44 GMT+0900 (日本標準時)* (5 votes)

I tried to fine-tune Llama3 model inspired by [fine-tune-llama-3-for-sentiment-analysis](https://www.kaggle.com/code/lucamassaron/fine-tune-llama-3-for-sentiment-analysis) notebook. But I was facing the following error:

torch.cuda.OutOfMemoryError: CUDA out of memory. Tried to allocate 224.00 MiB. GPU 0 has a total capacty of 14.75 GiB of which 11.06 MiB is free. Process 3258 has 14.73 GiB memory in use. Of the allocated memory 14.04 GiB is allocated by PyTorch, and 509.85 MiB is reserved by PyTorch but unallocated. If reserved but unallocated memory is large try setting max_split_size_mb to avoid fragmentation.  See documentation for Memory Management and PYTORCH_CUDA_ALLOC_CONF

I have already followed the solution suggested in [this discussion](https://www.kaggle.com/discussions/getting-started/140636). But these did not help. This is the link of [my notebook](https://www.kaggle.com/code/tabassumnova/lmsys-fine-tuning-llama3-8b/notebook)

Can anyone please suggest what I should do to avoid this error?



---

 # Comments from other users

> ## Ivan Vybornov
> 
> Enable gradient_checkpointing and use paged_adamw_8bit instead of a 32bit version. If does not work, try applying lora to less target_modules, for instance finetuning just ["q_proj", "k_proj", "v_proj", "o_proj"] ain't bad.
> 
> 
> 
> > ## Tabassum_NovaTopic Author
> > 
> > Thank you. Enabling gradient _checkpointing works. Training has started 😁
> > 
> > 
> > 


---

> ## Valentin Werner
> 
> If you are not using it already, use batch size 1. Maybe use T4 x2 
> 
> in general, kaggle GPU might be too slow for the amount and length of training data
> 
> 
> 
> > ## Tabassum_NovaTopic Author
> > 
> > I solved the issue. But it’s taking a long time to train. I am using Kaggle GPU T4x2. Could you please suggest any other option to train the model other than kaggle notebook? I don’t have any personal GPU
> > 
> > 
> > 
> > > ## Kishan Vavdara
> > > 
> > > There are many options , you can rent A100, Rtx4090 or any other GPU instances at [Vastai](https://vast.ai/),  [Runpod](https://www.runpod.io/), or other cloud host platforms,  train your model and then delete the instance. You can also start google cloud free trial, it will give you 300$ credits for 3 months. I think colab pro also gives access to A100 and V100 Gpu's. Personally, I found vastai to be more convenient and cheap. 
> > > 
> > > 
> > > 
> > > ## Tabassum_NovaTopic Author
> > > 
> > > Thank you for your suggestions
> > > 
> > > 
> > > 
> > > ## lijiang3859
> > > 
> > > I trained offline in my server, but it still requires memory. How can I solve it? 
> > > 
> > > If I submit this to notenotebook in the system, will the code still run on the same device I am using for inference? (so sad)
> > > 
> > > 
> > > 


---

> ## Kishan Vavdara
> 
> Try reducing LoRA config 'rank', it will reduce trainable params, in your notebook i see you're using 64 rank, try 4, 8, or 16.  And you can also try reducing max_length. 
> 
> 
> 
> > ## Tabassum_NovaTopic Author
> > 
> > I tried with rank 4, max_seq_length = 512; Still getting the same error
> > 
> > 
> > 


---

> ## kartikey bartwal
> 
> Are you doing your work on some other platform other thank kaggle notebooks or google colab ? I don't think such problem should've arrived with their TPU's
> 
> 
> 
> > ## Tabassum_NovaTopic Author
> > 
> > The training issue is solved. But it’s training too slowly. I have not tried with TPU. Could you please suggest any solution too solve this training speed?
> > 
> > 
> > 
> > > ## Tabassum_NovaTopic Author
> > > 
> > > Yeah I understand 
> > > 
> > > 
> > > 


---



</div>
<div class="column-right">

# 日本語訳

# Llama3モデルのファインチューニング中に「CUDA out of memory」エラーが発生

**Tabassum_Nova** *2024年5月31日 18:06:44 (日本標準時)* (5 votes)

[fine-tune-llama-3-for-sentiment-analysis](https://www.kaggle.com/code/lucamassaron/fine-tune-llama-3-for-sentiment-analysis) のノートブックを参考に、Llama3モデルのファインチューニングを試みました。しかし、以下のエラーが発生しました。

```
torch.cuda.OutOfMemoryError: CUDA out of memory. Tried to allocate 224.00 MiB. GPU 0 has a total capacty of 14.75 GiB of which 11.06 MiB is free. Process 3258 has 14.73 GiB memory in use. Of the allocated memory 14.04 GiB is allocated by PyTorch, and 509.85 MiB is reserved by PyTorch but unallocated. If reserved but unallocated memory is large try setting max_split_size_mb to avoid fragmentation.  See documentation for Memory Management and PYTORCH_CUDA_ALLOC_CONF
```

[このディスカッション](https://www.kaggle.com/discussions/getting-started/140636)で提案されている解決策を試しましたが、効果はありませんでした。私のノートブックのリンクはこちらです：[私のノートブック](https://www.kaggle.com/code/tabassumnova/lmsys-fine-tuning-llama3-8b/notebook)

このエラーを回避するために、何か提案していただけませんか？

---
# 他のユーザーからのコメント

> ## Ivan Vybornov
> 
> `gradient_checkpointing` を有効にして、32ビット版ではなく `paged_adamw_8bit` を使用してください。それでもうまくいかない場合は、`lora` を適用する `target_modules` を減らしてみてください。例えば、`["q_proj", "k_proj", "v_proj", "o_proj"]` だけをファインチューニングしても悪くありません。
> 
> 
> 
> > ## Tabassum_Novaトピック作成者
> > 
> > ありがとうございます。`gradient_checkpointing` を有効にしたら、トレーニングが開始されました 😁
> > 
> > 
> > 
---
> ## Valentin Werner
> 
> まだ使用していない場合は、バッチサイズを 1 にしてください。T4 x2 を使用することもできます。
> 
> 一般的に、Kaggle の GPU は、トレーニングデータの量と長さに対して遅すぎる可能性があります。
> 
> 
> 
> > ## Tabassum_Novaトピック作成者
> > 
> > 問題は解決しました。しかし、トレーニングに時間がかかります。Kaggle GPU T4x2 を使用しています。Kaggle ノートブック以外の方法でモデルをトレーニングする方法を提案していただけませんか？個人的な GPU はありません。
> > 
> > 
> > 
> > > ## Kishan Vavdara
> > > 
> > > 多くの選択肢があります。[Vastai](https://vast.ai/)、[Runpod](https://www.runpod.io/)、またはその他のクラウドホストプラットフォームで A100、Rtx4090、またはその他の GPU インスタンスをレンタルし、モデルをトレーニングしてからインスタンスを削除することができます。Google Cloud の無料トライアルを開始することもできます。3 か月間、300 ドルのクレジットがもらえます。Colab Pro も A100 と V100 GPU にアクセスできると思います。個人的には、Vastai が最も便利で安価だと感じています。
> > > 
> > > 
> > > 
> > > ## Tabassum_Novaトピック作成者
> > > 
> > > 提案ありがとうございます。
> > > 
> > > 
> > > 
> > > ## lijiang3859
> > > 
> > > サーバーでオフラインでトレーニングしましたが、それでもメモリが必要です。どうすれば解決できますか？
> > > 
> > > このノートブックをシステムに提出した場合、コードは推論に使用しているのと同じデバイスで実行されますか？ (悲しい)
> > > 
> > > 
> > > 
---
> ## Kishan Vavdara
> 
> LoRA 設定の `rank` を減らしてみてください。これにより、トレーニング可能なパラメータが減ります。ノートブックでは、`rank` に 64 を使用していますが、4、8、または 16 を試してみてください。また、`max_length` を減らすこともできます。
> 
> 
> 
> > ## Tabassum_Novaトピック作成者
> > 
> > `rank` を 4 に、`max_seq_length` を 512 にして試しましたが、同じエラーが発生します。
> > 
> > 
> > 
---
> ## kartikey bartwal
> 
> Kaggle ノートブックや Google Colab 以外のプラットフォームで作業していますか？TPU を使用していれば、このような問題は発生しないはずです。
> 
> 
> 
> > ## Tabassum_Novaトピック作成者
> > 
> > トレーニングの問題は解決しました。しかし、トレーニングが遅すぎます。TPU は試していません。トレーニング速度を上げるための解決策を提案していただけませんか？
> > 
> > 
> > 
> > > ## Tabassum_Novaトピック作成者
> > > 
> > > はい、理解しました。
> > > 
> > > 
> > > 
---




</div>