# 要約 
このディスカッションは、Kaggleコンペティションにおけるインターネットアクセスに関する制限について議論しています。

コンペティション参加者であるKamil Machalicaは、インターネットアクセスが制限されている場合に、事前学習済みモデルをダウンロードして使用できるかどうかを質問しました。

Valentin Wernerは、2つの解決策を提案しました。

1. モデルをKaggleデータセットとして保存し、Kaggleデータセットから読み込む。
2. インターネットアクセスのあるノートブックでモデルをトレーニングし、チェックポイントを保存。その後、インターネットアクセスがない別のノートブックでチェックポイントを読み込んで推論を行う。

Muhammad Tariq Pervezは、コンペティションの「インターネット無効」という条件は、提出されたコードがインターネットにアクセスできない環境で実行されることを意味すると説明しました。つまり、コード内で外部URLからのデータダウンロードやオンラインAPIへのアクセスは許可されていません。

このディスカッションは、コンペティション参加者がインターネットアクセスに関する制限を理解し、それに対応する適切な方法を見つけるのに役立ちます。


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

# Internet access condition

**Kamil Machalica** *Fri May 17 2024 21:07:02 GMT+0900 (日本標準時)* (1 votes)

Hi Kagglers!

If there is internet access restrictions can we even use pre-trained models to download them?

Thanks

Kamil



---

 # Comments from other users

> ## Valentin Werner
> 
> There are several things you can do, and what is often done:
> 
> 1) You can download the models, save them as kaggle dataset, load them from kaggle dataset instead (same goes for pip installs you might want to do)
> 
> 2) You can train models in one notebook with internet access, save the model checkpoint at the end and then create a separate notebook without internet access. Then you can simply add the training notebook as input for the inference notebook!
> 
> Hope this helps, welcome to kaggle and good luck!
> 
> 
> 
> > ## Kamil MachalicaTopic Author
> > 
> > Thank you, it explains a lot!
> > 
> > 
> > 


---

> ## Muhammad Tariq Pervez
> 
> [@machalx](https://www.kaggle.com/machalx), In Kaggle competitions, "disabling internet" means that the code you submit to Kaggle for scoring is executed in an environment that does not have access to the internet. Ensure your submission does not include any code that requires internet access, such as downloading data from external URLs or accessing online APIs.
> 
> Otherwise no issue. 
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# インターネットアクセスに関する条件

**Kamil Machalica** *2024年5月17日 金曜日 21:07:02 日本標準時* (1票)
Kaggleの皆さん、こんにちは！
インターネットアクセスが制限されている場合、事前学習済みモデルをダウンロードして使用することは可能でしょうか？
よろしくお願いします。
Kamil

---
# 他のユーザーからのコメント
> ## Valentin Werner
> 
> いくつかできることがありますし、よく行われている方法もあります。
> 
> 1) モデルをダウンロードしてKaggleデータセットとして保存し、Kaggleデータセットから読み込むことができます（pipインストールについても同様です）。
> 
> 2) インターネットアクセスのあるノートブックでモデルをトレーニングし、最後にモデルのチェックポイントを保存します。その後、インターネットアクセスがない別のノートブックを作成します。そして、トレーニングノートブックを推論ノートブックの入力として追加するだけです！
> 
> お役に立てれば幸いです。Kaggleへようこそ、頑張ってください！
> 
> 
> 
> > ## Kamil Machalica トピック作成者
> > 
> > ありがとうございます。よくわかりました！
> > 
> > 
> > 
---
> ## Muhammad Tariq Pervez
> 
> [@machalx](https://www.kaggle.com/machalx) 、Kaggleコンペティションでは、「インターネット無効」とは、Kaggleに提出してスコア付けを行うコードが、インターネットにアクセスできない環境で実行されることを意味します。提出物に、外部URLからデータのダウンロードやオンラインAPIへのアクセスなど、インターネットアクセスを必要とするコードが含まれていないことを確認してください。
> 
> それ以外は問題ありません。
> 
> 
> 
--- 



</div>