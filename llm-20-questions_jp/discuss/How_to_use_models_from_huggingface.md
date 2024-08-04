# Hugging Face のモデルをどのように使用すればいいですか？
**Parashuram Chavan** *金 6月 21 2024 21:42:16 GMT+0900 (日本標準時)* (0 票)
または、Hugging Face のモデルを API を使って使用できますか？
---
# 他のユーザーからのコメント
> ## Chris Deotte
> 
> ## コードのコミット
> 
> コミット時に、モデルをダウンロードしてフォルダに保存します。
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
> pip インストールがある場合は、`/tmp/submission/lib` にインストールします。
> 
> ```
> os.system("pip install -U -t /tmp/submission/lib PACKAGE")
> 
> ```
> 
> 次に、`/tmp/submissions` フォルダ全体を `submission.tar.gz` に圧縮します。圧縮コマンドについては、Kaggle のスターターコードを参照してください。
> 
> ## コードの提出
> 
> 次に、提出時に `/tmp/submission/main.py` ファイルに以下を追加します（すべての pip インストールとモデルが動作します）。
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
> > ## Parashuram Chavanトピック作成者
> > 
> > ありがとうございます！
> > 
> > 
> > 
---

