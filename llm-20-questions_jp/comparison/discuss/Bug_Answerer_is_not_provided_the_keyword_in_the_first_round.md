# 要約 
ディスカッションでは、ユーザー「monoxgas」が回答者エージェントが最初のラウンドでキーワードを受け取っていないことを報告しています。リプレイログの調査から、観測結果のキーワードやカテゴリが空の状態で回答者がアクティブになっていることが確認され、エージェントが「幻覚」を伴う簡単な質問をする傾向があるとの指摘があります。問題は、スタートノートブックのコードによるもので、空の値にアクセスすることで発生しています。ユーザーは、エラーを捕捉するテストコードを提出したが、バリデーション中に例外が発生することにも言及しています。最後に、「Bovard Doerschuk-Tiberi」がこの問題を確認する旨のコメントをしています。

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

# Bug: Answerer is not provided the keyword in the first round

**monoxgas** *Wed May 22 2024 10:16:36 GMT+0900 (日本標準時)* (7 votes)

This should be confirmed by the authors, but I'm fairly confident the answerer agent is not being passed the keyword in it's observation the first time it's used.

You can somewhat guess this by inspecting the replay logs, which show the answerer agents being active with empty keyword/category values on step 2. Also, agents frequently seem to "hallucinate" easy questions at the first round. This issue would be covered up by the fact that the fstring in the starter notebook simply accesses the obs.keyword prop blindly, which is an empty string.

I also added test code to our submission to raise an error if this situation ever occurs, and it does trigger the exception during validation:

```
def answer(base: rg.PendingChat, observation: Observation) -> t.Literal["yes", "no"]:
    if not observation.keyword:
        print("Keyword wasn't provided to answerer", file=sys.stderr)
        raise Exception("Keyword wasn't provided to answerer")

```

Exception Thrown

Answerer is passed the first question:

It selected 'yes' without a keyword available



---

 # Comments from other users

> ## Bovard Doerschuk-Tiberi
> 
> I'll take a look at this, thanks for reporting!
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# バグ: 回答者に最初のラウンドでキーワードが提供されていない
**monoxgas** *2024年5月22日水曜日 10:16:36 日本標準時* (7票)
これは著者によって確認されるべきですが、私は回答者エージェントが最初に使用される際にキーワードが観測結果に渡されていないとかなり自信を持っています。
リプレイログを調査することで、ステップ2でキーワードやカテゴリの値が空の状態で回答者エージェントがアクティブになっていることが見て取れます。また、エージェントは最初のラウンドで簡単な質問を「幻覚」することがよくあるようです。この問題は、スタートノートブックのfstringがobs.keywordプロパティを盲目的にアクセスしているために隠蔽されていますが、その値は空の文字列です。
この状況が発生した場合にエラーを発生させるテストコードも私たちの提出物に追加しましたが、バリデーション中に例外が発生します:
```
def answer(base: rg.PendingChat, observation: Observation) -> t.Literal["yes", "no"]:
    if not observation.keyword:
        print("回答者にキーワードが提供されていません", file=sys.stderr)
        raise Exception("回答者にキーワードが提供されていません")
```
例外発生
回答者は最初の質問を受けます:
キーワードが利用できない状態で「はい」を選択しました
---
 # 他のユーザーからのコメント
> ## Bovard Doerschuk-Tiberi
> 
> 確認してみます。報告ありがとうございます！


</div>