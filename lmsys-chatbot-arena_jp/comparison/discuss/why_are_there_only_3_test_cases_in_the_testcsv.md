# 要約 
このディスカッションは、Kaggleコンペティション「LMSYS - Chatbot Arena 人間による好み予測チャレンジ」の参加者であるKaizhao Liang氏が、テストデータセットに含まれるデータ数が少ないことに疑問を呈したことから始まりました。

Ravi Ramakrishnan氏は、テストデータセットはコードチェック用のサンプルであり、実際のデータは非公開であると説明しました。

Kaizhao Liang氏は、インターネットアクセス不可の制約について質問し、事前トレーニング済みモデルへのアクセス方法について疑問を呈しました。

Ravi Ramakrishnan氏は、事前トレーニング済みモデルはKaggleのモデル/データセットにインポートしてから、提出用カーネルで使用することができると回答し、自身のベースライン作業を参照するように促しました。

このディスカッションは、コンペティションのデータセットとコード要件に関する参加者の疑問を解消する役割を果たしました。


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

# why are there only 3 test cases in the test.csv?

**Kaizhao Liang** *Mon May 13 2024 23:44:03 GMT+0900 (日本標準時)* (1 votes)

Is this expected?



---

 # Comments from other users

> ## Ravi Ramakrishnan
> 
> This is expected- your test data in the data page is a sample to be used for code check- the actual one is hidden [@lkz919](https://www.kaggle.com/lkz919) 
> 
> 
> 
> > ## Kaizhao LiangTopic Author
> > 
> > Ah thank you, so basically when they are running the notebook they would replace it with the hidden csv file. One additional question about no internet access, does it mean we can't access the trained models we upload ourselves when they run it? A bit confused by this constraint, and where should we download the pretrained weights if we use anything from huggingface.
> > 
> > 
> > 
> > > ## Ravi Ramakrishnan
> > > 
> > > Pre trained models need to be imported into a Kaggle model/ dataset and then used in the submission kernel [@lkz919](https://www.kaggle.com/lkz919) 
> > > 
> > > You can refer my baseline work to know more 
> > > 
> > > 
> > > 


---



</div>
<div class="column-right">

# 日本語訳

# test.csv にはなぜテストケースが3つしかないのですか？
**Kaizhao Liang** *2024年5月13日 月曜日 23:44:03 GMT+0900 (日本標準時)* (1票)
これは想定されていることでしょうか？
---
# 他のユーザーからのコメント
> ## Ravi Ramakrishnan
> 
> これは想定されています。データページのテストデータはコードチェックに使用されるサンプルであり、実際のデータは非公開です [@lkz919](https://www.kaggle.com/lkz919) 
> 
> 
> 
> > ## Kaizhao Liangトピック作成者
> > 
> > ありがとうございます。つまり、ノートブックを実行する際に、非公開の CSV ファイルに置き換えられるということですね。インターネットアクセス不可について、追加で質問があります。これは、実行時に自分自身でアップロードしたトレーニング済みモデルにアクセスできないことを意味するのでしょうか？この制約が少しわかりません。また、Hugging Face から何かを使用する場合、事前トレーニング済みウェイトはどこからダウンロードすればよいのでしょうか？
> > 
> > 
> > 
> > > ## Ravi Ramakrishnan
> > > 
> > > 事前トレーニング済みモデルは、Kaggle モデル/データセットにインポートしてから、提出用カーネルで使用してください [@lkz919](https://www.kaggle.com/lkz919) 
> > > 
> > > 詳細については、私のベースラインの作業を参照してください。
> > > 
> > > 
---



</div>