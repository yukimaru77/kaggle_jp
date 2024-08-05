# 要約 
コンペティションに関するディスカッションでは、キーワードのサンプリング制御方法についての質問が話題になっています。ユーザーのloh-maaが、kaggle_environmentsをインポートする際にキーワードが一度だけ設定されるため、新しいキーワードでテストを行うにはVMをリセットする必要があると述べています。代わりにキーワードを再度引き直す方法があるのか検討していますが、試したコードではうまくいかなかったとのことです。

これに対して、RS Turleyはキーワードを手動またはランダムに設定する方法を提案し、特定の変数を変更することが重要だと指摘しています。彼は具体的なコード例を示しながら、ノートブックでのキーワード設定手順を共有しました。

さらに、参加者のi_am_nothingは、最終提出時に質問者エージェントが環境からすべての可能なキーワードを確認できるかどうかを尋ねています。このディスカッションは、キーワードの変更やサンプリングについての実務的な考慮事項を探求している様子を示しています。

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

# How to control keyword sampling for testing?

**loh-maa** *Mon Jun 10 2024 00:41:34 GMT+0900 (日本標準時)* (1 votes)

It seems the keyword is drawn only once upon import kaggle_environments. So when working with Notebooks, it takes a VM reset to test the notebook with a new keyword, or perhaps I missed the way to re-draw the keyword? A way to control the sampling of keywords for testing would be helpful.

I tried

```
import importlib
importlib.reload(kaggle_environments)

```

but it doesn't work.



---

 # Comments from other users

> ## RS Turley
> 
> Yes, the keyword is set once kaggle_environments loads the "llm_20_questions" module. The easiest way to set the keyword manually (or randomly) is to change this variable. You'll also want to change the alts and category variables. 
> 
> I put an example in my public notebook ([https://www.kaggle.com/code/rturley/run-debug-llm-20-questions-in-a-notebook](https://www.kaggle.com/code/rturley/run-debug-llm-20-questions-in-a-notebook)), and the relevant code would be:
> 
> ```
> import kaggle_environments
> env = kaggle_environments.make(environment="llm_20_questions")
> 
> # Set the new keyword to "Duck"
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
> > Will our guesser (questioner) agent be able to look at all possible keywords in final submission by calling some function from the environment
> > 
> > 
> > 


---



</div>
<div class="column-right">

# 日本語訳

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


</div>