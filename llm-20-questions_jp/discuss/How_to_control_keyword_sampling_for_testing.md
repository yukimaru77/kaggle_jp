# キーワードサンプリングの制御方法について
**loh-maa** *2024年6月10日 00:41:34 (日本標準時)* (1票)
キーワードは、kaggle_environmentsをインポートした際に1度だけ決まるようです。そのため、ノートブックで作業していると、新しいキーワードでノートブックをテストするにはVMをリセットする必要があります。もしかしたら、キーワードを再度引き直す方法を見逃しているのかもしれません。テスト用のキーワードのサンプリングを制御する方法があれば便利です。

試したこと:
```
import importlib
importlib.reload(kaggle_environments)
```
しかし、うまくいきませんでした。

---
## 他のユーザーからのコメント
> ## RS Turley
>
> そうですね、キーワードは"kaggle_environments"が"llm_20_questions"モジュールを読み込む際に1度設定されます。キーワードを手動（またはランダム）で設定する最も簡単な方法は、この変数を変更することです。また、altsとcategoryの変数も変更する必要があります。
>
> 私の公開ノートブックに例を載せました（[こちら](https://www.kaggle.com/code/rturley/run-debug-llm-20-questions-in-a-notebook)）。関連するコードは以下の通りです:
>
> ```
> import kaggle_environments
> env = kaggle_environments.make(environment="llm_20_questions")
>
> # 新しいキーワードを「Duck」に設定
> keyword = "Duck"
> alts = ["The Duck","A Duck"]
> kaggle_environments.envs.llm_20_questions.llm_20_questions.category = "Example"
> kaggle_environments.envs.llm_20_questions.llm_20_questions.keyword_obj = {'keyword':keyword,'alts':alts}
> kaggle_environments.envs.llm_20_questions.llm_20_questions.keyword = keyword
> kaggle_environments.envs.llm_20_questions.llm_20_questions.alts = alts
> ```
>
> > ## i_am_nothing
> > 
> > 最終提出時に、私たちの推測者（質問者）エージェントは、環境からの関数を呼び出すことで、すべての可能なキーワードを見ることができるでしょうか？
