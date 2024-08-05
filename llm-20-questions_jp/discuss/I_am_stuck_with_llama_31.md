# Llama 3.1に関する問題
**VolodymyrBilyachat** *2024年8月1日 19:36:09 JST* (1票)
Llama 3.1の実行に関して助けが必要です。最新のtransformersライブラリがlibフォルダにインストールされています。そして、私のコードは以下の通りです。
```
KAGGLE_AGENT_PATH = "/kaggle_simulations/agent/"
if os.path.exists(KAGGLE_AGENT_PATH):
    print("Kaggle Env")
    sys.path.insert(0, os.path.join(KAGGLE_AGENT_PATH, 'lib'))
    HF_MODEL_PATH = os.path.join(KAGGLE_AGENT_PATH, 'model')
else:
    sys.path.insert(0, "submission/lib")
    HF_MODEL_PATH = "submission/model"
```
しかし、以下のエラーが発生しています。
nError loading model: rope_scaling must be a dictionary with two fields, type and factor, got {'factor': 8.0, 'low_freq_factor': 1.0, 'high_freq_factor': 4.0, 'original_max_position_embeddings': 8192, 'rope_type': 'llama3'}\n\n", "stderr": "Traceback (most recent call last):\n  File \"/opt/conda/lib/python3.10/site-packages/kaggle_environments/agent.py\", line 50, in get_last_callable\n    exec(code_object, env)\n  File \"/kaggle_simulations/agent/main.py\", line 48, in <module>\n    raise e\n  File \"/kaggle_simulations/agent/main.py\", line 33, in <module>\n    model = AutoModelForCausalLM.from_pretrained(\n  File \"/opt/conda/lib/python3.10/site-packages/transformers/models/auto/auto_factory.py\", line 523, in from_pretrained\n    config, kwargs = AutoConfig.from_pretrained(\n  File \"/opt/conda/lib/python3.10/site-packages/transformers/models/auto/configuration_auto.py\", line 958, in from_pretrained\n    return config_class.from_dict(config_dict, **unused_kwargs)\n  File \"/opt/conda/lib/python3.10/site-packages/transformers/configuration_utils.py\", line 768, in from_dict\n    config = cls(**config_dict)\n  File \"/opt/conda/lib/python3.10/site-packages/transformers/models/llama/configuration_llama.py\", line 161, in __init__\n    self._rope_scaling_validation()\n

---
> ## Matthew S Farmer
> 
> [ここをクリックして詳細を確認](https://www.kaggle.com/competitions/llm-20-questions/discussion/523619)
> 
> 
---
> ## Krupal Patel
> 
> ```python
> from transformers import AutoModelForCausalLM, AutoConfig
> 
> config = AutoConfig.from_pretrained('model_path')
> 
> model = AutoModelForCausalLM.from_pretrained('model_path', config=config)
> ```
> 
---
> ## Ngo Gia Lam
> 
> 試してみてください：
> ```
> !pip install --upgrade transformers
> import transformers
> print(transformers.__version__)
> ```
> 確か、llama 3.1にはtransformers >= 4.43.0が必要です。まだこのバグが発生する場合は、アップグレードを繰り返したり、ランタイムをリセットしたりしてみてください。私はランタイムを2回リセットすることでこの問題を解決しました。llama 3.1のランタイムのtransformersバージョンは4.43.3です。
> 
---
> ## Matthew S Farmer
> 
> RoPEエラーは、transformersライブラリが更新されるまで知られた問題です。ノートブックでtransformersを更新することはできますが、提出に成功した実装は見たことがありません。
