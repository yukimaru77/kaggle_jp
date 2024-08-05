# vllmの問題
**padeof** *2024年7月28日 18:41:08 (日本標準時)* (0票)
誰か、LLMクラスを使って直接vllmを実行できる人はいますか？
"/kaggle_simulations/agent/srvlib/vllm/_C.cpython-310-x86_64-linux-gnu.so: undefined symbol"というエラーを解決しようと1週間試みましたが、うまくいきませんでした…
vllmをサーバーとして実行すると、ランダムに起動に失敗することもあります。
ノートブックの提出でデバッグするのが非常に難しいです🤣
---
# 他のユーザーからのコメント
> ## Chris Deotte
> 
> ここにKaggleでvLLMを使ったコード例があります。vLLMはインストールされていますが、Kaggleで動作させるためにはpipのアップグレードやいくつかのファイルを変更する必要があります。[https://www.kaggle.com/code/cdeotte/infer-34b-with-vllm](https://www.kaggle.com/code/cdeotte/infer-34b-with-vllm)
> 
> 
> > ## padeof トピック作成者
> > 
> > ありがとうございます！あなたの投稿を読みました。しかし、この方法は提出時には機能しないようです。どうやら、エージェントスクリプト内でsysパスに変更を加える前にtorchモジュールが読み込まれてしまっているようです。そのため、vllmとtorchのバイナリが一致していません。 
> > 
> > 
> >
