# 新しいQ20LLMデータセット、78,000以上の質問を含む

**ivan** *2024年5月28日 火曜日 02:34:18 GMT+0900 (日本標準時)* (3票)

こんにちは。最近、[Mistral AIハッカソン](https://x.com/MistralAILabs/status/1788970688172245256) で、[Mistral API](https://docs.mistral.ai/api/) と [Groq Cloud](https://docs.mistral.ai/api/) の提供するAPIを使って新しいデータセット [Q20LLM](https://huggingface.co/datasets/cvmistralparis/Q20LLM) を作成しました。

私の知る限り、一般的な質問から具体的な質問へと進むような対話形式の質問を含むデータセットはありません。そこで、LLMを使ってそのような対話を構築してみました。また、このデータセットを使って「指示に従う」モデルをファインチューニングしてみましたが、成功しませんでした。モデルは、トレーニング中に見ただけ多くの質問をしてしまう傾向があります。 

