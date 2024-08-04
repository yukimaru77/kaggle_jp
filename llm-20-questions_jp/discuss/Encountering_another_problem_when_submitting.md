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
