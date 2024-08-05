# 要約 
このディスカッションは、Kaggleコンペティション「LMSYS - Chatbot Arena 人間による好み予測チャレンジ」に参加しているユーザーが、提出物のスコア計算エラーに遭遇した際に、その原因と解決策を探るものです。

投稿者は、初心者であり、コンペティションへの参加は初めてであることを明かし、エラーの原因を質問しています。添付された画像には、エラーメッセージが表示されています。

他のユーザーからのコメントでは、以下の可能性が指摘されています。

* **ノートブックの実行が失敗している可能性**: 実行ログを確認し、失敗した場所を特定する必要がある。
* **提出ファイルのデータ形式が正しくない可能性**: 特に、確率の合計が1を超えている場合、データ形式を確認する必要がある。
* **CSVファイル保存時の`index=False`設定が不足している可能性**: 以前はこれが問題を引き起こしていたことがある。
* **確率の合計が1を超えている可能性**: これは、ログ損失の実装に問題がないため、考えられる原因ではない。

Anyaは、自分の提出データに確率の合計が1を超えている問題があったことを認め、他のユーザーからのコメントが役に立ったことを示しています。

このディスカッションは、コンペティション参加者にとって、よくあるエラーとその解決策を理解する上で役立つ情報となっています。


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

# Submission Scoring Error

**RomanZubarev** *Wed Jun 12 2024 20:49:41 GMT+0900 (日本標準時)* (2 votes)

Hi! I'm a newbie and it's my first time participating in a competition here. Can anyone tell me why I get "Submission Scoring Error"? Everything seems to be under the rules and expectations of the result.

[2024-06-12 14-44-23.png](https://storage.googleapis.com/kaggle-forum-message-attachments/2868474/20808/2024-06-12 14-44-23.png)

---

 # Comments from other users

> ## Ahmad Al-Husainy
> 
> Was the notebook execution successful, or did it fail? If it succeeded, the only other possible reason I can think of, aside from what other Kagglers mentioned about probabilities summing up to more than one, could be the data format in the columns . If the notebook failed, you should check the execution logs, which will show you where it failed. 
> 
> 
> 


---

> ## Valentin Werner
> 
> You can try setting index=False during saving the csv, that caused problems for me before I think.
> 
> Is it because (winner_model_a + winner_model_b + winner_tie) > 1?
> 
> I don't think this should matter, as the log loss implementation is a wrapper for sklearn, where this is not an issue from my experiments
> 
> 
> 


---

> ## Masayuki Takahashi
> 
> Is it because (winner_model_a + winner_model_b + winner_tie) > 1?
> 
> 
> 
> > ## Anya
> > 
> > Good remind! I found my submission data has this problem.
> > 
> > 
> > 


---



</div>
<div class="column-right">

# 日本語訳

# 提出のスコア計算エラー

**RomanZubarev** *2024年6月12日 水曜日 20:49:41 日本標準時* (2票)
こんにちは！私は初心者で、ここで初めてコンペティションに参加します。なぜ「提出のスコア計算エラー」が発生するのか教えていただけますか？すべてがルールと結果の期待に沿っているように思えます。
[2024-06-12 14-44-23.png](https://storage.googleapis.com/kaggle-forum-message-attachments/2868474/20808/2024-06-12 14-44-23.png)
---
# 他のユーザーからのコメント
> ## Ahmad Al-Husainy
> 
> ノートブックの実行は成功しましたか、それとも失敗しましたか？成功した場合、他のKagglersが言及した確率の合計が1を超えること以外に考えられる理由は、列のデータ形式だけです。ノートブックが失敗した場合、実行ログを確認する必要があります。ログには失敗した場所が表示されます。
> 
> 
> 
---
> ## Valentin Werner
> 
> CSVを保存する際に`index=False`を設定してみてください。以前はこれが問題を引き起こしていました。
> 
> `(winner_model_a + winner_model_b + winner_tie) > 1`が原因でしょうか？
> 
> 私の実験では、これは問題ではないため、ログ損失の実装はsklearnのラッパーであるため、問題ないと思います。
> 
> 
> 
---
> ## Masayuki Takahashi
> 
> `(winner_model_a + winner_model_b + winner_tie) > 1`が原因でしょうか？
> 
> 
> 
> > ## Anya
> > 
> > 良いリマインダー！私の提出データにこの問題があることがわかりました。
> > 
> > 
> > 
---



</div>