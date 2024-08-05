# 要約 
このディスカッションは、Kaggleコンペティション「LMSYS - Chatbot Arena 人間による好み予測チャレンジ」における予測の提出方法についてです。

Rikesh Prajapatiさんが、予測の提出方法について質問しています。Valentin Wernerさんが、以下の3つの方法で提出できることを説明しています。

1. **ノートブックによる提出:**
    - ノートブックを作成し、モデリングと予測を行います。
    - 予測を"id"、"winner_model_a"、"winner_model_b"、"winner_tie"という列を持つ"submission.csv"という名前のCSVファイルに保存します。
    - ノートブックをインターネットアクセスを無効にして提出します。
2. **予測の提出ページによる提出:**
    - ノートブックが上記条件を満たしていることを確認します。
    - コンペティションページの右上の「予測の提出」をクリックします。
    - 提出するノートブックとバージョン、出力ファイル（"submission.csv"のみ）を選択します。
3. **ノートブックの出力ページによる提出:**
    - 提出するノートブックに移動し、「出力」をクリックします。
    - 出力ページにも提出ボタンがあり、オプション2と同じ選択画面に移動します。

Valentin Wernerさんは、pandasを使用している場合は、インデックスなしでCSVファイルを保存する必要があることを補足しています。


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

# how to submit my predictions

**Rikesh Prajapati** *Thu May 23 2024 12:11:21 GMT+0900 (日本標準時)* (0 votes)

can anyone tell me how to submit my predictions?



---

 # Comments from other users

> ## Valentin Werner
> 
> This is a simple step-by-step guide:
> 
> 1) Create your notebook, do your modelling and predictions. Get the predictions in the right format, you want a csv file called "submission.csv" with the columns "id", "winner_model_a", "winner_model_b", "winner_tie". If you are using pandas, you want to save the csv file WITHOUT index, such as sub.to_csv('submission.csv', index=False).
> 
> 2) The notebook needs to have Internet Access disabled
> 
> 3) Actually submit your notebook by clicking on "Submit" in the sidebar.
> 
> Note that there are also other ways to submit your predictions, which do not require you to go into the editor of a notebook.
> 
> Option 2) After making sure step 1 & 2 of the above guide are still fulfilled, you can click on the "Submit Prediction" top right of this page (or any other page of the competition). There you can select a notebook and a notebook version you want to submit. There you can also specify the output file, but you can only submit files called "submission.csv". If you DID NOT save your predictions as csv, you cannot submit them.
> 
> Option 3) You can go to the notebook you want to submit and click on "Output". There you will also find a submit button, which leads you to the same selection as Option 2.
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# 予測の提出方法

**Rikesh Prajapati** *木曜日 5月 23日 2024 12:11:21 GMT+0900 (日本標準時)* (0 票)
予測の提出方法を教えてください。

---
# 他のユーザーからのコメント
> ## Valentin Werner
> 
> これは簡単なステップバイステップガイドです。
> 
> 1) ノートブックを作成し、モデリングと予測を行います。予測を正しい形式で取得します。つまり、"id"、"winner_model_a"、"winner_model_b"、"winner_tie"という列を持つ "submission.csv" という名前の CSV ファイルが必要です。pandas を使用している場合は、インデックスなしで CSV ファイルを保存する必要があります。例: sub.to_csv('submission.csv', index=False)。
> 
> 2) ノートブックはインターネットアクセスを無効にする必要があります。
> 
> 3) サイドバーの「提出」をクリックして、実際にノートブックを提出します。
> 
> ノートブックのエディタに移動しなくても、予測を提出する他の方法もあります。
> 
> オプション 2) 上記のガイドのステップ 1 と 2 が満たされていることを確認したら、このページ（またはコンペティションの他のページ）の右上の「予測の提出」をクリックできます。そこで、提出するノートブックとノートブックのバージョンを選択できます。そこで、出力ファイルも指定できますが、"submission.csv" という名前のファイルのみを提出できます。予測を CSV として保存していない場合は、提出できません。
> 
> オプション 3) 提出するノートブックに移動して、「出力」をクリックします。そこにも提出ボタンがあり、オプション 2 と同じ選択画面に移動します。
> 
> 
> 
---



</div>