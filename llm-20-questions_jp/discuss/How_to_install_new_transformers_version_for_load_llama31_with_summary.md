# 要約 
コンペティションのディスカッションでは、TuMinhDang氏が新しいllama3.1モデルをインストールする際に遭遇した問題について述べています。特に、transformersのバージョンが4.43.1に必要であるにもかかわらず、4.41.2に固定されてしまうエラーが発生しているとのことです。氏はアップグレードを試みたが、環境内で複数のtransformersバージョンが存在する可能性があると指摘しています。

そこで、Chris Deotte氏が提出時に必要なパッケージをインストールする方法を提案し、tarボールで提出する必要性を説明しています。TuMinhDang氏は自分の取り組みとして、tarファイルに圧縮して提出したものの、問題が解決しなかったと報告しています。

他の参加者からも同様の問題に関する質問が寄せられ、Chris Deotte氏が自身のスターターノートブックの使用を勧めており、その中にtransformersのアップグレードコードを追加すべきだとアドバイスしています。全体として、transformersパッケージのバージョン管理に関する技術的な問題とその解決策が議論されています。

---
# 新しいtransformersバージョンをインストールして llama3.1 を読み込む方法
**TuMinhDang** *2024年7月24日 17:25:21 (日本標準時)* (4票)
新しい llama3.1 モデルを使用しようとしたところ、インストール中にエラーが発生しました。transformers がアップグレードできず、動作には 4.43.1 が必要なようです。エージェントのログは以下の通りです：
```
[[{"duration": 35.35021, "stdout": "new trans\n4.41.2\n\n", "stderr": "Traceback (most recent call last):\n  File \"/opt/conda/lib/python3.10/site-packages/kaggle_environments/agent.py\", line 50, in get_last_callable\n    exec(code_object, env)\n  File \"/kaggle_simulations/agent/main.py\", line 56, in <module>\n    model = AutoModelForCausalLM.from_pretrained(model_id,\n  File \"/opt/conda/lib/python3.10/site-packages/transformers/models/auto/auto_factory.py\", line 523, in from_pretrained\n    config, kwargs = AutoConfig.from_pretrained(\n  File \"/opt/conda/lib/python3.10/site-packages/transformers/models/auto/configuration_auto.py\", line 958, in from_pretrained\n    return config_class.from_dict(config_dict, **unused_kwargs)\n  File \"/opt/conda/lib/python3.10/site-packages/transformers/configuration_utils.py\", line 768, in from_dict\n    config = cls(**config_dict)\n  File \"/opt/conda/lib/python3.10/site-packages/transformers/models/llama/configuration_llama.py\", line 161, in __init__\n    self._rope_scaling_validation()\n  File \"/opt/conda/lib/python3.10/site-packages/transformers/models/llam"}]]
```
transformers をアップグレードしなければエラーになります。以下のコードを使ってアップグレードしましたが：
```
import subprocess
subprocess.run(f'pip install --no-index --find-links "/kaggle_simulations/agent/lib" transformers', shell=True, check=True)
import transformers
from importlib import reload
transformers = reload(transformers)
print('new trans')
print(transformers.__version__) # 4.41.2
```
しかし、transformers は 4.41.2 に固定されてしまいました。誰か助けてください。
---
 # コメント
> ## davide
> 
> 誰か解決策を見つけましたか？私も同じ問題を抱えています。[@cdeotte](https://www.kaggle.com/cdeotte) の提案は私にはうまくいきませんでした…素晴らしいノートブックですが！
> 
> ---
> ## TuMinhDang（トピック作成者）
> 
> こんにちは [@cdeotte](https://www.kaggle.com/cdeotte) さん、
> 
> 新しい transformers バージョン（4.43.2 と表示されています）を提出環境にインストールしましたが、llama3.1 を読み込もうとするとエラーが発生します。どうやら環境内に 2 つの transformers バージョンがあるようで、それを処理できません。
> 
> > ## Chris Deotte
> > 
> > 提出時にインストールすることはできません。コミット時にインストールし、そのインストールファイルをタールボールに保存する必要があります。それからタールボールを提出します。
> 
> > > ## TuMinhDang（トピック作成者）
> > > 
> > > 私はインストールしてタールファイルに圧縮しましたが、その後 main.py ファイルからインストールして提出しましたが、上記のような問題が発生しました。llama 3.1 での提出を試しましたか？試してみて、提出時のエージェントログを確認してください。
> > > 
> > > > ## kumar sauryan
> > > > …llama 3.1 での提出ですか？試してみて、提出時のエージェントログを確認してみてください。
> > 
> ---
> ## Chris Deotte
> 
> 私のスターターノートブックを使用できると思います [こちら](https://www.kaggle.com/code/cdeotte/starter-code-for-llama-8b-llm-lb-0-750)。コードセル #2 に `pip install -U transformers` を追加してください。
> 
> ---
