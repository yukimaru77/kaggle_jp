# バグ: 回答者エージェントに最初のラウンドでキーワードが渡されていない

**monoxgas** *2024年5月22日 水曜日 10:16:36 日本標準時* (7票)

これは主催者によって確認されるべきですが、回答者エージェントが初めて使用された際に、その観察結果にキーワードが渡されていないことはほぼ確実です。

リプレイログを調べると、回答者エージェントがステップ2で空のキーワード/カテゴリ値でアクティブになっていることがわかります。また、エージェントは最初のラウンドで頻繁に簡単な質問を「幻覚」しているように見えます。この問題は、スターターノートブックのfstringが単にobs.keywordプロパティを盲目的にアクセスしているため、隠されています。これは空の文字列です。

また、この状況が発生した場合にエラーを発生させるテストコードを提出物に追加しましたが、検証中に例外が発生します。

```python
def answer(base: rg.PendingChat, observation: Observation) -> t.Literal["yes", "no"]:
    if not observation.keyword:
        print("Keyword wasn't provided to answerer", file=sys.stderr)
        raise Exception("Keyword wasn't provided to answerer")
```

例外が発生しました。
回答者エージェントに最初の質問が渡されました。
キーワードが利用できない状態で「yes」を選択しました。
---
# 他のユーザーからのコメント

> ## Bovard Doerschuk-Tiberi
> 
> ご報告ありがとうございます。確認してみます！
> 
> 
> 
--- 

