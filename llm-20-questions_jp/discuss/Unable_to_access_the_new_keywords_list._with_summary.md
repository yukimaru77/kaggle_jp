# 要約 
このディスカッションは、KaggleのLLM 20 Questionsコンペティションで、新しいキーワードリストにアクセスできないという問題についてです。

ユーザーのG R Shanker Saiは、新しいノートブックを作成してコンペティションをインプットとして追加しても、古いキーワードリストしか表示されないことを報告しています。

Chris Deotteは、新しいキーワードリストはKaggleのウェブサイトでは更新されていませんが、KaggleのGitHubリポジトリで確認できることを説明しています。また、パブリックLBには、どこにも表示されていない隠された単語も含まれており、それらを表示するには、パブリックLBでプレイされたすべてのゲームをダウンロードしてキーワードを抽出する必要があることを指摘しています。Chris Deotteは、このプロセスを自動化したパブリックノートブックとCSVファイルへのリンクを提供しています。 


---
# 新しいキーワードリストにアクセスできません。

**G R Shanker Sai** *2024年7月16日 火曜日 15:58:54 日本標準時* (1票)

新しいノートブックを作成してLLM 20 Questionsコンペティションをインプットとして追加しても、古いキーワードリストが表示されます。新しいキーワードリストを表示してアクセスするにはどうすればよいですか？
お手伝いをお願いします！🙂

---
# 他のユーザーからのコメント

> ## Chris Deotte
> 
> ファイルはKaggleのウェブサイトでは更新されていませんが、KaggleのGitHub [こちら](https://github.com/Kaggle/kaggle-environments/blob/master/kaggle_environments/envs/llm_20_questions/keywords.py)で新しいファイルを見ることができます。パブリックLBには、どこにも表示されていない隠された単語も含まれていることに注意してください。これらの隠された単語を表示するには、パブリックLBでプレイされたすべてのゲームをダウンロードしてキーワードを抽出する必要があります。これは、パブリックノートブック[こちら](https://www.kaggle.com/code/waechter/llm-20-questions-games-dataset/notebook)で行われ、CSVファイル[こちら](https://www.kaggle.com/code/waechter/llm-20-questions-games-dataset/output?select=keywords.csv)に保存されました。
> 
> 
> 
---

