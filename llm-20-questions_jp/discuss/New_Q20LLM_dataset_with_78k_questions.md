# 新しいQ20LLMデータセットが登場、78,000以上の質問を収録
**ivan** *2024年5月28日 02:34:18 GMT+0900 (日本標準時)* (3票)
こんにちは、最近[ミストラルAIハッカソン](https://x.com/MistralAILabs/status/1788970688172245256)で提供されたAPIを利用して、新しいデータセット[Q20LLM](https://huggingface.co/datasets/cvmistralparis/Q20LLM)を作成しました。APIは[Mistral API](https://docs.mistral.ai/api/)と[Groq Cloud](https://docs.mistral.ai/api/)から提供されました。
私の知る限り、一般的な質問から具体的な質問までの対話形式のデータセットは存在ません。このような対話をLLMを使って構築しようと試みました。また、このデータセットを使って「指示に従う」モデルのファインチューニングも試みましたが、成功しませんでした。モデルは、訓練中に見た質問の数だけ質問をしようとする傾向があります。
