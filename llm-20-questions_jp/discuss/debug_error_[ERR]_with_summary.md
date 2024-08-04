# 要約 
このディスカッションは、Kaggleの「LLM 20 Questions」コンペティションにおけるデバッグに関するものです。ユーザーのPaul Pawlettaは、LLama 8Bのノートブックをテスト提出として実行したところ、1ラウンド目で-237のペナルティが発生したと報告しています。リプレイは問題なく動作し、エージェントログにも異常は見られないため、原因が特定できていません。

他のユーザーのwaechterは、デバッグのために提出にprint文を追加することを提案しています。また、回答がコンペティションのルールに従っているか確認するようアドバイスしています。 


---
## デバッグエラー [ERR]

**Paul Pawletta** *水曜日 7月 31日 2024 00:32:11 GMT+0900 (日本標準時)* (0票)

このコンペティションに今参加して、テスト提出として LLama 8B のノートブックを実行しました。1ラウンドまでは問題なく動作しますが、1ラウンドでエージェントが -237 のペナルティを受けます。
リプレイは最後まで問題なく動作し、エージェントログにも何も表示されません 🤷‍♂️ この問題に遭遇した人はいますか？または、デバッグする方法を知っている人はいますか？
---
# 他のユーザーからのコメント
> ## waechter
> 
> デバッグを助けるために、提出に print を追加できます。これらは stdout に表示されます。
> 
> 回答が [ルール](https://www.kaggle.com/competitions/llm-20-questions/overview/20-questions-rules) に従っていることを確認してください。
> 
> 
> 
---
