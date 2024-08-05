# 要約 
以下は、コンペのディスカッションに関する要約です。

---

**タイトル:** Llama 3.1 ハック - Kaggle 環境での動作確認

**発信者:** Matthew S Farmer (2024年8月2日)

要約:

Llama 3.1の最新リリースについて、Kaggleの「20の質問」コンペティションでの動作に関する問題が取り上げられています。特に、RoPEスケーリングに関するエラーが発生し、オンラインでは「transformersを更新しろ」との情報しか得られなかったとのこと。しかし、著者はtransformersを更新しなくても動作させるワークアラウンドを提供しました。

具体的な実装手順として、以下の内容が説明されています：
1. transformersの更新を解除する。
2. 使用するLlama 3.1モデルをインポートする。
3. config.jsonのパスを確認し、指定のコードで編集する。
4. 提出用のスクリプトを準備する。
5. モデルとスクリプトを正常に読み込む。
6. 設定ファイルを圧縮し、提出する。

最後に、他の参加者からの感謝のコメントが寄せられており、コンペティションの成功を祈る言葉で締めくくられています。

--- 

この要約は、ディスカッションの主旨や重要なポイントを簡潔にまとめたものです。

---


<style>
.column-left{
  float: left;
  width: 47.5%;
  text-align: left;
}
.column-right{
  float: right;
  width: 47.5%;
  text-align: left;
}
.column-one{
  float: left;
  width: 100%;
  text-align: left;
}
</style>


<div class="column-left">

# original

# Llama 3.1 Hack - Confirmed to Work in Kaggle Environment (Notebooks and Competition)

**Matthew S Farmer** *Fri Aug 02 2024 04:34:42 GMT+0900 (日本標準時)* (21 votes)

# Llama 3.1

So, you saw the latest release of Llama 3.1 and thought to yourself "I bet this would be good in the LLM 20 Questions competition". Then you fired up a notebook, imported the model, attempted to load it, then were faced with an error about RoPE scaling… You jump on the discussion board and don't find any help. You look online and all the posts say "update transformers". You do that and the notebook works, but then you get that pesky validation error. What are we to do! As any tinkerers or hackers know, there's always a workaround somewhere…

## We have a workaround!

I have validated that this works in the notebook and game environment without updating transformers. 

```
import json
with open("YOUR_LOCAL_MODEL_PATH/config.json", "r") as file:
    config = json.load(file)
config["rope_scaling"] = {"factor":8.0,"type":"dynamic"}
with open("YOUR_LOCAL_MODEL_PATH/config.json", "w") as file:
    json.dump(config, file)

```

## Implementation

Remove any updates to transformers that you were trying.
Import your desired llama 3.1 model to your working folder
Validate the path to config.json in that folder and replace the all caps path in the code above.
Add the code in a code block that precedes your submission .py script and tarball submission. 
Load the model and script as you normally would. 
Validate text generation in the notebook if desired.
Prepare your script for submission, ensuring that the updated config file is zipped with the model. 
Enjoy the green checkmark after validation. 

I hope this raises the bar for everyone in this competition as we approach the final evaluation. May the best agents win!

## TL;DR

Modify config.json to a dictionary that the current version of Transformers expects (2 fields). 

Cheers! Happy Kaggling 

If you have questions about RoPE scaling, check out [the docs! ](https://huggingface.co/docs/text-generation-inference/en/basic_tutorials/preparing_model)



---

 # Comments from other users

> ## VolodymyrBilyachat
> 
> Legend! thank you for this simple hack :)
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# Llama 3.1 ハック - Kaggle 環境（ノートブックおよびコンペティション）で動作確認済み
**Matthew S Farmer** *2024年8月2日金曜日 04:34:42 GMT+0900（日本標準時）* (21票)

# Llama 3.1
最新のLlama 3.1のリリースを見て、「これがLLM 20 Questionsコンペティションで使えそう」と思ったことでしょう。ノートブックを立ち上げてモデルをインポートし、読み込もうとすると、RoPEスケーリングに関するエラーが発生しました…。ディスカッションボードにアクセスしても助けを見つけられず、オンラインでは「transformersを更新しろ」としか書いていません。それを実行するとノートブックは動くようになりますが、今度は厄介なバリデーションエラーに直面します！どうすればいいのでしょう？いじくり回すことが好きな人なら、どこかにワークアラウンドがあることを知っています…

## 私たちにはワークアラウンドがあります！
私は、transformersを更新することなく、ノートブックおよびゲーム環境で動作することを確認しました。 
```
import json
with open("YOUR_LOCAL_MODEL_PATH/config.json", "r") as file:
    config = json.load(file)
config["rope_scaling"] = {"factor":8.0,"type":"dynamic"}
with open("YOUR_LOCAL_MODEL_PATH/config.json", "w") as file:
    json.dump(config, file)
```
## 実装手順
1. 試していたtransformersの更新をすべて取り消します。
2. 使用したいLlama 3.1モデルを作業フォルダにインポートします。
3. そのフォルダ内のconfig.jsonのパスを確認し、上記のコード内の全大文字のパスに置き換えます。
4. 提出用の.pyスクリプトおよびtarball提出の前に、コードブロック内にこのコードを追加します。
5. 通常通りモデルとスクリプトを読み込みます。
6. 必要に応じてノートブック内でテキスト生成を確認します。
7. 更新された設定ファイルをモデルと一緒に圧縮して提出用に準備します。
8. バリデーション後の緑のチェックマークを楽しんでください。

最終評価が迫る中、皆さんのコンペティションのレベルが上がることを願っています。最良のエージェントが勝ちますように！

## 要約
config.jsonを現在のtransformersバージョンが期待する辞書（2つのフィールド）に変更します。 
では、ハッピーカグリングを！

RoPEスケーリングについて質問がある場合は、[ドキュメントをチェックしてみてください！ ](https://huggingface.co/docs/text-generation-inference/en/basic_tutorials/preparing_model)

---

# 他のユーザーからのコメント
> ## VolodymyrBilyachat
> 
> 伝説ですね！このシンプルなハックに感謝します :)


</div>