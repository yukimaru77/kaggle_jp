# 要約 
このKaggleコンペティションのディスカッションは、ユーザーが提出時に新しいTorchバージョンをインストールできない問題について議論しています。

**問題:**

* ユーザーは提出時にTorch 2.3.1をインストールしようとしましたが、常に2.1.2のままです。
* 提出ファイルで`pip install`を使って新しいバージョンをインストールしようとしましたが、うまくいきませんでした。

**原因:**

* Valerio Morelliは、コンペティションの環境がすでにTransformersをインポートしているため、Torchも依存関係としてすでにインポートされている可能性があると指摘しています。
* mxmm2123は、コンペティションの環境が`llm_20_questions.py`ファイルを`main.py`ファイルの前に実行するため、`main.py`ファイルで新しいモデルを使用できないと説明しています。

**解決策:**

* 現時点では、ユーザーは古いモデルを使用するしかありません。
* ホストからのサポートを待つ必要があります。

**要約:**

このディスカッションは、Kaggleコンペティションの提出環境で新しいTorchバージョンをインストールできない問題について議論しています。これは、コンペティションの環境がすでにTorchをインポートしているため、ユーザーが新しいバージョンをインストールできないことが原因です。ユーザーは、ホストからのサポートを待つ必要があります。


---
# Kaggle提出環境で新しいTorchバージョンをインストールする方法

**torino** *2024年7月15日 月曜日 12:14:08 JST* (6票)

提出時に新しいTorchバージョンをインストールできた人はいますか？

提出時にTorch 2.3.1をインストールしようとしましたが、Torchのバージョンは常に2.1.2です。私の提出ファイルは以下の通りです。

```
%%writefile submission/main.py
import os
import subprocess
KAGGLE_AGENT_PATH = "/kaggle_simulations/agent/"
KAGGLE_DATA_PATH = "/kaggle_simulations/agent/"
if not os.path.exists(KAGGLE_AGENT_PATH):
    KAGGLE_AGENT_PATH = '/kaggle/working/'
    KAGGLE_DATA_PATH = "/kaggle/input/"
subprocess.run(f'pip install --no-index --find-links {KAGGLE_DATA_PATH}torch_whl torch==2.3.1', shell=True, check=True, capture_output = True)
print('ok torch')
import torch
print('torch', torch.__version__) # 2.1.2のまま
```

そして、エージェントログは以下の通りです。

```
[[{"duration": 98.399694, "stdout": "ok torch
torch 2.1.2
ok torch
torch 2.1.2
", "stderr": "Traceback (most recent call last):
  File \"/opt/conda/lib/python3.10/site-packages/kaggle_environments/agent.py\", line 56, in get_last_callable
    return [v for v in env.values() if callable(v)][-1]
IndexError: list index out of range
During handling of the above exception, another exception occurred:
Traceback (most recent call last):
  File \"/opt/conda/lib/python3.10/site-packages/kaggle_environments/agent.py\", line 159, in act
    action = self.agent(*args)
  File \"/opt/conda/lib/python3.10/site-packages/kaggle_environments/agent.py\", line 125, in callable_agent
    agent = get_last_callable(raw_agent, path=raw) or raw_agent
  File \"/opt/conda/lib/python3.10/site-packages/kaggle_environments/agent.py\", line 64, in get_last_callable
    raise InvalidArgument(\"Invalid raw Python: \" + repr(e))
kaggle_environments.errors.InvalidArgument: Invalid raw Python: IndexError('list index out of range')
"}]]
```

Torch whl データセット [torch2.3.1](https://www.kaggle.com/code/pnmanh2123/try-install-torch2-3)

私の提出テストノートブック [こちら](https://www.kaggle.com/code/pnmanh2123/try-install-torch2-3)

---

# 他のユーザーからのコメント

> ## Valerio Morelli
> 
> 私も同じ問題に遭遇しました。これは、環境がすでにここでTransformersをインポートしているためだと思います。[https://github.com/Kaggle/kaggle-environments/blob/master/kaggle_environments/envs/llm_20_questions/llm_20_questions.py](https://github.com/Kaggle/kaggle-environments/blob/master/kaggle_environments/envs/llm_20_questions/llm_20_questions.py) したがって、Torchも依存関係としてすでにインポートされています。
> 
> TorchモジュールはすでにPythonインタープリターにロードされているため、インポートは実際には新しいバージョンをインポートしていません。importlibのreloadとIPythonsのdeep reloadを試しましたが、成功しませんでした。解決策を見つけられましたか？
> 
> 
> 
> > ## mxmm2123
> > 
> > これが、新しいモデルを使用できない理由でもあります。明らかなllm_20_questions.pyファイルは常にmain.pyファイルの前に実行され、main.pyファイルは実行前にコンパイルされているため、何もできません（少なくとも私にとっては）。
> > 
> > 
> > 
> > > ## torinoTopic Author
> > > 
> > > Hi [@mxmm2123](https://www.kaggle.com/mxmm2123) [@vmorelli](https://www.kaggle.com/vmorelli) ,
> > > 
> > > 現在、私はまだ古いモデルを使用しています。Transformersの問題から、ホストからのサポートを待つしかないと思います。
> > > 
> > > 
> > > 
--- 

