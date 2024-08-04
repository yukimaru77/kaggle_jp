# 要約 
このディスカッションは、Kaggleの「LLM 20 Questions」コンペティションの参加者であるGODDiaoさんが、コンペティションのコード `llm_20_questions.py` にある `active` や `inactive` などのオブジェクトの説明が不明確であること、および `obs.turnType` や `obs.question` などのオブジェクトのメソッドがどこで見られるのかを質問したことから始まりました。

Bovard Doerschuk-Tiberiさんは、GODDiaoさんの質問に対して、`print(dir(obs))` を追加してデバッグモードで実行すれば、オブジェクトに含まれるすべてのものが表示されると回答しました。 


---
# 観察に関するおかしな質問

**GODDiao** *2024年6月2日 日曜日 16:32:43 JST* (1票)

`llm_20_questions.py` のコードを読みました。`active` や `inactive` などのオブジェクトの説明が明確ではありませんでした。

`obs.turnType` や `obs.question` などのオブジェクトのメソッドはどこで見ることができますか？

---

# 他のユーザーからのコメント

> ## Bovard Doerschuk-Tiberi
> 
> `print(dir(obs))` を追加してデバッグモードで実行すると、そこに含まれるすべてのものが表示されます！
> 
> 
> 
--- 

