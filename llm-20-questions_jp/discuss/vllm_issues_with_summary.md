# 要約 
このディスカッションは、Kaggleの「LLM 20 Questions」コンペティションにおけるvLLMライブラリに関する問題についてです。

投稿者は、vLLMクラスを使って直接vLLMを実行しようとしましたが、`"/kaggle_simulations/agent/srvlib/vllm/_C.cpython-310-x86_64-linux-gnu.so: undefined symbol"`というエラーが発生し、解決できないでいます。また、vLLMをサーバーとして実行しても、ランダムに起動に失敗することがあるとのことです。

他のユーザーからのコメントでは、Chris Deotte氏がKaggleでvLLMを使用するコード例を共有しています。しかし、投稿者はこの方法が提出時には機能しないと指摘し、エージェントスクリプトでsysパスを変更する前にtorchモジュールがロードされているため、vLLMとtorchのバイナリが一致しないことが原因だと考えています。

このディスカッションは、KaggleのコンペティションでvLLMを使用する際に発生する可能性のある問題と、その解決策について議論しています。特に、vLLMとtorchのバイナリが一致しない問題が、提出時にvLLMを使用する際に大きな課題となっていることがわかります。


---
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

