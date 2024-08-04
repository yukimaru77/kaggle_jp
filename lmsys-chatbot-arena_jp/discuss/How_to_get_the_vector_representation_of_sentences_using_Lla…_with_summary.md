# 要約 
このディスカッションは、KaggleのLMSYS - Chatbot Arena Human Preference Predictionsコンペティションにおける、Llama3モデルを用いた文章のベクトル表現取得に関するものです。

投稿者は、ファインチューニングされたLlama3モデルから、応答の埋め込みを取得する方法を探しています。これは、埋め込みを他の分類器に供給することで、より精度の高い予測を行うことを目指しているためです。

コメント欄では、RB氏が`output_hidden_states=True`をモデル初期化時に渡すことで、隠れ状態を取得できることを指摘しています。投稿者は、これが求めている情報であることを確認し、感謝の言葉を述べています。

要約すると、このディスカッションは、Llama3モデルを用いて文章のベクトル表現を取得する方法について、具体的な解決策を提示したものです。


---
# Llama3を使って文章のベクトル表現を取得する方法

**godmysalary** *2024年6月28日 金曜日 17:22:14 JST* (0票)

皆さん、こんにちは！現在、ほとんどのパブリックノートブックでは、ファインチューニングと予測確率の取得に直接「LlamaForSequenceClassification」を使用しています。私は、予測に加えて、response_aとresponse_bの学習済み埋め込みを取得する方法を知りたいと思っています。なぜなら、埋め込みは他の異なる分類器に供給できると思うからです。時間制約のため、別のLLMを使用したくありません。そこで、ファインチューニングされたLlama3の副産物として、応答の埋め込みを取得する方法を教えていただけますか？よろしくお願いします。

---
# 他のユーザーからのコメント

> ## RB
> 
> モデルの初期化時に`output_hidden_states=True`を渡すことができます。以下のような感じです。
> 
> ```
> model  = AutoModelForCausalLM.from_pretrained(model_path, quantization_config=quantization_config, output_hidden_states=True)
> 
> out = model(input_ids = tokenized['input_ids'], attention_mask = tokenized['attention_mask'])
> 
> out.hidden_states
> 
> ```
> 
> 
> 
> > ## godmysalaryTopic Author
> > 
> > ありがとうございます！
> > 
> > 
> > 
---
> ## 表示名を入力してください
> 
> あなたが求めているのは、モデルの出力の最後の隠れ状態ではないでしょうか？
> 
> 
> 
> > ## godmysalaryTopic Author
> > 
> > その通りです。それを取得する方法はあるのでしょうか？ありがとうございます。
> > 
> > 
> > 
--- 

