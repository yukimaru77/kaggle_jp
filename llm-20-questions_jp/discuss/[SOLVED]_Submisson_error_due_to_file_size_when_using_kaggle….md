# [解決済み] KaggleノートブックでKaggle CLIを使用する際のファイルサイズによる提出エラー
**c-number** *2024年6月28日 金曜日 11:28:47 (日本標準時)* (0票)
こんにちは、
この[ノートブック](https://www.kaggle.com/code/robikscube/intro-to-rigging-for-llm-20-questions-llama3)を基にコンペティションに取り組んでいるのですが、ノートブックから提出しようとすると以下のエラーが出ます。
400 - 不正なリクエスト - 提出不可: ファイルサイズが最大20GBを超えています。
20GB以上のファイルを提出する方法をご存知の方はいらっしゃいますか？また、このコンペティションの提出ファイルはそのサイズに制限されているのでしょうか？（そのような記載は見当たりませんでした。）
事前にありがとうございます。
---
 # 他のユーザーからのコメント
> ## OminousDude
>
> ファイルサイズには制限がありますが、〜8GBを超えるファイルは提出時にTesla T4で実行する時間が足りなくなることがあります。小さいモデルを使用してみてください（恐らくGemma 2を使用したのではないかと推測しています🫣）。
>
> > ## c-numberトピック作成者
> > 
> > ありがとうございます。いくつかのモデルをアップロードしようとしていて（Gemma 2は使用していません😅）、それらを単一の質問に対して実行しようとしていました。
> > 
> > 量子化された重みを直接アップロードすべきかもしれません。
> > 
> ---
> 
> ## Sumo
> 
> [@cnumber](https://www.kaggle.com/cnumber) 遅れましたが、このスレッドを解決済みにマークしているのを見ました。どのようにして回避しましたか？私も同じ問題に直面しています。
> 
> > ## c-numberトピック作成者
> > 
> > 実際には解決はしていませんが、量子化することで2つのモデルを20GBに収めることができました。
> > 
> > これが役に立つことを願っています！
> > 
> > > ## Sumo
> > > > 残念ですが、ありがとうございます！
> > > > 他の話ですが、私たちはこのコンペ（および今後のコンペ）でチームメイトを探しています。もし興味があれば、ぜひあなたをチームに迎えたいです 😊
> > > > 
> > > > > ## OminousDude
> > > > > トピックはそれますが、上位にいる方々に質問しているのですが、公開リーダーボードのキーワードをモデルに使用していますか？あなたのチームはそれを使っていますか？
> > > > > 
---
> ## c-numberトピック作成者
> 
> 2つの7B〜8Bモデルを提出しようとして苦労しています。Kaggleが提出ファイルのサイズ制限を緩和してくれることを期待しています。
> 
> > ## OminousDude
> > 
> > 問題は、KaggleのGPU上では、そのようなモデルが実行する時間（60秒）が不足する可能性があることです。
> > 
> > > ## c-numberトピック作成者
> > > 
> > > アドバイスありがとうございますが、現在のところ1つの7B〜8Bモデルを指定の計算時間内で実行するのには問題がなく、ログによるともう1つのモデルにも時間があるかもしれません。
> > > 
> > > 
> > > 
