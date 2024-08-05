# 要約 
ディスカッションの要約:

ユーザー「torino」は、Kaggleの提出環境で新しいPyTorchバージョン（2.3.1）をインストールしようとしたが、常にバージョン2.1.2のままであることに困惑している。提案されたコードを使用してインストールを試みたが、エージェントログでは新しいバージョンに成功せずエラーが表示された。彼はtorchの新しいバージョンをインストールするための作業を共有している。

中には「Valerio Morelli」や「mxmm2123」といった他のユーザーも参加し、transformersライブラリが先にインポートされているために新しいtorchバージョンが正しく読み込まれない可能性について言及している。また、llm_20_questions.pyファイルが実行前に常にコンパイルされるため、ユーザー側での解決策が限られているとも指摘している。

最終的に、「torino」は今は古いモデルを使用し続けるしかないと結論づけており、ホストからのサポートを待つ意向を示している。

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

# How to install new torch version in kaggle submit environment?

**torino** *Mon Jul 15 2024 12:14:08 GMT+0900 (日本標準時)* (6 votes)

Has anyone successfully installed the new torch version when submit?

i try to install torch 2.3.1 when submit but torch version always is 2.1.2, my submit file like:

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
print('torch', torch.__version__) # stuck in 2.1.2

```

then agent log:

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

torch whl dataset [torch2.3.1](https://www.kaggle.com/code/pnmanh2123/try-install-torch2-3)

my submit test notebook  [here](https://www.kaggle.com/code/pnmanh2123/try-install-torch2-3)



---

 # Comments from other users

> ## Valerio Morelli
> 
> I ran into the same problem and believe it's due to the environment already importing transformers here [https://github.com/Kaggle/kaggle-environments/blob/master/kaggle_environments/envs/llm_20_questions/llm_20_questions.py](https://github.com/Kaggle/kaggle-environments/blob/master/kaggle_environments/envs/llm_20_questions/llm_20_questions.py) and therefore also importing torch already as a dependency.
> 
> Since the torch module is already loaded in the Python interpreter your import does not actually import the new version. I tried importlib's reload and IPythons deep reload with no success. Did you manage do find a solution?
> 
> 
> 
> > ## mxmm2123
> > 
> > This is also why we can't use a newer model. That clear llm_20_questions.py file always runs before the main.py file, and the main.py file was compiled before running, so we can't do anything(at least for me).
> > 
> > 
> > 
> > > ## torinoTopic Author
> > > 
> > > Hi [@mxmm2123](https://www.kaggle.com/mxmm2123) [@vmorelli](https://www.kaggle.com/vmorelli) ,
> > > 
> > > I currently still using older models, with the transformers issue I think we can only wait for support from the host.
> > > 
> > > 
> > > 


---



</div>
<div class="column-right">

# 日本語訳

# Kaggleの提出環境で新しいtorchバージョンをインストールする方法
**torino** *2024年7月15日 12:14 (日本標準時)* (6票)
提出時に新しいtorchバージョンをインストールすることに成功した人はいますか？
提出時にtorch 2.3.1をインストールしようとしましたが、torchのバージョンは常に2.1.2のままです。私の提出ファイルは以下の通りです：
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
print('torch', torch.__version__) # 2.1.2で止まってしまう
```
その後のエージェントログ：
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
torch whlデータセット [torch2.3.1](https://www.kaggle.com/code/pnmanh2123/try-install-torch2-3)
私の提出テストノートブック [こちら](https://www.kaggle.com/code/pnmanh2123/try-install-torch2-3)
---
 # 他のユーザーからのコメント
> ## Valerio Morelli
> 
> 私も同じ問題に遭遇したと思いますが、これは環境がすでにtransformersをインポートしているために発生しています。こちらをご覧ください：[kaggle_environments](https://github.com/Kaggle/kaggle-environments/blob/master/kaggle_environments/envs/llm_20_questions/llm_20_questions.py)。そのため、torchも依存関係としてすでにインポートされています。
> 
> Pythonインタープリターですでにtorchモジュールが読み込まれているため、新しいバージョンが実際にはインポートされません。私はimportlibのreloadやIPythonのdeep reloadを試みましたが、成功しませんでした。何か解決策を見つけましたか？

> > ## mxmm2123
> > 
> これは、より新しいモデルを使用できない理由でもあります。このllm_20_questions.pyファイルは、main.pyファイルの前に常に実行され、main.pyファイルは実行前にコンパイルされるため、私たちには何もできないようです（少なくとも私には）。
> 
> > > ## torinoトピック作成者
> > > > こんにちは[@mxmm2123](https://www.kaggle.com/mxmm2123) [@vmorelli](https://www.kaggle.com/vmorelli) ,
> > > >
> > > > 現在、私は古いモデルを使用しています。transformersの問題については、ホストからのサポートを待つしかないと思います。
> > > >
> > > > >


</div>