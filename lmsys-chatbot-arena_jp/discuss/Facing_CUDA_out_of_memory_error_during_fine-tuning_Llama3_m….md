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


