# 要約 
コンペティションに参加しているユーザーがKaggleノートブックからファイルを提出しようとしたところ、最大20GBのファイルサイズ制限に引っかかり、エラーが発生したという内容のディスカッションです。ユーザーは、20GBを超えるファイルを提出する方法について質問しました。

他のユーザーからは、ファイルサイズには制限があり、8GBを超えるファイルは提出時に実行時間が足りなくなる可能性があるというアドバイスや、小さいモデルを使用する提案がありました。トピック作成者は、2つのモデルを量子化することで20GBに収めることができたと報告し、同様の問題に直面している他のユーザーと情報を共有しました。

また、これに関連してチームメイトを探している他の参加者との交流もあり、上位のチームが公開リーダーボードのキーワードをモデルに使用しているかどうかの質問が出たり、モデルのサイズ制限に関する期待についても言及されました。全体的に、このディスカッションはKaggleのファイルサイズ制限とそれに対する回避策についての情報交換が中心になっています。

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

# [SOLVED] Submisson error due to file size when using kaggle CLI in kaggle notebook

**c-number** *Fri Jun 28 2024 11:28:47 GMT+0900 (日本標準時)* (0 votes)

Hello,

I am working on the competition based on this [notebook](https://www.kaggle.com/code/robikscube/intro-to-rigging-for-llm-20-questions-llama3), but I get the following error when trying to submit from the notebook.

400 - Bad Request - Submission not allowed:  Your file exceeds the maximum size of 20 GB.

Does anyone know how to submit files larger than 20GB? or is the submission file limited to that size for this competition? (I couldn' t find such a statement though.)

Thank you in advance.



---

 # Comments from other users

> ## OminousDude
> 
> The file size is limited however files larger than ~ 8 GB won't have time to run on the Tesla T4s for submission. Try using a smaller model (guessing you used Gemma 2 🫣)
> 
> 
> 
> > ## c-numberTopic Author
> > 
> > Thanks, I was trying to upload several models (Gemma 2 is not one of them :) ) and run all of them for a single question.
> > 
> > Maybe I should upload the quantized weights directly.
> > 
> > 
> > 


---

> ## Sumo
> 
> [@cnumber](https://www.kaggle.com/cnumber) I'm a bit late to the party, but I saw you marked this thread as solved. How did you get around it? I'm running into the same issue
> 
> 
> 
> > ## c-numberTopic Author
> > 
> > Well, it's not actually solved, but I managed to fit 2 models in 20GB by quantizing them.
> > 
> > Hope this helps!
> > 
> > 
> > 
> > > ## Sumo
> > > 
> > > ah that's a shame. Thank you anyway!
> > > 
> > > offtopic, but we're looking for a teammate for this comp (and future competitions!), in case you're interested we'll be very happy to have you in our team :) 
> > > 
> > > 
> > > 
> > > ## OminousDude
> > > 
> > > Off topic but I am asking all of the top places about if they use the public lb keywords for their model. Does your team use them?
> > > 
> > > 
> > > 


---

> ## c-numberTopic Author
> 
> I'm having some trouble trying to submit 2 7B~8B models, so I really hope Kaggle would relax the submission file size restriction.
> 
> 
> 
> > ## OminousDude
> > 
> > I see the problem however is that on the Kaggle GPUs such a model would likely not have enough time (60 sec) to run
> > 
> > 
> > 
> > > ## c-numberTopic Author
> > > 
> > > Thanks for you advice, but currently I have no problems with running a single 7~8B model in the given computation time, and the log tells me that I might have time for another model.
> > > 
> > > 
> > > 


---



</div>
<div class="column-right">

# 日本語訳

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


</div>