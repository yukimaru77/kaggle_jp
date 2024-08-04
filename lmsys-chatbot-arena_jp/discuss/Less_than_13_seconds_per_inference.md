# 推論時間1.3秒以下？

**Rishiraj Acharya** *2024年5月3日 金曜日 14:21:19 日本標準時* (17票)

テストデータは約25,000行あり、9時間のランタイムは推論あたり1.3秒未満になります。これは、このコンペティションで大型言語モデルの使用を無効にするのでしょうか？私はこれほど高速に動作するLLMを知りませんが、学ぶことに意欲的です。
---
# 他のユーザーからのコメント
> ## Raja Biswas
> 
> 私の提出では、推論時間は以下の通りでした（T4 x2）：
> 
> - deberta-v3-large（約1.5時間）
> 
> - mistral 7b（約4時間）
> 
> - llama3 8b（約4時間）
> 
> 使用された最大シーケンス長：1.8k
> 
> 
> 
---
> ## Siddhantoon
> 
> データをバッチ処理することもできます。なぜすべての行を順番に実行するのですか？
> 
> 
> 
---
> ## Fritz Cremer
> 
> 私は1時間以内に予測するdeberta-v3-baseのノートブックを公開しました。deberta-v3-largeでも問題ないと思います。
> 
> [https://www.kaggle.com/code/fritzcremer/lmsys-deberta-v3-base-baseline](https://www.kaggle.com/code/fritzcremer/lmsys-deberta-v3-base-baseline)
> 
> 
> 
---
> ## Angela
> 
> あなたは正しいです。このコンペティションでは、LLMのプ rompt エンジニアリングを利用できないようです。
> 
> 
> 
---

