# 要約 
ディスカッションでは、Hugging FaceのモデルをAPIで使用する方法についての質問が寄せられています。ユーザー**Parashuram Chavan**が、Hugging FaceのモデルをどのようにAPI経由で使用するかを尋ねたところ、**Chris Deotte**から具体的なコード例と手順が示されました。

具体的な内容は以下の通りです：

1. **モデルのダウンロードと保存**:
   - `AutoTokenizer`と`AutoModelForCausalLM`を使用してモデルをダウンロードし、特定のフォルダーに保存する方法が示されています。

2. **必要なパッケージのインストール**:
   - 必要なパッケージを/tmp/submission/libにインストールする方法も説明されています。

3. **圧縮と提出**:
   - 最後に、submissionフォルダーを圧縮し、main.pyファイルを使ってモデルが正しく動作するようにする手順が詳しく記載されています。

トピック作成者の**Parashuram Chavan**は、これに対して感謝の意を表しています。

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

# How to use models from huggingface?

**Parashuram Chavan** *Fri Jun 21 2024 21:42:16 GMT+0900 (日本標準時)* (0 votes)

or can i use huggingface models by API 



---

 # Comments from other users

> ## Chris Deotte
> 
> ## Commit Code
> 
> During commit, download and save the models to folder
> 
> ```
> from transformers import AutoTokenizer, AutoModelForCausalLM
> model = AutoModelForCausalLM.from_pretrained()
> tokenizer = AutoTokenizer.from_pretrained()
> model.save_pretrained("/tmp/submission/weights")
> tokenizer.save_pretrained("/tmp/submission/weights")
> 
> ```
> 
> If you have any pip installs then install into /tmp/submission/lib
> 
> ```
> os.system("pip install -U -t /tmp/submission/lib PACKAGE")
> 
> ```
> 
> Then zip up the entire /tmp/submissions folder to submission.tar.gz. See Kaggle starter code for zip commands.
> 
> ## Submit Code
> 
> Then during submit inside your /tmp/submission/main.py file add the following (and all your pip installs and models will work):
> 
> ```
> import os
> KAGGLE_AGENT_PATH = "/kaggle_simulations/agent/"
> if not os.path.exists(KAGGLE_AGENT_PATH):
>     KAGGLE_AGENT_PATH = "/tmp/submission/"
> 
> import sys
> from transformers import AutoTokenizer, AutoModelForCausalLM
> sys.path.insert(0, f"{KAGGLE_AGENT_PATH}lib")
> model = AutoModelForCausalLM.from_pretrained(
>     f"{KAGGLE_AGENT_PATH}weights/")
> tokenizer = AutoTokenizer.from_pretrained(
>     f"{KAGGLE_AGENT_PATH}weights/")
> 
> ```
> 
> 
> 
> > ## Parashuram ChavanTopic Author
> > 
> > ohh thank you sir 
> > 
> > 
> > 


---



</div>
<div class="column-right">

# 日本語訳

# Hugging Faceのモデルの使い方
**Parashuram Chavan** *2024年6月21日 金曜日 21:42:16 (日本標準時)* (0票)
Hugging FaceのモデルをAPIで使用することはできますか？

---
 # 他のユーザーからのコメント
> ## Chris Deotte
> 
> ## コードのコミット
> 
> コミット時にモデルをフォルダーにダウンロードして保存します。
> 
> ```python
> from transformers import AutoTokenizer, AutoModelForCausalLM
> model = AutoModelForCausalLM.from_pretrained()
> tokenizer = AutoTokenizer.from_pretrained()
> model.save_pretrained("/tmp/submission/weights")
> tokenizer.save_pretrained("/tmp/submission/weights")
> ```
> 
> 必要なpipインストールがあれば、それを/tmp/submission/libにインストールします。
> 
> ```python
> os.system("pip install -U -t /tmp/submission/lib PACKAGE")
> ```
> 
> 次に、/tmp/submissionsフォルダー全体をsubmission.tar.gzとして圧縮します。圧縮コマンドはKaggleのスターターコードを参照してください。
> 
> ## コードの提出
> 
> 提出時には、/tmp/submission/main.pyファイル内に次のように記述して、すべてのpipインストールとモデルが動作するようにします。
> 
> ```python
> import os
> KAGGLE_AGENT_PATH = "/kaggle_simulations/agent/"
> if not os.path.exists(KAGGLE_AGENT_PATH):
>     KAGGLE_AGENT_PATH = "/tmp/submission/"
> 
> import sys
> from transformers import AutoTokenizer, AutoModelForCausalLM
> sys.path.insert(0, f"{KAGGLE_AGENT_PATH}lib")
> model = AutoModelForCausalLM.from_pretrained(
>     f"{KAGGLE_AGENT_PATH}weights/")
> tokenizer = AutoTokenizer.from_pretrained(
>     f"{KAGGLE_AGENT_PATH}weights/")
> ```
> 
> 
> > ## Parashuram Chavan トピック作成者
> > 
> > ありがとうございます！ 
> > 
> >


</div>