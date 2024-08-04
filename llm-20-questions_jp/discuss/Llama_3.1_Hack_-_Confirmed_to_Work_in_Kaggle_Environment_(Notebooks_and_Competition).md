# Llama 3.1 ハック - Kaggle 環境（ノートブックとコンペティション）で動作確認済み
**Matthew S Farmer** *2024年8月2日 金曜日 04:34:42 GMT+0900 (日本標準時)* (17票)
# Llama 3.1
Llama 3.1 の最新リリースを見て、「これは LLM 20 Questions コンペティションで役に立つだろう」と思った人もいるでしょう。そして、ノートブックを起動してモデルをインポートし、ロードしようとしたら、RoPE スケーリングに関するエラーに遭遇したかもしれません… ディスカッションボードを見ても解決策が見つかりません。オンラインで検索しても、すべての投稿は「transformers をアップデートしてください」と書いてあります。アップデートしてもノートブックは動作しますが、厄介なバリデーションエラーが発生します。どうすればいいのでしょうか！ どんな工作好きやハッカーも知っているように、どこかに回避策があるはずです…
## 回避策があります！
この回避策がノートブックとゲーム環境で動作することを確認しました。transformers をアップデートする必要はありません。
```
import json
with open("YOUR_LOCAL_MODEL_PATH/config.json", "r") as file:
    config = json.load(file)
config["rope_scaling"] = {"factor":8.0,"type":"dynamic"}
with open("YOUR_LOCAL_MODEL_PATH/config.json", "w") as file:
    json.dump(config, file)
```
## 実装
transformers のアップデートをすべて削除してください。
お好みの llama 3.1 モデルを作業フォルダにインポートします。
フォルダ内の config.json へのパスを確認し、上記のコード内のすべて大文字のパスを置き換えます。
上記のコードを、提出する .py スクリプトと tarball 提出の前にあるコードブロックに追加します。
通常どおりモデルとスクリプトをロードします。
必要に応じて、ノートブックでテキスト生成を検証します。
提出用のスクリプトを準備し、更新された config ファイルがモデルと一緒に圧縮されていることを確認します。
バリデーション後に緑色のチェックマークが表示されることを確認してください。
このハックが、最終評価が近づくにつれて、このコンペティションの参加者全員のレベルを引き上げることを願っています。最高のエージェントが勝利することを祈っています！
## TL;DR
config.json を、現在のバージョンの Transformers が期待する辞書（2 つのフィールド）に変更します。
乾杯！ 楽しい Kaggling を！
RoPE スケーリングについて質問がある場合は、[ドキュメントをご覧ください！](https://huggingface.co/docs/text-generation-inference/en/basic_tutorials/preparing_model)
---
 # 他のユーザーからのコメント
> ## VolodymyrBilyachat
> 
> 伝説！ この簡単なハックをありがとう :)
> 
> 
> 
---

