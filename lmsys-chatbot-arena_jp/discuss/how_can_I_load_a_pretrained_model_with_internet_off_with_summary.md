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
