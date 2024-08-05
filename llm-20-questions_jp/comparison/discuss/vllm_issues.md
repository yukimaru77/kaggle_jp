# 要約 
ディスカッションでは、ユーザー*padeof*がvllmを使用してLLMクラスを実行しようとする中で、エラー「undefined symbol」に直面したことを共有しています。彼はこの問題を解決するために1週間奮闘しましたが、うまくいかなかったと述べています。また、vllmをサーバーとして実行する際にランダムに起動に失敗することもあると報告しています。この状況でノートブックの提出をデバッグするのが難しいと愚痴っています。

これに対して、ユーザー*Chris Deotte*がKaggleでのvLLMの使用例を提供し、必要なpipのアップグレードやファイルの修正が必要であることを指摘しています。*padeof*はその後、Chrisの投稿を読み、自身の試みが提出時に機能しないことを説明しました。具体的には、エージェントスクリプトでsysパスに変更を加える前にtorchモジュールが読み込まれてしまうため、vllmとtorchのバイナリに不一致が生じることが問題であると述べています。

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

# vllm issues

**padeof** *Sun Jul 28 2024 18:41:08 GMT+0900 (日本標準時)* (0 votes)

Anyone be able to run vllm directly by using the LLM class?

Tried to fix this "/kaggle_simulations/agent/srvlib/vllm/_C.cpython-310-x86_64-linux-gnu.so: undefined symbol" error for a week but no luck…

Running vllm as a server suffers from random start failures also.

Debugging a notebook submission is so hard 🤣



---

 # Comments from other users

> ## Chris Deotte
> 
> Here is a code example using vLLM on Kaggle. Even though vLLM is installed, we need to pip upgrade and change some files to make it work on Kaggle. [https://www.kaggle.com/code/cdeotte/infer-34b-with-vllm](https://www.kaggle.com/code/cdeotte/infer-34b-with-vllm)
> 
> 
> 
> > ## padeofTopic Author
> > 
> > Thank you! I have read your post.  However, this method does not work at submission time.  Looks like the torch module is loaded before any change made to sys path in agent script.  Thus the binary of vllm and torch do not match
> > 
> > 
> > 


---



</div>
<div class="column-right">

# 日本語訳

# vllmの問題
**padeof** *2024年7月28日 18:41:08 (日本標準時)* (0票)
誰か、LLMクラスを使って直接vllmを実行できる人はいますか？
"/kaggle_simulations/agent/srvlib/vllm/_C.cpython-310-x86_64-linux-gnu.so: undefined symbol"というエラーを解決しようと1週間試みましたが、うまくいきませんでした…
vllmをサーバーとして実行すると、ランダムに起動に失敗することもあります。
ノートブックの提出でデバッグするのが非常に難しいです🤣
---
# 他のユーザーからのコメント
> ## Chris Deotte
> 
> ここにKaggleでvLLMを使ったコード例があります。vLLMはインストールされていますが、Kaggleで動作させるためにはpipのアップグレードやいくつかのファイルを変更する必要があります。[https://www.kaggle.com/code/cdeotte/infer-34b-with-vllm](https://www.kaggle.com/code/cdeotte/infer-34b-with-vllm)
> 
> 
> > ## padeof トピック作成者
> > 
> > ありがとうございます！あなたの投稿を読みました。しかし、この方法は提出時には機能しないようです。どうやら、エージェントスクリプト内でsysパスに変更を加える前にtorchモジュールが読み込まれてしまっているようです。そのため、vllmとtorchのバイナリが一致していません。 
> > 
> > 
> >


</div>