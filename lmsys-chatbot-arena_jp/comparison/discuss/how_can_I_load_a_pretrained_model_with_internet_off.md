# 要約 
このディスカッションは、Kaggleコンペティションでインターネット接続なしで事前学習済みモデルをロードする方法について議論しています。

**問題:**

* ディスカッションの投稿者は、コンペティションでインターネット接続ができないため、事前学習済みモデルをロードする方法がわからないと述べています。
* Hugging Faceからモデルをダウンロードしようとしましたが、`OSError: You seem to have cloned a repository without having git-lfs installed.`というエラーが発生しました。

**解決策:**

* **モデルをローカルマシンにクローンしてKaggleのプライベートスペースにデータセットとしてアップロードする**という方法が提案されています。
* **トレーニングと推論を別々のノートブックで行い、トレーニングノートブックでモデルをダウンロード/ロード/トレーニングし、推論ノートブックでインポートする**という方法も提案されています。
* **Hugging Faceで事前学習済みモデルをダウンロードして、Kaggleにモデルとしてアップロードし、ノートブックでロードする**という方法も提案されています。

**追加情報:**

* Kaggleコンペティションのルールでは、モデルをダウンロードして使用することへの制限はありません。
* 「インターネットの無効化」とは、スコアリングのためにKaggleに提出するコードが、インターネットにアクセスできない環境で実行されることを意味します。

**結論:**

このディスカッションは、Kaggleコンペティションでインターネット接続なしで事前学習済みモデルをロードする方法について、いくつかの解決策を提案しています。これらの解決策は、モデルをローカルマシンにクローンしてKaggleにアップロードしたり、トレーニングと推論を別々のノートブックで行ったり、Hugging FaceからモデルをダウンロードしてKaggleにアップロードしたりすることです。


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

# how can I load a pretrained model with internet off

**Dirk N** *Tue May 14 2024 23:56:23 GMT+0900 (日本標準時)* (2 votes)

It seems I cannot use pip install, what is the best way to load a pretrained model with internet off?



---

 # Comments from other users

> ## RobsonDSP
> 
> I tried download a model from huggingface but until now is not working. I cloned the model to my local machine and uploaded it to my private space here on Kaggle as dataset. I uploaded all files, config.json, tf_model.h5, vocab.json and others. I tried to load them using the code bellow:
> 
> from transformers import AutoModelForSequenceClassification
> 
> from transformers import TFAutoModelForSequenceClassification
> 
> from transformers import AutoTokenizer, AutoConfig
> 
> import numpy as np
> 
> from scipy.special import softmax
> 
> MODEL = f"/kaggle/input/pretrained-model-from-huggingface/"
> 
> tokenizer = AutoTokenizer.from_pretrained(MODEL)
> 
> config = AutoConfig.from_pretrained(MODEL)
> 
> model = AutoModelForSequenceClassification.from_pretrained(MODEL)
> 
> Now I'm getting the following error message:
> 
> OSError: You seem to have cloned a repository without having git-lfs installed. Please install git-lfs and run git lfs install followed by git lfs pull in the folder you cloned.
> 
> When I run the commands in my machine it starts to download a huge file. I stopped at 1GB and the progress bar at 0%. I intended to upload this file to my account on Kaggle too but I stopped because I'm probably doing something wrong. 
> 
> I really don't know what to do now because I cannot enabled the internet access.
> 
> 
> 


---

> ## Muhammad Tariq Pervez
> 
> [@dirknbr](https://www.kaggle.com/dirknbr), Kaggle competition rules don't impose restrictions to download a model and use it. In Kaggle competitions, "disabling internet" means that the code you submit to Kaggle for scoring is executed in an environment that does not have access to the internet. Ensure your submission does not include any code that requires internet access, such as downloading data from external URLs or accessing online APIs.
> 
> 
> 


---

> ## Kishan Vavdara
> 
> Keep train and inference separate notebooks, download/load/train model in train notebook and import it in inference notebook. 
> 
> 
> 


---

> ## djchen
> 
> You can download the pertrained model on huggingface and upload it to Kaggle as a model, then you can load such pertrained model in your notebook.
> 
> 
> 


---

> ## Simon Veitner
> 
> You can clone the huggingface repository and upload it as a dataset. There are many examples how to load it from there.
> 
> Also you should check, if somebody else did it already :)
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# インターネット接続なしで事前学習済みモデルをロードするにはどうすればよいですか？

**Dirk N** *2024年5月14日 火曜日 23:56:23 JST* (2 votes)
pip install を使用できないようです。インターネット接続なしで事前学習済みモデルをロードする最良の方法は何ですか？
---
# 他のユーザーからのコメント
> ## RobsonDSP
> 
> Hugging Face からモデルをダウンロードしようとしましたが、まだうまくいきません。モデルをローカルマシンにクローンして、Kaggle のプライベートスペースにデータセットとしてアップロードしました。config.json、tf_model.h5、vocab.json などのすべてのファイルをアップロードしました。以下のコードを使用してロードしようとしました。
> 
> from transformers import AutoModelForSequenceClassification
> 
> from transformers import TFAutoModelForSequenceClassification
> 
> from transformers import AutoTokenizer, AutoConfig
> 
> import numpy as np
> 
> from scipy.special import softmax
> 
> MODEL = f"/kaggle/input/pretrained-model-from-huggingface/"
> 
> tokenizer = AutoTokenizer.from_pretrained(MODEL)
> 
> config = AutoConfig.from_pretrained(MODEL)
> 
> model = AutoModelForSequenceClassification.from_pretrained(MODEL)
> 
> すると、次のエラーメッセージが表示されます。
> 
> OSError: You seem to have cloned a repository without having git-lfs installed. Please install git-lfs and run git lfs install followed by git lfs pull in the folder you cloned.
> 
> マシンでコマンドを実行すると、巨大なファイルのダウンロードが始まります。1GB でダウンロードを停止しましたが、進捗バーは 0% のままです。このファイルを Kaggle アカウントにもアップロードしようと思いましたが、おそらく何か間違っているため、途中でやめました。
> 
> インターネットアクセスを有効にできないため、どうすればいいのか本当にわかりません。
> 
> 
> 
---
> ## Muhammad Tariq Pervez
> 
> [@dirknbr](https://www.kaggle.com/dirknbr), Kaggle コンテストのルールでは、モデルをダウンロードして使用することへの制限はありません。Kaggle コンテストでは、「インターネットの無効化」とは、スコアリングのために Kaggle に提出するコードが、インターネットにアクセスできない環境で実行されることを意味します。提出物に、外部 URL からデータのダウンロードやオンライン API へのアクセスなど、インターネットアクセスを必要とするコードが含まれていないことを確認してください。
> 
> 
> 
---
> ## Kishan Vavdara
> 
> トレーニングと推論を別々のノートブックにして、トレーニングノートブックでモデルをダウンロード/ロード/トレーニングし、推論ノートブックでインポートします。
> 
> 
> 
---
> ## djchen
> 
> Hugging Face で事前学習済みモデルをダウンロードして、Kaggle にモデルとしてアップロードできます。その後、ノートブックでその事前学習済みモデルをロードできます。
> 
> 
> 
---
> ## Simon Veitner
> 
> Hugging Face リポジトリをクローンして、データセットとしてアップロードできます。そこからロードする方法の例はたくさんあります。
> 
> また、すでに誰かがやったかどうかを確認する必要があります :)
> 
> 
> 
---


</div>