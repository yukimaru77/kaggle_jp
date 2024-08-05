# 要約 
ディスカッションでは、新しくリリースされたGemma 2を使用して成功した参加者がいるかどうかが問われています。参加者のVassiliPhがこのモデルについての経験を尋ね、他のユーザーからの反応が続いています。

- **Kasahara**は、GPUメモリエラーのためGemma 2を実行できず、別のコードを用いてローカルでテスト環境を構築したが、出力ファイルが容量を超えて提出できなかったと報告しています。
  
- **Mitsutani**もGemma 2を試みており、ノートブックの出力を圧縮後に提出したが、バリデーションに失敗したことを述べています。彼は、実行時に特定のファイルのみを必要とするようにコードを修正する方法についてアドバイスを求めています。

このように、Gemma 2を使用する際の技術的な問題や成功の試みが議論されています。

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

# Gemma 2 - any success?

**VassiliPh** *Fri Jun 28 2024 03:36:25 GMT+0900 (日本標準時)* (2 votes)

Has anyone succeeded in using new Gemma 2 (it was just released today) for this competition?

[https://www.kaggle.com/models/google/gemma-2/keras](https://www.kaggle.com/models/google/gemma-2/keras)



---

 # Comments from other users

> ## Kasahara
> 
> I couldn't run it due to a GPU memory error. 
> 
> So, I downloaded the LLM locally as shown in [this code](https://www.kaggle.com/code/kasafumi/gemma2-9b-it-llm20-questions), and it worked in my test environment.
> 
> However, creating the submit file would exceed the capacity of the output directory, so i could not submit.
> 
> 
> 
> > ## Mitsutani
> > 
> > I've been trying to use Gemma 2 as well. I downloaded your notebook's output and compressed it on my computer, then submitted the compressed file but it didn't pass validation (the logs were empty). Do you have any idea why that could be or how to change the code so that main.py runs only on the files in /submission? I'm new to this so any help is appreciated. 
> > 
> > 
> > 


---



</div>
<div class="column-right">

# 日本語訳

# Gemma 2 - 成功した人いますか？
**VassiliPh** *2024年6月28日 金曜 03:36:25 GMT+0900 (日本標準時)* (2票)
新しくリリースされたGemma 2（今日リリースされました）をこのコンペティションで使用して成功した人はいますか？
[https://www.kaggle.com/models/google/gemma-2/keras](https://www.kaggle.com/models/google/gemma-2/keras)
---
 # 他のユーザーからのコメント
> ## Kasahara
> 
> GPUメモリエラーのため、実行できませんでした。
> 
> そこで、[このコード](https://www.kaggle.com/code/kasafumi/gemma2-9b-it-llm20-questions)に従ってLLMをローカルにダウンロードし、テスト環境で動作させました。
> 
> ただ、提出ファイルを作成すると出力ディレクトリの容量を超えてしまったため、提出できませんでした。
> 
> > ## Mitsutani
> > 
> > 私もGemma 2を使おうとしています。あなたのノートブックの出力をダウンロードして、コンピュータ上で圧縮した後、その圧縮ファイルを提出しましたが、バリデーションに通りませんでした（ログは空でした）。なぜそうなったのか、またはmain.pyが/submission内のファイルだけで実行されるようにコードを変更する方法について、何かアイデアはありますか？私は初心者なので、どんな助けでも感謝します。
> > 
> > 
> 


</div>