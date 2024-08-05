# 要約 
ディスカッションでは、ユーザーのjazivxtがtar.gzファイルや.pyファイルの提出に関する問題を提起しました。ファイルサイズがシミュレーションコンペティションの最大サイズ100 MBを超えているため、提出できないという内容です。その後、他の参加者からのコメントがあり、DJ Sterlingが設定ミスを修正したことを伝え、jazivxtは感謝の意を示しました。また、Rob Mullaは、ファイルのコード内にバグがあり、両役割が「guesser」に設定されていることを指摘しました。さらに、marketneutralがルールでは最大サイズが100 GBと記載されていると指摘したのに対し、jazivxtは自身の試みが100 MBの制限を示していることを明らかにしました。

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

# Cannot submit tar.gz file or .py file? [SOLVED]

**jazivxt** *Thu May 16 2024 17:50:41 GMT+0900 (日本標準時)* (2 votes)

Cannot submit

Your file exceeds the Simulations Competition maximum size of 100 Mb.

The size is driven by the LLM choice.  Are we supposed to create an LLM to meet the limit?



---

 # Comments from other users

> ## DJ Sterling
> 
> Sorry about that, indeed we had a misconfiguration which should be fixed now.
> 
> 
> 
> > ## jazivxtTopic Author
> > 
> > Awesome, thanks!  I also had some code errors that have now been corrected. Looks like it will be a very fun competition, thank you!
> > 
> > 
> > 
> > ## Rob Mulla
> > 
> > We noticed that in the llm_20_questions.py file there looks to be a bug where both guesser and answerer are set as "guesser". Is this the same code used on the leaderboard?
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
> Did you mean "100 GB"? The maximum size in the rules says 100 GB.
> 
> 
> 
> > ## jazivxtTopic Author
> > 
> > Try submitting from my public notebook scrip5 output, message indicates 100 Mb
> > 
> > 
> > 


---



</div>
<div class="column-right">

# 日本語訳

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


</div>