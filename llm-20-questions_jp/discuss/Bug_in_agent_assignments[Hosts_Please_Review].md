# エージェントの割り当てに関するバグ[ホストの確認をお願いします]
**クリス・スミス** *2024年5月20日 03:07:46 GMT+0900 (日本標準時)* (3票)

この問題について多くの人に目を向けてもらうために新しいディスカッションスレッドを始めることにしました。
[@robikscube](https://www.kaggle.com/robikscube)が別のスレッドで言及していたのですが、
llm_20_questions.pyファイルにおいて、guessとanswerの両方が「guesser」と設定されるバグがあるようです。これはリーダーボードで使用されているコードと同じなのでしょうか？
[こちらのリンク](https://github.com/Kaggle/kaggle-environments/blob/da684ac3cd41a43c8cf7e103989c98bba8d05a61/kaggle_environments/envs/llm_20_questions/llm_20_questions.py#L31)にご覧ください。
```
GUESSER = "guesser"
ANSWERER = "guesser"
```
彼の投稿は[こちらで確認できます](https://www.kaggle.com/competitions/llm-20-questions/discussion/503163#2821043)。
私も同様のことに気づきましたが、無視していました。その理由は、スクリプトの後半でそれらの変数が上で定義されたメソッドを使用して新たに割り当てられているからです：
```
agents = {GUESSER: guesser_agent, ANSWERER: answerer_agent}
```
[こちらのリンク](https://github.com/Kaggle/kaggle-environments/blob/da684ac3cd41a43c8cf7e103989c98bba8d05a61/kaggle_environments/envs/llm_20_questions/llm_20_questions.py#L87)にご覧ください。
私は何か見落としているのでしょうか？最初に同じ値が割り当てられた後、さらに下の部分では適切な新しい値が割り当てられるように見えます。
ホストの方々、この問題が実際に影響を及ぼしていないことを確認していただけますか？
