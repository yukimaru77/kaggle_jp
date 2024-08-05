# 要約 
コンペのディスカッションでは、参加者のGODDiaoが、llm_20_questions.pyのコードにおいて「active」や「inactive」といったオブジェクトが十分に説明されていないことに気づき、obsオブジェクトのメソッド（obs.turnTypeやobs.questionなど）についての情報をどこで確認できるかを尋ねています。それに対して、Bovard Doerschuk-Tiberiが、デバッグモードで実行し、`print(dir(obs))`を使うことで利用できるオブジェクトの詳細を確認できると回答しています。

---
# 観察に関するちょっとした質問
**GODDiao** *2024年6月2日 16:32:43 JST* (1票)
llm_20_questions.pyのコードを読んでみたところ、activeやinactiveといった多くのオブジェクトが明確に説明されていないことに気付きました。
obsのようなオブジェクトのメソッド（obs.turnTypeやobs.questionなど）をどこで見ることができるのか、気になっています。
---
 ## ユーザーからのコメント
> ## Bovard Doerschuk-Tiberi
> 
> debugモードで実行し、print(dir(obs))を使えば、そこにあるすべてのものが表示されるはずですよ！
