# 要約 
ディスカッションでは、参加者のG R Shanker Saiが、ローカルの言語モデル（LLM）用にLangChainを基にしたエージェントラッパーを作る過程で直面している問題について、Hugging FaceやGroqのオープンソースモデルをAPIコールを使って利用できるか質問しました。これに対し、Matthew S Farmerが評価環境ではインターネットアクセスができないため、APIコールは機能しないと説明しました。Hugging Faceのモデルを利用する場合は、モデルの重みを提出物にロードする必要があり、これにはスナップショットをダウンロードしてアップロードするか、transformersライブラリのsave_pretrained関数を使用する方法があると述べました。また、Groqはインターネット接続が必要のため利用できないとのことです。

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

# Open source models from hugging face or Groq

**G R Shanker Sai** *Mon Jul 15 2024 19:40:58 GMT+0900 (日本標準時)* (0 votes)

Hi ,

Is it possible to use models hosted in hugging face / groq, via an api call, as i am facing lot of issues to create a langchain based agent wrapper for the local llm?



---

 # Comments from other users

> ## Matthew S Farmer
> 
> The evaluation environment does not access the internet. Model weights must be loaded into submission. Therefore, an API call that relies on an internet connection would not work. Models on HF can be used, but you need to either download the snapshot and upload or use the save pretrained function within the transformers library. Since groq would rely on an internet connection, it would not work. 
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# Hugging FaceやGroqのオープンソースモデルについて
**G R Shanker Sai** *2024年7月15日 19:40:58 (日本標準時)* (0票)
こんにちは、
ローカルのLLM用にLangChainベースのエージェントラッパーを作成する際に多くの問題に直面しているため、Hugging FaceやGroqでホスティングされているモデルをAPIコールを介して使用することは可能でしょうか？

---
# 他のユーザーからのコメント
> ## Matthew S Farmer
> 
> 評価環境ではインターネットにアクセスできません。モデルの重みは提出物にロードする必要があります。したがって、インターネット接続に依存するAPIコールは機能しません。Hugging Faceのモデルは使用できますが、スナップショットをダウンロードしてアップロードするか、transformersライブラリ内のsave_pretrained関数を使用する必要があります。Groqはインターネット接続に依存するため、機能しません。
> 
> ---


</div>