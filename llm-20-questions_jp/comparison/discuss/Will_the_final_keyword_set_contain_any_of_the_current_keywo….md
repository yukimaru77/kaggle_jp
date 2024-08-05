# 要約 
ディスカッションでは、コンペティションにおける最終的なキーワードセットに現在のキーワードが含まれるかどうかが中心的な話題になっています。ジャスパー・ブッチャーは、成功した手法の多くが特定のキーワードセットに依存しており、最終テストセットに現在のキーワードが含まれていない場合、これらの手法が失敗する可能性があることを懸念しています。彼は、事前に設けられた質問の確認だけで十分であり、その場合にはLLM（大規模言語モデル）が必要ないと考えています。

バレンティン・バルタザールは、トップリーダーボードモデルの多くがLLMを使用していないことを指摘し、代わりに決定論的な方法で固定された質問を繰り返していることを述べています。彼は、もし完全なキーワードセットが公開されれば、LLMの必要性がさらに薄れると考えています。このように、LLMの必要性やキーワードセットの公開に関連する懸念が議論されています。

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

# Will the final keyword set contain any of the current keywords?

**Jasper Butcher** *Sun Jul 14 2024 07:52:18 GMT+0900 (日本標準時)* (3 votes)

I was wondering this since most successful methods exclusively use the keyword set and would fail horribly if none of the current keywords were in the final test set - e.g. bots which use lexicographical ordering (does the kw come before 'x' in alphabetical order etc.) rely exclusively on having access to such words beforehand.

I personally think these are far less interesting than using LLMs or other methods - you could simply write a bunch of checks see which type of such pre-built question is being asked and the competition wouldn't require any LLMs to be used…



---

 # Comments from other users

> ## Valentin Baltazar
> 
> Yea, from what I can see all the top LB models are not really using an LLM for questions….they just have some list of fixed questions that they repeat every time with deterministic guesses from the known keywords.py list. If they release the full set then they will just add those words to their list and yea…no LLM needed.
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# 最終的なキーワードセットには現在のキーワードが含まれるのでしょうか？
**ジャスパー・ブッチャー** *2024年7月14日 07:52:18 日本標準時* (3票)
このことが気になっています。成功した手法のほとんどは、キーワードセットを独占的に使用し、最終テストセットに現在のキーワードがまったく含まれていなかった場合にはひどく失敗するでしょう。たとえば、辞書順での順序付けを使用するボット（「x」より前に来るキーワードがあるかどうかなど）は、事前にそのような単語にアクセスすることに完全に依存しています。
私個人としては、LLMやその他の方法を使用するよりもはるかに興味が薄いと考えています。事前に用意された質問がどのタイプかを確認するために一連のチェックを書くだけで済むので、競技ではLLMが必要なくなってしまいます…

---
 # 他のユーザーからのコメント
> ## バレンティン・バルタザール
> 
> はい、私が見たところ、トップLBモデルのすべてが質問に対してLLMを実際には使用していないようです。彼らは単に固定された質問のリストを持っていて、それを毎回繰り返し、既知のkeywords.pyリストから決定論的に推測を行っています。もし彼らが完全なセットを公開すれば、その単語はリストに追加され、そうなれば…LLMは必要なくなります。
> 
> ---


</div>