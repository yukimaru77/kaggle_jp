# Llama3.1 をロードするための新しい transformers バージョンのインストール方法

**TuMinhDang** *2024年7月24日 水曜日 17:25:21 JST* (4票)

新しい Llama3.1 モデルを使用しようとしましたが、インストール時にエラーが発生しました。transformers をアップグレードできないようで、実行には 4.43.1 が必要です。エージェントログは次のとおりです。

```
[[{"duration": 35.35021, "stdout": "new trans\n4.41.2\n\n", "stderr": "Traceback (most recent call last):\n  File \"/opt/conda/lib/python3.10/site-packages/kaggle_environments/agent.py\", line 50, in get_last_callable\n    exec(code_object, env)\n  File \"/kaggle_simulations/agent/main.py\", line 56, in <module>\n    model = AutoModelForCausalLM.from_pretrained(model_id,\n  File \"/opt/conda/lib/python3.10/site-packages/transformers/models/auto/auto_factory.py\", line 523, in from_pretrained\n    config, kwargs = AutoConfig.from_pretrained(\n  File \"/opt/conda/lib/python3.10/site-packages/transformers/models/auto/configuration_auto.py\", line 958, in from_pretrained\n    return config_class.from_dict(config_dict, **unused_kwargs)\n  File \"/opt/conda/lib/python3.10/site-packages/transformers/configuration_utils.py\", line 768, in from_dict\n    config = cls(**config_dict)\n  File \"/opt/conda/lib/python3.10/site-packages/transformers/models/llama/configuration_llama.py\", line 161, in __init__\n    self._rope_scaling_validation()\n  File \"/opt/conda/lib/python3.10/site-packages/transformers/models/llam"}]]
```

transformers をアップグレードしないとエラーが発生します。以下は、アップグレードに使用したコードです。

```
import subprocess
subprocess.run(f'pip install --no-index --find-links "/kaggle_simulations/agent/lib" transformers', shell=True, check=True)
import transformers
from importlib import reload
transformers = reload(transformers)
print('new trans')
print(transformers.__version__) # 4.41.2
```

しかし、transformers は 4.41.2 のままです。どなたかお助けいただけますか？

---
# 他のユーザーからのコメント

> ## davide
> 
> 誰かこの問題の解決策を見つけましたか？私も同じ問題に直面しています。残念ながら、[@cdeotte](https://www.kaggle.com/cdeotte) が提案していることは、今のところ私の場合はうまくいきません…（素晴らしいノートブックですが！）
> 
> 
> 
---
> ## TuMinhDangTopic Author
> 
> [@cdeotte](https://www.kaggle.com/cdeotte) さん、こんにちは。
> 
> 私は新しい transformers バージョン（4.43.2 と表示されます）を提出環境にインストールしましたが、Llama3.1 をロードしようとするとエラーが発生します。環境に 2 つの transformers バージョンがあるようで、対処できません。
> 
> 
> 
> > ## Chris Deotte
> > 
> > 提出中はインストールできません。コミット時にインストールし、インストールファイルを tarball に保存する必要があります。その後、tarball を提出します。
> > 
> > 
> > 
> > > ## TuMinhDangTopic Author
> > > 
> > > 私はそれをインストールして tar ファイルに圧縮し、提出時に main.py ファイルからインストールしましたが、上記のような問題が発生しました。Llama 3.1 で提出を試しましたか？試していない場合は、提出時のエージェントログを確認してみてください。
> > > 
> > > 
> > > 
> > > ## kumar sauryan
> > > 
> > > …Llama 3.1 で提出を試しましたか？試していない場合は、提出時のエージェントログを確認してみてください。
> > > 
> > > 
> > > 
---
> ## Chris Deotte
> 
> 私のスターターノートブック [こちら](https://www.kaggle.com/code/cdeotte/starter-code-for-llama-8b-llm-lb-0-750) を使用できます。コードセル #2 に `pip install -U transformers` を追加してください。
> 
> 
> 
---


