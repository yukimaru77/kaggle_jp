# llm_20_questions.pyの役割について
**Matthew S Farmer** *2024年6月12日 05:41:55 JST* (0票)
このコンペティションにおける入力の.pyファイルの役割と、提出物のフォーマットについて考えるとき、よく理解できていません。  
入力ノートブックで定義されたエージェントは、私たちの提出物に設定されたプロンプトを上書きするのでしょうか？  
エージェントを作成する際にこの入力ファイルを参照するべきですか？  
もし答えが明白であれば申し訳ありません、私は学ぼうとしています。

---

# 他のユーザーからのコメント
> ## loh-maa
> 
> llm_20_questions.pyについて心配する必要はありません。これはゲームを実行するための環境の一部です。あなたが実装する必要があるのは、agent_fn関数です。例えば、以下のようになります：
> 
> ```
> def agent_fn(obs, cfg):
>     if obs.turnType == "ask":
>         response = "それはアヒルですか？"
>     elif obs.turnType == "answer":
>         response = "いいえ"
>     elif obs.turnType == "guess":
>         response = "アヒルが2匹"
>     return response
> ```
> 
> [このノートブック](https://www.kaggle.com/code/rturley/run-debug-llm-20-questions-in-a-notebook)が理解の助けになると思います。
> 
> ---
