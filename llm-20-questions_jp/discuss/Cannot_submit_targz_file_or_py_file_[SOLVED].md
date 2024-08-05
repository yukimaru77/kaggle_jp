# tar.gzファイルや.pyファイルを提出できない？ [解決済み]
**jazivxt** *2024年5月16日 17:50:41 GMT+0900 (日本標準時)* (2票)
提出できない
あなたのファイルはシミュレーションコンペティションの最大サイズ100 MBを超えています。
サイズはLLMの選択によって決まります。制限を満たすためにLLMを作成する必要がありますか？
---
# 他のユーザーからのコメント
> ## DJ Sterling
> 
> ご迷惑をおかけしました。実際、設定ミスがあり、現在は修正されたはずです。
> 
> > ## jazivxtトピック作成者
> > 
> > すごいですね、ありがとうございます！私もいくつかのコードエラーを修正しました。とても楽しいコンペティションになりそうです、感謝します！
> > 
> > 
> > ## Rob Mulla
> > 
> > llm_20_questions.pyファイルにバグがあることに気づきました。両方の役割が「guesser」に設定されていますが、これはリーダーボードで使用されている同じコードですか？
> > 
> > [https://github.com/Kaggle/kaggle-environments/blob/da684ac3cd41a43c8cf7e103989c98bba8d05a61/kaggle_environments/envs/llm_20_questions/llm_20_questions.py#L31](https://github.com/Kaggle/kaggle-environments/blob/da684ac3cd41a43c8cf7e103989c98bba8d05a61/kaggle_environments/envs/llm_20_questions/llm_20_questions.py#L31)
> > 
> > ```
> > GUESSER = "guesser"
> > ANSWERER = "guesser"
> > ```
> > 
> > 
---
> ## marketneutral
> 
> 「100 GB」のことを言ったのでしょうか？ルールでは最大サイズは100 GBと記載されています。
> 
> > ## jazivxtトピック作成者
> > 
> > 私のパブリックノートブックscrip5の出力から提出を試みて、メッセージには100 MBと表示されます。
> > 
> > 
---
