# 誰もが量子化モデルをゲーム環境にロードすることに成功しましたか？
**Matthew S Farmer** *2024年7月3日 水曜日 01:06:04 GMT+0900 (日本標準時)* (0票)

依存関係のインストール
```
import os
os.system("pip install -t /tmp/submission/lib auto-gptq optimum > /dev/null 2>&1")
```
モデルを一時フォルダに保存します。これは量子化されていないモデルでは機能しますが、検証に合格しません。
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
提出ファイル(.py)内
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
これらはすべてノートブックでは機能しますが、検証に失敗します。stderr の出力は制限されていますが、確認できる内容は次のとおりです。
```
[[{"duration": 0.166034, "stdout": "", "stderr": "Traceback (most recent call last):\n  File \"/opt/conda/lib/python3.10/site-packages/kaggle_environments/agent.py\", line 50, in get_last_callable\n    exec(code_object, env)\n  File \"/kaggle_simulations/agent/main.py\", line 13, in <module>\n    model = AutoModelForCausalLM.from_pretrained(KAGGLE_AGENT_PATH, device_map=\"cuda:0\", torch_dtype=\"auto\")\n  File \"/opt/conda/lib/python3.10/site-packages/transformers/models/auto/auto_factory.py\", line 563, in from_pretrained\n    return model_class.from_pretrained(\n  File \"/opt/conda/lib/python3.10/site-packages/transformers/modeling_utils.py\", line 3192, in from_pretrained\n    config.quantization_config = AutoHfQuantizer.merge_quantization_configs(\n  File \"/opt/conda/lib/python3.10/site-packages/transformers/quantizers/auto.py\", line 157, in merge_quantization_configs\n    quantization_config = AutoQuantizationConfig.from_dict(quantization_config)\n  File \"/opt/conda/lib/python3.10/site-packages/transformers/quantizers/auto.py\", line 87, in from_dict\n    return target_cls.fro"}]]
```
---
# 他のユーザーからのコメント
> ## Sumo
> 
> こんにちは、私は成功しました！（4ビットのチェックポイントを保存してから、提出物にロードしました）bitsandbytes と accelerate が lib にインストールされていることを確認しましたか？これらはカーネルにネイティブではなく、それらがないとロード時にエラーが発生します。
> 
> 
> 
> > ## Matthew S Farmerトピック作成者
> > 
> > bitsandbytes と accelerate が /lib ディレクトリにインストールされ、tarball に追加されていることを確認しました… stderr が切り捨てられているため、GPTQ モデルのロードに問題があるのかもしれません？わかりません。さまざまな方法を試してみます。
> > 
> > 
> > 
> > > ## Sumo
> > > 
> > > うーん、実際には、最初にモデルを量子化する際に使用された量子化構成に大きく依存します。
> > > 
> > > もう1つの点は、lib/ フォルダを sys.path の最初の項目に挿入することを確認することです。lib/ の transformers と transformers のバージョンが異なる可能性があり、バグが隠れてしまい、ノートブックでは正常にロードされているように見える可能性があります。インターネットをオフにするのも良いでしょう。HF では、ネットワーク呼び出しが隠されている可能性があります… わかりません。
> > > 
> > > 
> > > 
---

