# 要約 
ディスカッションでは、ユーザーのMitulが「llm_20_questions」環境を作成しようとした際に「無効な引数: 不明な環境仕様」というエラーに直面したことを報告しています。これに対し、他のユーザーが解決策を提供しています。Bovard Doerschuk-Tiberiは最新のバージョンがPyPIにプッシュされたため、通常通りpipでのインストールが機能するはずだとコメントしました。また、loh-maaはローカルにインストールしたkaggle-environmentsでも同様のエラーが発生したが、リポジトリからのインポートでエラーが解消されたと述べています。Mitulはその後、うまく動作するようになったと報告していますが、Rinku Sahuとneelpanchalは依然としてエラーに直面していることを記しています。

---
# 無効な引数: 不明な環境仕様
**Mitul** *2024年5月31日（金）16:34:41 GMT+0900 (日本標準時)* (2票)
環境を作成しようとすると、このエラーが出ます。
無効な引数                           トレースバック (最新の呼び出し最後)
Cell In[119], line 2
      1 from kaggle_environments import make
      2 env = make(environment="llm_20_questions")
File ~\PycharmProjects\kaggle.venv\Lib\site-packages\kaggle_environments\core.py:108, in make(environment, configuration, info, steps, logs, debug, state)
    106 elif has(environment, path=["interpreter"], is_callable=True):
    107     return Environment(**environment, configuration=configuration, info=info, steps=steps, logs=logs, debug=debug, state)
--> 108 raise InvalidArgument("Unknown Environment Specification")
無効な引数: 不明な環境仕様
from kaggle_environments import make
env = make(environment="llm_20_questions")
---
 # 他のユーザーからのコメント
> ## Bovard Doerschuk-Tiberi
> 
> 新しいバージョンがPyPIにプッシュされましたので、pipでのインストールが通常通りに動作するはずです。
> 
> ---
> 
> ## loh-maa
> 
> pipでローカルにインストールしたkaggle-environmentsでも同じエラーが出ますが、クローンしたリポジトリからインポートするとエラーは消えました。
> 
> > ## Mitulトピック作成者
> > 
> > ありがとうございます、うまく動作するようになりました  
> > 
> > 
> --- 
> > ## Rinku Sahu
> > 
> > どうやってやったのですか？クローンしたリポジトリを使おうとしていますが、エラーが出ます。
> > 
> ---
> 
> ## neelpanchal
> 
> 私も同じエラーが出ています。
