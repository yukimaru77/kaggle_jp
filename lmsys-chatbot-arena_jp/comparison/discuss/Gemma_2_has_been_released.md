# 要約 
このディスカッションは、Googleがリリースした新しい言語モデルGemma v2についてです。このモデルは9Bと27Bの2つのバージョンで提供され、ユーザーは9Bのバージョンを試すことを推奨されています。

ディスカッションでは、Gemma v2の性能について、いくつかのユーザーがコメントしています。特に、Gemma v2がいくつかのベンチマークでLlama 3 8bを上回っているという意見が出ています。

一方で、Gemma v2をこのコンペティションで実装する際に、いくつかの問題が発生しているようです。例えば、BitsAndBytesの設定に関するエラーや、GGUFファイルの互換性に関する問題などが報告されています。

このディスカッションは、Gemma v2の性能と実装に関する議論が活発に行われていることを示しています。ユーザーは、Gemma v2の性能や実装に関する情報を共有し、互いに助け合っています。


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

# Gemma 2 has been released

**Anil Ozturk** *Fri Jun 28 2024 00:49:26 GMT+0900 (日本標準時)* (26 votes)

Google has released the v2 for Gemma. It is available in two versions: 9B and 27B. You might want to try the 9B one.

HuggingFace: [https://huggingface.co/collections/google/gemma-2-release-667d6600fd5220e7b967f315](https://huggingface.co/collections/google/gemma-2-release-667d6600fd5220e7b967f315)



---

 # Comments from other users

> ## Valentin Werner
> 
> If they keep making the small models bigger, kaggle should keep making GPUs bigger 😉
> 
> 
> 
> > ## Enter your display name
> > 
> > Agree, also many packages now no longer support installation on older GPUs like the T4.
> > 
> > 
> > 
> > ## Yashchavn
> > 
> > true, lets see what happens
> > 
> > 
> > 
> > ## SunshineMoment
> > 
> > Agree! we need more powerful gpu
> > 
> > 
> > 


---

> ## Cody_Null
> 
> Update: I have found the reason. The top here causes an OOM error while the bottom works fine. 
> 
> `
> 
> # BitsAndBytes configuration
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
> > thanks for that!
> > 
> > 
> > 
> > > ## Matous Famera
> > > 
> > > [@luciferisback](https://www.kaggle.com/luciferisback) I have read Gemma 2 outperforms Llama 3 8b in several benchmarks. I don't know if Gamma 2 can be implemented in this competition though.
> > > 
> > > 
> > > 
> > ## mbyc_xkyz_2023
> > 
> > but , after i strat my code, Unused kwargs: ['bnb_8bit_quant_type', 'bnb_8bit_use_double_quant', 'bnb_8bit_compute_dtype']. These kwargs are not used in , how to understand?
> > 
> > 
> > 


---

> ## xiaotingting
> 
> Gemma v2 is indeed the most useful one I have tried in this competition.
> 
> 
> 


---

> ## Nikhil Tumbde
> 
> Added the 9b base model on kaggle, [here](https://www.kaggle.com/models/nikhiltumbde/gemma-2-9b-hf)
> 
> 
> 


---

> ## Rishit Jakharia
> 
> ### Regarding the GGUF files
> 
> - Did anyone manage to use the Gemma 2 GGUF files on Kaggle
> 
> I am unable to do so myself, as I'm using llama cpp  and the latest version of llamaCPP seems to not be compatible with Kaggle
> 
> 
> 


---

> ## Guocheng Song
> 
> wow， that's amazing
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

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



</div>