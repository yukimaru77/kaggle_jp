# 要約 
このディスカッションは、Kaggleの「LLM 20 Questions」コンペティションにおけるエージェント割り当てのバグに関するものです。

投稿者は、コンペティションのコード内で、`GUESSER`と`ANSWERER`の両方が"guesser"に設定されていることに気づきました。これは、回答者エージェントが質問者エージェントとして誤って割り当てられる可能性があることを意味します。

しかし、投稿者は、コードの後半でこれらの変数が適切な値に割り当てられているため、これはバグではない可能性があると指摘しています。

投稿者は、ホストにこの問題を確認し、バグがコンペティションに影響を与えていないことを確認するよう求めています。


---
# エージェント割り当てのバグについて [ホストへの確認依頼]

**Kris Smith** *2024年5月20日 月曜日 03:07:46 GMT+0900 (日本標準時)* (3票)

この件について、皆さんに確認していただきたく、新しいディスカッションスレッドを作成しました。

[@robikscube](https://www.kaggle.com/robikscube) は別のスレッドでこの問題について言及していました。

> llm_20_questions.py ファイルに、guesser と answerer の両方が "guesser" に設定されているバグがあるように見えます。これはリーダーボードで使用されているのと同じコードですか？
> [https://github.com/Kaggle/kaggle-environments/blob/da684ac3cd41a43c8cf7e103989c98bba8d05a61/kaggle_environments/envs/llm_20_questions/llm_20_questions.py#L31](https://github.com/Kaggle/kaggle-environments/blob/da684ac3cd41a43c8cf7e103989c98bba8d05a61/kaggle_environments/envs/llm_20_questions/llm_20_questions.py#L31)
> ```
> GUESSER = "guesser"
> ANSWERER = "guesser"
> ```
> 彼の投稿はこちらをご覧ください: [https://www.kaggle.com/competitions/llm-20-questions/discussion/503163#2821043](https://www.kaggle.com/competitions/llm-20-questions/discussion/503163#2821043)

私もコード内で同じことに気づきましたが、後の方で同じスクリプト内でこれらの変数が上記で定義されたメソッドを使用して割り当てられているため、無視していました。

```
agents = {GUESSER: guesser_agent, ANSWERER: answerer_agent}
```
[https://github.com/Kaggle/kaggle-environments/blob/da684ac3cd41a43c8cf7e103989c98bba8d05a61/kaggle_environments/envs/llm_20_questions/llm_20_questions.py#L87](https://github.com/Kaggle/kaggle-environments/blob/da684ac3cd41a43c8cf7e103989c98bba8d05a61/kaggle_environments/envs/llm_20_questions/llm_20_questions.py#L87)

何か見落としているのでしょうか？コードの最初に同じ値が割り当てられているように見えるのはバグのようですが、後の方では適切な新しい値が割り当てられているようです。

ホストの皆さん、これが問題を引き起こしていないことを確認していただけますか？

