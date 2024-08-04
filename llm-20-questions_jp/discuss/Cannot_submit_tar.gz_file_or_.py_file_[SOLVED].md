# tar.gz ファイルまたは .py ファイルを提出できませんか？ [解決済み]
**jazivxt** *2024年5月16日木曜日 17:50:41 GMT+0900 (日本標準時)* (2票)

提出できません。
ファイルがシミュレーションコンペティションの最大サイズである100MBを超えています。
サイズはLLMの選択によって決まります。制限を満たすLLMを作成する必要があるのでしょうか？
---
# 他のユーザーからのコメント
> ## DJ Sterling
> 
> ごめんなさい、確かに設定ミスがありました。今は修正されているはずです。
> 
> 
> 
> > ## jazivxtトピック作成者
> > 
> > 素晴らしい、ありがとう！コードのエラーもいくつか修正しました。とても楽しいコンペティションになりそうなので、ありがとうございます！
> > 
> > 
> > 
> > ## Rob Mulla
> > 
> > llm_20_questions.py ファイルに、guesser と answerer の両方が "guesser" に設定されているバグがあるように見えます。これはリーダーボードで使用されているのと同じコードですか？
> > 
> > [https://github.com/Kaggle/kaggle-environments/blob/da684ac3cd41a43c8cf7e103989c98bba8d05a61/kaggle_environments/envs/llm_20_questions/llm_20_questions.py#L31](https://github.com/Kaggle/kaggle-environments/blob/da684ac3cd41a43c8cf7e103989c98bba8d05a61/kaggle_environments/envs/llm_20_questions/llm_20_questions.py#L31)
> > 
> > ```
> > GUESSER = "guesser"
> > ANSWERER = "guesser"
> > 
> > ```
> > 
> > 
> > 
---
> ## marketneutral
> 
> 「100GB」の間違いではありませんか？ ルールでは最大サイズは100GBとなっています。
> 
> 
> 
> > ## jazivxtトピック作成者
> > 
> > パブリックノートブックスクリプト5の出力から提出してみましたが、メッセージには100MBと表示されています。
> > 
> > 
> > 
--- 

