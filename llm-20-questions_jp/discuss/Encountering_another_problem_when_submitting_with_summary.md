# 要約 
このディスカッションは、Kaggleの「LLM 20 Questions」コンペティションにおける参加者Yuang Wu氏が、Gemma 2 9b itモデルを使用した提出時にエラーが発生した問題について議論しています。

Yuang Wu氏は、検証プロセス中にエージェント0のログにエラーメッセージが表示され、エージェント1のログには内容がないことを報告しました。エラーメッセージは、TransformersライブラリがGemma 2モデルのアーキテクチャを認識していないことを示しています。

他のユーザーからのコメントでは、以下の解決策が提案されています。

* **AutoModelForCasualLMを使用する:** gwh666氏は、AutoConfigではなくAutoModelForCasualLMを使用してモデルをロードすることを提案しました。
* **Transformersの最新バージョンをインストールする:** Chris Deotte氏は、Gemma 2のコードを含む、より新しいバージョンのTransformersをpipでインストールする必要があると指摘しました。

Yuang Wu氏は、これらの解決策を試したものの、まだ問題が解決していないことを報告しました。

このディスカッションは、コンペティション参加者が直面する可能性のある技術的な問題と、コミュニティからのサポートによって解決策を見つけることができることを示しています。


---
# 提出時に別の問題が発生

**Yuang Wu** *2024年7月17日 水曜日 16:15:50 GMT+0900 (日本標準時)* (1票)

現在使用しているモデルはGemma 2 9b itです。検証プロセス中に、エージェント0のログは以下のように表示され、エージェント1のログには内容がありません。

[[{"duration": 1.089666, "stdout": "", "stderr": "Traceback (most recent call last):\n  File \"/opt/conda/lib/python3.10/site-packages/transformers/models/auto/configuration_auto.py\", line 951, in from_pretrained\n    config_class = CONFIG_MAPPING[config_dict[\"model_type\"]]\n  File \"/opt/conda/lib/python3.10/site-packages/transformers/models/auto/configuration_auto.py\", line 653, in __getitem__\n    raise KeyError(key)\nKeyError: 'gemma2'\n\nDuring handling of the above exception, another exception occurred:\n\nTraceback (most recent call last):\n  File \"/opt/conda/lib/python3.10/site-packages/kaggle_environments/agent.py\", line 50, in get_last_callable\n    exec(code_object, env)\n  File \"/kaggle_simulations/agent/main.py\", line 69, in <module>\n    config = AutoConfig.from_pretrained(model_id)\n  File \"/opt/conda/lib/python3.10/site-packages/transformers/models/auto/configuration_auto.py\", line 953, in from_pretrained\n    raise ValueError(\nValueError: The checkpoint you are trying to load has model typegemma2but Transformers does not recognize this architecture. This"}]]

この問題に遭遇した人はいますか？

---
# 他のユーザーからのコメント

> ## gwh666
> 
> AutoConfigは現在、TransformersでGemma-2と一致しないようです。AutoModelForCasualLMのみを使用してロードできます。
> 
> 
> 
> > ## Yuang Wuトピック作成者
> > 
> > 素晴らしいアドバイスですね。試してみます。ありがとうございます、gwh
> > 
> > 
> > 
> > ## Yuang Wuトピック作成者
> > 
> > AutoModelForCausalLMもAutoConfigを使用するようです… 今はわかりません
> > 
> > 
> > 
> > > ## gwh666
> > > 
> > > model = AutoModelForCausalLM.from_pretrained(
> > > 
> > >     "google/gemma-2-9b-it",
> > > 
> > >     device_map="auto",
> > > 
> > >     torch_dtype=torch.bfloat16
> > > 
> > > )
> > > 
> > > 試してみますか？
> > > 
> > > 
> > > 
---
> ## Chris Deotte
> 
> Gemma2のコードを含む、より新しいバージョンのTransformersをpipでインストールする必要があります。
> 
> 
> 
> > ## Yuang Wuトピック作成者
> > 
> > はい、Huggingfaceでそのアドバイスを見ました。しかし、すでに「pip install -U transfromers」を実行しましたが、まだ役に立ちません。
> > 
> > 
> > 
---

