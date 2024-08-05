# 要約 
このディスカッションは、KaggleのLMSYS - Chatbot Arena Human Preference Predictionsコンペティションにおける提出に関するエラーについてです。

AlphaTT30というユーザーは、ノートブックが正常に実行されたにもかかわらず、提出時にエラーが発生したと報告しています。エラーメッセージは表示されていませんが、BertTokenizerFastトークナイザーを使用していることが明らかになっています。

Anyaというユーザーも同様のエラーを経験しており、解決策を求めています。Anyaは、関連する別のディスカッションへのリンクを共有し、それが役に立つ可能性を示唆しています。

その後、AlphaTT30は問題を解決したと報告し、Anyaに解決策を提供する意思を示しています。

このディスカッションは、コンペティション参加者にとって役立つ情報源となり、同様のエラーが発生した場合の解決策を見つけるのに役立ちます。


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

# Getting error in sumbission.

**AlphaTT30** *Sun Jun 30 2024 21:56:50 GMT+0900 (日本標準時)* (1 votes)

Notebook successfully rans but then getting error like this 

[no idea what's going no or why happening this ] 

What to do now ? 

You're using a BertTokenizerFast tokenizer. Please note that with a fast tokenizer, using the __call__ method is faster than using a method to encode the text followed by a call to the pad method to get a padded encoding.

89.2s    2   /opt/conda/lib/python3.10/site-packages/traitlets/traitlets.py:2930: FutureWarning: --Exporter.preprocessors=["remove_papermill_header.RemovePapermillHeader"] for containers is deprecated in traitlets 5.0. You can pass --Exporter.preprocessors item … multiple times to add items to a list.

89.2s    3     warn(

89.2s    4   [NbConvertApp] WARNING | Config option kernel_spec_manager_class not recognized by NbConvertApp.

89.3s    5   [NbConvertApp] Converting notebook notebook.ipynb to notebook

89.7s    6   [NbConvertApp] Writing 32587 bytes to notebook.ipynb

91.3s    7   /opt/conda/lib/python3.10/site-packages/traitlets/traitlets.py:2930: FutureWarning: --Exporter.preprocessors=["nbconvert.preprocessors.ExtractOutputPreprocessor"] for containers is deprecated in traitlets 5.0. You can pass --Exporter.preprocessors item … multiple times to add items to a list.

91.3s    8     warn(

91.3s    9   [NbConvertApp] WARNING | Config option kernel_spec_manager_class not recognized by NbConvertApp.

91.3s    10  [NbConvertApp] Converting notebook notebook.ipynb to html

92.2s    11  [NbConvertApp] Writing 319012 bytes to results.html



---

 # Comments from other users

> ## Anya
> 
> Same situation. Waiting for resolution🤷‍♂️
> 
> 
> 
> > ## Anya
> > 
> > [https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/511861](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/511861)
> > 
> > There is a similar tag, you can check if it helps.
> > 
> > 
> > 
> > > ## AlphaTT30Topic Author
> > > 
> > > I solved my problem. Do you need a solution? 
> > > 
> > > 
> > > 


---



</div>
<div class="column-right">

# 日本語訳

# 提出でエラーが発生しています。
**AlphaTT30** *2024年6月30日 21:56:50 GMT+0900 (日本標準時)* (1 votes)
ノートブックは正常に実行されましたが、このようなエラーが発生しています。
[何が起こっているのか、なぜ起こっているのか分かりません]
どうすればいいですか？
BertTokenizerFast トークナイザーを使用しています。高速トークナイザーを使用する場合、__call__ メソッドを使用すると、テキストをエンコードするためのメソッドを使用してから pad メソッドを呼び出してパディングされたエンコーディングを取得するよりも高速です。
89.2s    2   /opt/conda/lib/python3.10/site-packages/traitlets/traitlets.py:2930: FutureWarning: --Exporter.preprocessors=["remove_papermill_header.RemovePapermillHeader"] for containers is deprecated in traitlets 5.0. You can pass --Exporter.preprocessors item … multiple times to add items to a list.
89.2s    3     warn(
89.2s    4   [NbConvertApp] WARNING | Config option kernel_spec_manager_class not recognized by NbConvertApp.
89.3s    5   [NbConvertApp] Converting notebook notebook.ipynb to notebook
89.7s    6   [NbConvertApp] Writing 32587 bytes to notebook.ipynb
91.3s    7   /opt/conda/lib/python3.10/site-packages/traitlets/traitlets.py:2930: FutureWarning: --Exporter.preprocessors=["nbconvert.preprocessors.ExtractOutputPreprocessor"] for containers is deprecated in traitlets 5.0. You can pass --Exporter.preprocessors item … multiple times to add items to a list.
91.3s    8     warn(
91.3s    9   [NbConvertApp] WARNING | Config option kernel_spec_manager_class not recognized by NbConvertApp.
91.3s    10  [NbConvertApp] Converting notebook notebook.ipynb to html
92.2s    11  [NbConvertApp] Writing 319012 bytes to results.html
---
 # 他のユーザーからのコメント
> ## Anya
> 
> 同じ状況です。解決策を待っています🤷‍♂️
> 
> 
> 
> > ## Anya
> > 
> > [https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/511861](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/511861)
> > 
> > 似たようなタグがあります。役に立つかどうか確認してください。
> > 
> > 
> > > ## AlphaTT30トピック作成者
> > > 
> > > 問題を解決しました。解決策が必要ですか？ 
> > > 
> > > 
> > > 
---



</div>