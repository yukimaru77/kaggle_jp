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
