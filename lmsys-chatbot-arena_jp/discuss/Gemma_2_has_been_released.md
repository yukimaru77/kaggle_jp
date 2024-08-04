# Gemma 2 がリリースされました

**Anil Ozturk** *2024年6月28日 金曜日 00:49:26 GMT+0900 (日本標準時)* (26票)

Google は Gemma の v2 をリリースしました。9B と 27B の 2 つのバージョンで提供されています。9B のバージョンを試してみることをお勧めします。

HuggingFace: [https://huggingface.co/collections/google/gemma-2-release-667d6600fd5220e7b967f315](https://huggingface.co/collections/google/gemma-2-release-667d6600fd5220e7b967f315)

---

# 他のユーザーからのコメント

> ## Valentin Werner
> 
> Google が小さいモデルを大きくし続けるなら、Kaggle も GPU を大きくし続けるべきです 😉
> 
> 
> 
> > ## 表示名を入力してください
> > 
> > 同意します。また、多くのパッケージは、T4 などの古い GPU ではインストールできなくなりました。
> > 
> > 
> > 
> > ## Yashchavn
> > 
> > 確かに、どうなるか見てみましょう。
> > 
> > 
> > 
> > ## SunshineMoment
> > 
> > 同意！もっと強力な GPU が必要です。
> > 
> > 
> > 
---
> ## Cody_Null
> 
> 更新: 原因がわかりました。上のコードは OOM エラーを引き起こしますが、下のコードは正常に動作します。
> 
> `
> 
> # BitsAndBytes の設定
> 
> ```
> bnb_config =  BitsAndBytesConfig(
>     load_in_8bit=True,
>     bnb_8bit_compute_dtype=torch.float16,
>     bnb_8bit_use_double_quant=False)
> 
> bnb_config = BitsAndBytesConfig(
>     load_in_8bit=True,
>     bnb_8bit_quant_type="nf8",
>     bnb_8bit_use_double_quant=True,
>     bnb_8bit_compute_dtype=torch.bfloat16)
> 
> ```
> 
> `
> 
> 
> 
> > ## Lucifer_is_back_
> > 
> > ありがとうございます！
> > 
> > 
> > 
> > > ## Matous Famera
> > > 
> > > [@luciferisback](https://www.kaggle.com/luciferisback) Gemma 2 はいくつかのベンチマークで Llama 3 8b を上回っていることを読みました。ただし、Gamma 2 をこのコンペティションで実装できるかどうかはわかりません。
> > > 
> > > 
> > > 
> > ## mbyc_xkyz_2023
> > 
> > しかし、コードを実行すると、`Unused kwargs: ['bnb_8bit_quant_type', 'bnb_8bit_use_double_quant', 'bnb_8bit_compute_dtype']` というエラーが表示されます。これらの kwargs は使用されていません。どうすれば理解できますか？
> > 
> > 
> > 
---
> ## xiaotingting
> 
> Gemma v2 は、このコンペティションで私が試した中で最も役に立つものです。
> 
> 
> 
---
> ## Nikhil Tumbde
> 
> Kaggle に 9b のベースモデルを追加しました。[こちら](https://www.kaggle.com/models/nikhiltumbde/gemma-2-9b-hf)
> 
> 
> 
---
> ## Rishit Jakharia
> 
> ### GGUF ファイルについて
> 
> - Kaggle で Gemma 2 の GGUF ファイルを使用できた人はいますか？
> 
> 私は llama cpp を使用していますが、最新バージョンの llamaCPP は Kaggle と互換性がないようです。
> 
> 
> 
---
> ## Guocheng Song
> 
> わお、すごいですね！
> 
> 
> 
---

