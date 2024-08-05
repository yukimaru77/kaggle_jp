# 要約 
このディスカッションは、KaggleのLMSYS - Chatbot Arena Human Preference Predictionsコンペティションにおけるデータリーク問題についてです。

コンペティション主催者のSohier Daneは、公開データセットにコンペティションの隠されたテストセットの一部が含まれていたことを認めました。これは、コンペティションの公平性に影響を与える可能性があります。

コミュニティメンバーは、この問題について懸念を表明し、リークされたデータへのアクセスが可能な場合、コンペティションの公平性が損なわれる可能性を指摘しました。

主催者は、ソリューションファイルを更新して影響を受ける行を無視し、すべての提出物を再評価することを約束しました。また、リークされたデータへのリンクを提供し、問題を解決するために努力していることを表明しました。

コミュニティメンバーは、主催者の迅速な対応と透明性を高く評価しました。


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

# Solution file to be updated the week of May 28th

**Sohier Dane** *Tue May 21 2024 01:30:43 GMT+0900 (日本標準時)* (31 votes)

A Kaggle community member informed us that the hidden test set for this competition contains values that have already been published. We were aware of some existing public data, but not that there are actually different versions of the public data using one name. We will update the solution file to ignore the affected rows next week and then rescore all existing submissions. You are welcome to continue to make submissions in the meantime.

Thank you very much to the Kaggler that disclosed this issue.

To everyone else, apologies for the disruption and thank you in advance for your patience. 



---

 # Comments from other users

> ## Psi
> 
> Given the top score, high probability there is another leak…
> 
> 
> 
> > ## Chris Deotte
> > 
> > If it is a leak, this is frustrating. Many teams spent a lot of money and time on compute. 
> > 
> > If it is a leak in the form of released test data, doesn't the host know where they published their test data? Couldn't this have been discovered day one?
> > 
> > 
> > 
> > > ## Psi
> > > 
> > > as you can see in this thread, it already happened once…
> > > 
> > > I hope it is not an explicit data leak, or no leak at all (which seems unlikely though), but rather some clever data exploitation
> > > 
> > > 
> > > 
> > > ## CPMP
> > > 
> > > I miss the days where people had to disclose every external data they used in competition forums.
> > > 
> > > 
> > > 
> > > ## Fae Gaze
> > > 
> > > Hi, I also miss that part. I would appreciate any help on that
> > > 
> > > 
> > > 


---

> ## Paul Mooney
> 
> Following up to note that we updated the solution file and rescored the submissions. The leaderboard page now shows the updated scores. Thanks again to the community members that disclosed this issue!
> 
> 
> 


---

> ## heartkilla
> 
> A link to the data would be appreciated 
> 
> 
> 
> > ## heartkilla
> > 
> > I will clarify. If this data is public and someone has access to it, they can still use it for analysis, even if it’s removed from the test set. 
> > 
> > 
> > 
> > ## dott
> > 
> > It is the 33k LMSYS dataset published on HF [https://huggingface.co/datasets/lmsys/chatbot_arena_conversations](https://huggingface.co/datasets/lmsys/chatbot_arena_conversations) and preprocessed by one of the Kagglers [https://www.kaggle.com/code/abdullahmeda/33k-lmsys-chatbot-arena-conversations](https://www.kaggle.com/code/abdullahmeda/33k-lmsys-chatbot-arena-conversations) into the competition format. We used the latter to detect the leak.
> > 
> > 
> > 
> > > ## heartkilla
> > > 
> > > That's the spirit. Thanks.
> > > 
> > > 
> > > 


---

> ## Fae Gaze
> 
> Thank you for the update and for handling this issue. Looking forward to the revised scores next week!
> 
> 
> 


---

> ## Wasiu Olaitan Garuba 
> 
> That's a lovely idea 
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# 5月28日週に更新される予定のソリューションファイル
**Sohier Dane** *2024年5月21日 火曜日 01:30:43 GMT+0900 (日本標準時)* (31票)
Kaggle コミュニティのメンバーから、このコンペティションの隠されたテストセットに、すでに公開されている値が含まれていることが報告されました。私たちは、いくつかの公開データの存在は認識していましたが、実際には同じ名前で異なるバージョンの公開データが存在することは知りませんでした。来週、ソリューションファイルを更新して影響を受ける行を無視し、その後、既存のすべての提出物を再評価します。それまでの間も、提出を続けることができます。
この問題を明らかにしてくれたKagglerに心から感謝します。
他の皆さんには、混乱をおかけして申し訳ありません。ご理解のほどよろしくお願いいたします。
---
# 他のユーザーからのコメント
> ## Psi
> 
> トップスコアを見る限り、別のリークがある可能性が高い…
> 
> 
> 
> > ## Chris Deotte
> > 
> > もしリークなら、これは非常に不満です。多くのチームが、計算に多額の費用と時間を費やしました。
> > 
> > もしリークが公開されたテストデータの形であれば、ホストは自分のテストデータをどこで公開したかを知っているはずです。これは、初日から発見できたはずです。
> > 
> > 
> > 
> > > ## Psi
> > > 
> > > このスレッドでわかるように、すでに一度発生しています…
> > > 
> > > 明確なデータリークではなく、リークが全くない（ただし、可能性は低い）か、あるいは巧妙なデータの悪用であることを願っています。
> > > 
> > > 
> > > 
> > > ## CPMP
> > > 
> > > 人々がコンペティションフォーラムで使用するすべての外部データを公開しなければならなかった時代が懐かしいです。
> > > 
> > > 
> > > 
> > > ## Fae Gaze
> > > 
> > > はい、私もその部分に懐かしさを感じます。その点について、何か助けがあれば幸いです。
> > > 
> > > 
> > > 
---
> ## Paul Mooney
> 
> ソリューションファイルを更新し、提出物を再評価したことをお知らせします。リーダーボードページには、更新されたスコアが表示されています。この問題を明らかにしてくれたコミュニティメンバーに改めて感謝します！
> 
> 
> 
---
> ## heartkilla
> 
> データへのリンクがあれば幸いです。
> 
> 
> 
> > ## heartkilla
> > 
> > 明確に説明します。このデータが公開されており、誰かがアクセスできる場合、テストセットから削除されていても、分析に利用できます。
> > 
> > 
> > 
> > ## dott
> > 
> > これは、HF [https://huggingface.co/datasets/lmsys/chatbot_arena_conversations](https://huggingface.co/datasets/lmsys/chatbot_arena_conversations) に公開されている33k LMSYS データセットであり、Kaggler の一人がコンペティション形式に前処理しました [https://www.kaggle.com/code/abdullahmeda/33k-lmsys-chatbot-arena-conversations](https://www.kaggle.com/code/abdullahmeda/33k-lmsys-chatbot-arena-conversations)。私たちは後者を使用してリークを検出しました。
> > 
> > 
> > 
> > > ## heartkilla
> > > 
> > > 素晴らしいですね。ありがとうございます。
> > > 
> > > 
> > > 
---
> ## Fae Gaze
> 
> 更新とこの問題の処理について感謝します。来週の改訂されたスコアを楽しみにしています！
> 
> 
> 
---
> ## Wasiu Olaitan Garuba 
> 
> 素晴らしいアイデアですね。
> 
> 
> 
---



</div>