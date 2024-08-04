# Llama 3.1 でつまづいています

**VolodymyrBilyachat** *2024年8月1日 19:36:09 (日本標準時)* (1票)

Llama 3.1 を実行する際に、いくつか助けが必要なんです。最新の transformers が lib フォルダにインストールされているのですが、コードで

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

を実行すると、エラーが発生してしまいます。

```
nError loading model:rope_scalingmust be a dictionary with two fields,typeandfactor, got {'factor': 8.0, 'low_freq_factor': 1.0, 'high_freq_factor': 4.0, 'original_max_position_embeddings': 8192, 'rope_type': 'llama3'}\n\n", "stderr": "Traceback (most recent call last):\n  File \"/opt/conda/lib/python3.10/site-packages/kaggle_environments/agent.py\", line 50, in get_last_callable\n    exec(code_object, env)\n  File \"/kaggle_simulations/agent/main.py\", line 48, in <module>\n    raise e\n  File \"/kaggle_simulations/agent/main.py\", line 33, in <module>\n    model = AutoModelForCausalLM.from_pretrained(\n  File \"/opt/conda/lib/python3.10/site-packages/transformers/models/auto/auto_factory.py\", line 523, in from_pretrained\n    config, kwargs = AutoConfig.from_pretrained(\n  File \"/opt/conda/lib/python3.10/site-packages/transformers/models/auto/configuration_auto.py\", line 958, in from_pretrained\n    return config_class.from_dict(config_dict, **unused_kwargs)\n  File \"/opt/conda/lib/python3.10/site-packages/transformers/configuration_utils.py\", line 768, in from_dict\n    config = cls(**config_dict)\n  File \"/opt/conda/lib/python3.10/site-packages/transformers/models/llama/configuration_llama.py\", line 161, in __init__\n    self._rope_scaling_validation()\n
```

---
# 他のユーザーからのコメント

> ## Matthew S Farmer
> 
> [https://www.kaggle.com/competitions/llm-20-questions/discussion/523619](https://www.kaggle.com/competitions/llm-20-questions/discussion/523619)
> 
> 
> 
---
> ## Krupal Patel
> 
> from transformers import AutoModelForCausalLM, AutoConfig
> 
> config = AutoConfig.from_pretrained('model_path')
> 
> model = AutoModelForCausalLM.from_pretrained('model__path', config=config)
> 
> 
> 
---
> ## Ngo Gia Lam
> 
> 次を試してみてください。
> 
> ```
> !pip install --upgrade transformers
> import transformers
> print(transformers.__version__)
> 
> ```
> 
> 確か、Llama 3.1 には transformers 4.43.0 以上が必要だったはずです。それでもこのバグが発生する場合は、アップグレードを再試行するか、ランタイムをリセットしてみてください。ランタイムを2回リセットした後に、この問題を解決することができました。Llama 3.1 ランタイムの transformers バージョンは 4.43.3 です。
> 
> 
> 
---
> ## Matthew S Farmer
> 
> RoPE エラーは、transformers ライブラリが更新されるまでは、3.1 で発生する既知の問題です。ノートブックで transformers を更新できますが、提出に成功した実装を見たことがありません。
> 
> 
> 
---


