# 要約 
このディスカッションは、Kaggleの「LLM 20 Questions」コンペティションの参加者が、`kaggle_environments`ライブラリを使って環境を作成しようとした際に発生したエラーに関するものです。

**問題:**

* ユーザーは`env = make(environment="llm_20_questions")`を実行した際に、`InvalidArgument: Unknown Environment Specification`というエラーが発生しました。

**解決策:**

* Bovard Doerschuk-Tiberiは、PyPIに新しいバージョンの`kaggle_environments`がプッシュされたことを指摘し、pip installで問題が解決する可能性を示唆しました。
* loh-maaは、pipでローカルにインストールした`kaggle_environments`ではエラーが発生するものの、クローンされたリポジトリからインポートするとエラーが解消されたと報告しました。
* Mitulは、loh-maaの解決策で問題が解決したことを確認しました。
* Rinku Sahuは、クローンされたリポジトリを使用しようとした際にエラーが発生したと報告しました。
* neelpanchalも同様のエラーが発生したと報告しました。

**結論:**

このディスカッションは、`kaggle_environments`ライブラリに関連する問題と、その解決策について議論しています。pip installで最新バージョンをインストールするか、クローンされたリポジトリからインポートすることで、エラーを解決できる可能性があります。しかし、Rinku Sahuとneelpanchalのコメントから、まだ解決されていない問題がある可能性も示唆されています。


---
# 無効な引数: 未知の環境仕様
**Mitul** *2024年5月31日 金曜日 16:34:41 GMT+0900 (日本標準時)* (2票)

環境を作成しようとした際に、このエラーが発生しました。

```python
InvalidArgument                           Traceback (most recent call last)
Cell In[119], line 2
      1 from kaggle_environments import make
      2 env = make(environment="llm_20_questions")
File ~\PycharmProjects\kaggle.venv\Lib\site-packages\kaggle_environments\core.py:108, in make(environment, configuration, info, steps, logs, debug, state)
    106 elif has(environment, path=["interpreter"], is_callable=True):
    107     return Environment(**environment, configuration=configuration, info=info, steps=steps, logs=logs, debug=debug, state=state)
--> 108 raise InvalidArgument("Unknown Environment Specification")
InvalidArgument: Unknown Environment Specification
from kaggle_environments import make
env = make(environment="llm_20_questions")
```

---
# 他のユーザーからのコメント
> ## Bovard Doerschuk-Tiberi
> 
> PyPI に新しいバージョンがプッシュされました。pip install は正常に動作するはずです。
> 
> 
> 
---
> ## loh-maa
> 
> pip を介してローカルにインストールされた kaggle-environments を使用した場合も同じエラーが発生しますが、クローンされたリポジトリからインポートするとエラーはなくなります。
> 
> 
> 
> > ## MitulTopic Author
> > 
> > ありがとうございます。これで動作します。
> > 
> > 
> > 
> > ## Rinku Sahu
> > 
> > どうやってやったのですか？クローンされたリポジトリを使用しようとしていますが、エラーが発生しています。
> > 
> > 
> > 
---
> ## neelpanchal
> 
> 私も同じエラーが発生しています。
> 
> 
> 
--- 

