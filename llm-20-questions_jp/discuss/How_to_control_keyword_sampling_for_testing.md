# キーワードのサンプリングをテスト用に制御する方法

**loh-maa** *2024年6月10日 月曜日 00:41:34 JST* (1票)

キーワードは `kaggle_environments` のインポート時に一度だけ描画されるようです。そのため、ノートブックで作業している場合、新しいキーワードでノートブックをテストするには VM をリセットする必要があります。あるいは、キーワードを再描画する方法を見落としているのかもしれません。テスト用にキーワードのサンプリングを制御する方法があれば便利です。

以下を試してみました。

```
import importlib
importlib.reload(kaggle_environments)
```

しかし、これは機能しません。

---
# 他のユーザーからのコメント

> ## RS Turley
> 
> はい、キーワードは `kaggle_environments` が "llm_20_questions" モジュールをロードしたときに設定されます。キーワードを手動で（またはランダムに）設定する最も簡単な方法は、この変数を変更することです。`alts` と `category` 変数も変更する必要があります。
> 
> 私の公開ノートブック ([https://www.kaggle.com/code/rturley/run-debug-llm-20-questions-in-a-notebook](https://www.kaggle.com/code/rturley/run-debug-llm-20-questions-in-a-notebook)) に例を載せました。関連するコードは以下のとおりです。
> 
> ```
> import kaggle_environments
> env = kaggle_environments.make(environment="llm_20_questions")
> 
> # 新しいキーワードを "Duck" に設定
> keyword = "Duck"
> alts = ["The Duck","A Duck"]
> kaggle_environments.envs.llm_20_questions.llm_20_questions.category = "Example"
> kaggle_environments.envs.llm_20_questions.llm_20_questions.keyword_obj = {'keyword':keyword,'alts':alts}
> kaggle_environments.envs.llm_20_questions.llm_20_questions.keyword = keyword
> kaggle_environments.envs.llm_20_questions.llm_20_questions.alts = alts
> 
> ```
> 
> 
> 
> > ## i_am_nothing
> > 
> > 推測者（質問者）エージェントは、環境から何らかの関数呼び出しを行うことで、最終提出時にすべての可能なキーワードを見ることができるのでしょうか？
> > 
> > 
> > 
---

