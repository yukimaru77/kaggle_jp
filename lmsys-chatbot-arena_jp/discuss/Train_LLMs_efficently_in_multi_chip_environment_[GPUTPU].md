# 複数チップ環境（GPU/TPU）でLLMを効率的にトレーニングする

**Simon Veitner** *2024年5月29日 水曜日 16:24:01 GMT+0900 (日本標準時)* (4票)

皆さん、こんにちは！

FSDPとTP技術を使って、複数のGPU/TPUチップでLLMをトレーニングできるカスタマイズ可能なノートブックを共有しました。

このアーキテクチャは、[LLMサイエンス試験の1位ソリューション](https://www.kaggle.com/competitions/kaggle-llm-science-exam/discussion/446422)から着想を得ています。

ノートブックのスコアはあまり良くありませんが、前処理やモデリングなどを調整することで簡単に改善できます。

[ノートブックはこちら](https://www.kaggle.com/code/simonveitner/fsdp-with-scalax)をご覧ください。 

