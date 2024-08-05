# 要約 
ディスカッションでは、ユーザーYuang WuがモデルGemma 2 9bを使用している際に発生したエラーについて報告しています。具体的には、バリデーションプロセス中にエージェント0のログに表示されたエラーメッセージがあり、「gemma2」というモデルタイプがTransformersライブラリで認識されていないという内容です。この問題を共有したYuang Wuに対して、他のユーザーgwh666がAutoModelForCausalLMを使うべきだとアドバイスを提供しましたが、Yuang WuはAutoModelForCausalLMもAutoConfigを利用しているために解決策がわからないと述べています。その後、gwh666は特定のコードを提供し、使用を推奨しました。また、Chris DeotteはGemma2用のコードを含む最新バージョンのTransformersをpipでインストールする必要があると指摘し、Yuang Wuは既にアップデートを試みたが効果がなかったと応答しました。全体として、ユーザーたちはGemma 2 9bに関する技術的な問題とその解決策を模索しています。

---
# 提出時に別の問題に直面
**Yuang Wu** *2024年7月17日水曜日 16:15:50 JST* (1票)
現在使用しているモデルはGemma 2 9bです。バリデーションプロセス中に、エージェント0のログは次のようになり、エージェント1のログには内容がありません。
[[{"duration": 1.089666, "stdout": "", "stderr": "Traceback (most recent call last):\n  File \"/opt/conda/lib/python3.10/site-packages/transformers/models/auto/configuration_auto.py\", line 951, in from_pretrained\n    config_class = CONFIG_MAPPING[config_dict[\"model_type\"]]\n  File \"/opt/conda/lib/python3.10/site-packages/transformers/models/auto/configuration_auto.py\", line 653, in __getitem__\n    raise KeyError(key)\nKeyError: 'gemma2'\n\nDuring handling of the above exception, another exception occurred:\n\nTraceback (most recent call last):\n  File \"/opt/conda/lib/python3.10/site-packages/kaggle_environments/agent.py\", line 50, in get_last_callable\n    exec(code_object, env)\n  File \"/kaggle_simulations/agent/main.py\", line 69, in <module>\n    config = AutoConfig.from_pretrained(model_id)\n  File \"/opt/conda/lib/python3.10/site-packages/transformers/models/auto/configuration_auto.py\", line 953, in from_pretrained\n    raise ValueError(\nValueError: The checkpoint you are trying to load has model type gemma2 but Transformers does not recognize this architecture. This"}]]
この問題に直面した人はいませんか？

---
 # 他のユーザーからのコメント
> ## gwh666
> 
> 現在、AutoConfigがTransformers内でGemma-2と一致できないようです。AutoModelForCausalLMを使用してそれをロードすることができると思います。
> 
> 
> > ## Yuang Wu トピック作成者
> > 
> > おお、良いアドバイスですね、試してみます。ありがとうgwh
> > 
> > 
> > 
> > ## Yuang Wu トピック作成者
> > 
> > AutoModelForCausalLMもAutoConfigを使用するように思えます…今はどうすればいいのか分かりません
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
> > > これを試してみてください？
> > > 
> > > 
---
> ## Chris Deotte
> 
> Gemma2用のコードを含むより新しいバージョンのTransformersをpipでインストールする必要があります。
> 
> 
> > ## Yuang Wu トピック作成者
> > 
> > そうですね、Hugging Faceでのアドバイスを見ましたが、「pip install -U transformers」を既に実行しましたが、まだ効果がありません。
> > 
> > 
---
