# vllmに関する問題

**padeof** *2024年7月28日 日曜日 18:41:08 日本標準時* (0票)

vLLMクラスを使って直接vLLMを実行できる人はいませんか？

この "/kaggle_simulations/agent/srvlib/vllm/_C.cpython-310-x86_64-linux-gnu.so: undefined symbol" エラーを1週間試行錯誤しましたが、解決できませんでした…

vLLMをサーバーとして実行しても、ランダムに起動に失敗することがあります。

ノートブックの提出をデバッグするのは本当に難しいです🤣

---
# 他のユーザーからのコメント

> ## Chris Deotte
> 
> KaggleでvLLMを使用するコード例を以下に示します。vLLMはインストールされていますが、Kaggleで動作させるには、pipでアップグレードし、いくつかのファイルを修正する必要があります。[https://www.kaggle.com/code/cdeotte/infer-34b-with-vllm](https://www.kaggle.com/code/cdeotte/infer-34b-with-vllm)
> 
> 
> 
> > ## padeofトピック作成者
> > 
> > ありがとうございます！投稿を読みました。しかし、この方法は提出時には機能しません。エージェントスクリプトでsysパスを変更する前にtorchモジュールがロードされているようです。そのため、vLLMとtorchのバイナリが一致しません。
> > 
> > 
> > 
--- 

