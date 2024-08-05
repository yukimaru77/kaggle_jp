# 要約 
ディスカッションでは、参加者の**Matthew S Farmer**が量子化モデルをゲーム環境でロードする際の問題について投稿しました。彼は、依存関係のインストールを行ったものの、バリデーションには合格しなかったと述べています。コード例やエラーメッセージを共有し、具体的な問題点を明らかにしました。

他のユーザーである**Sumo**は、自分は成功したとし、量子化モデルを正しく読み込むためには、`bitsandbytes`と`accelerate`が正しくインストールされている必要があることを指摘しました。また、必要に応じて`lib/`フォルダを`sys.path`の先頭に挿入するよう勧めています。これにより、異なるバージョンのライブラリが原因でエラーが発生するリスクを減らせると説明しました。要するに、モデルの量子化と依存ライブラリの適切な管理が重要であるという内容です。

---
# 誰か、ゲーム環境で量子化モデルをロードすることに成功した人はいますか？
**Matthew S Farmer** *2024年7月3日 01:06:04 (日本標準時)* (0票)
依存関係のインストール
```
import os
os.system("pip install -t /tmp/submission/lib auto-gptq optimum > /dev/null 2>&1")
```
モデルを/tmpフォルダに保存します。これは非量子化モデルには成功しますが、バリデーションに合格しません。
```
from transformers import BitsAndBytesConfig, AutoTokenizer, AutoModelForCausalLM
model_id = 'private/my_quant_model_int4'
tokenizer = AutoTokenizer.from_pretrained("model_id")
model = AutoModelForCausalLM.from_pretrained(
    "model_id",
    device_map="cuda:0"
)
model.save_pretrained("/tmp/submission/")
tokenizer.save_pretrained("/tmp/submission/")
```
私の提出ファイル内の.py
```
import os
import sys
KAGGLE_AGENT_PATH = "/kaggle_simulations/agent/"
if not os.path.exists(KAGGLE_AGENT_PATH):
    KAGGLE_AGENT_PATH = "/tmp/submission/"
import sys
from transformers import AutoTokenizer, AutoModelForCausalLM, BitsAndBytesConfig
model = AutoModelForCausalLM.from_pretrained(KAGGLE_AGENT_PATH, device_map="cuda:0", torch_dtype="auto")
tokenizer = AutoTokenizer.from_pretrained(KAGGLE_AGENT_PATH)
```
これらすべてはノートブックで機能しますが、バリデーションに失敗します。stderrの出力は制限されていますが、以下のようなエラーメッセージが表示されています：
```
[[{"duration": 0.166034, "stdout": "", "stderr": "Traceback (most recent call last):\n  File \"/opt/conda/lib/python3.10/site-packages/kaggle_environments/agent.py\", line 50, in get_last_callable\n    exec(code_object, env)\n  File \"/kaggle_simulations/agent/main.py\", line 13, in <module>\n    model = AutoModelForCausalLM.from_pretrained(KAGGLE_AGENT_PATH, device_map=\"cuda:0\", torch_dtype=\"auto\")\n  File \"/opt/conda/lib/python3.10/site-packages/transformers/models/auto/auto_factory.py\", line 563, in from_pretrained\n    return model_class.from_pretrained(\n  File \"/opt/conda/lib/python3.10/site-packages/transformers/modeling_utils.py\", line 3192, in from_pretrained\n    config.quantization_config = AutoHfQuantizer.merge_quantization_configs(\n  File \"/opt/conda/lib/python3.10/site-packages/transformers/quantizers/auto.py\", line 157, in merge_quantization_configs\n    quantization_config = AutoQuantizationConfig.from_dict(quantization_config)\n  File \"/opt/conda/lib/python3.10/site-packages/transformers/quantizers/auto.py\", line 87, in from_dict\n    return target_cls.fro"}]]
```
---
# 他のユーザーからのコメント
> ## Sumo
> 
> こんにちは、私は成功しました！(4ビットのチェックポイントを保存し、再度読み込むことで) bitsandbytesとaccelerateがlibにインストールされていることを確認しましたか？これらはカーネルにネイティブではないため、ロード時にエラーが発生します。
> 
> > ## Matthew S Farmer (トピック作成者)
> > 
> > 私はbitsandbytesとaccelerateが/libディレクトリにインストールされ、tarballに追加されたことを確認しました… stderrが切り詰められているため、GPTQモデルのロードに問題があるかもしれません。不明ですが、異なる方法を試してみます。
> > 
> > > ## Sumo
> > > 
> > > 実際にモデルを量子化するために使用された量子化構成によって、かなりの部分が依存します。  
> > > 
> > > もう一つのことは、lib/フォルダをsys.pathの最初のアイテムとして挿入することです。lib/内のtransformersと他のtransformersが異なるバージョンであるかもしれず、これがバグを隠すことがあり、ノートブック内でうまく読み込まれているように見えるかもしれません。また、隠れたネットワーク呼び出しがあるかもしれないので、インターネットをオフにするのも良いでしょう…Hugging Faceについては、私たちは決してわからないです。
