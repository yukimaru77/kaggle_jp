# 要約 
このディスカッションは、KaggleのLMSYS - Chatbot Arena Human Preference Predictionsコンペティションにおける時間制限に関するものです。

投稿者は、コンペティションのルールで9時間という時間制限が設定されているにもかかわらず、それがテストセット全体の推論時間なのか、それともパブリックリーダーボードのデータに対する時間制限なのかを疑問視しています。

他のユーザーからのコメントでは、時間制限はパブリックリーダーボード用であり、プライベートリーダーボードのスコアは計算されているものの表示されていないことが明らかになりました。

また、時間制限が9時間では推論に時間がかかりすぎるという意見も出ており、時間制限の延長や効率的な推論技術の利用などの解決策が議論されています。

最終的に、投稿者は、時間制限はパブリックリーダーボード用であり、プライベートリーダーボードのスコアは計算されていることを確認し、時間制限の延長は難しいことを認識しました。


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

# Time constraint for private leaderboard [Solved]

**raconion** *Fri Jul 05 2024 11:15:47 GMT+0900 (日本標準時)* (2 votes)

There are roughly 25,000 rows in the test set. Among them, 26% are used for public lb while the rest 74% are used for private lb. 

Since in Overview section, the time constraint is 9 hrs, does this mean that our notebook has to finish the inference for 74%*25,000 =18,500 rows in the test set? Or this time constraint is for public lb and will be scaled according to the number of rows when it comes to private lb?

[@addisonhoward](https://www.kaggle.com/addisonhoward) [@mylesoneill](https://www.kaggle.com/mylesoneill) Would really appreciate if you can clarify this!

Update:

Our notebook will be run for all 25k rows but only 26% shown on public lb. Thanks for the comment [@lizhecheng](https://www.kaggle.com/lizhecheng) 

This comment also clarify this issue: [link](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/516995#2904512)



---

 # Comments from other users

> ## Enter your display name
> 
> As long as you can see your public score, your private score has also been calculated, but you just can't see it for now. Thus you don't need to worry about that.
> 
> 
> 
> > ## jiangli59
> > 
> > I vote for that. Is it possible to extend the time budget over 9 hrs? Or, Do we have other opinions to solve that? My code is extremely overwhelmed for the inference budget.  
> > 
> > 
> > 
> > > ## raconionTopic Author
> > > 
> > > I don't think the time constraint can be extended unless the competition host decides so. There are way arounds though such as all kinds of efficient inference techniques.
> > > 
> > > 
> > > 


---



</div>
<div class="column-right">

# 日本語訳

# プライベートリーダーボードの時間制限について [解決済み]

**raconion** *2024年7月5日 金曜日 11:15:47 日本標準時* (2票)

テストセットには約25,000行ありますが、そのうち26%がパブリックリーダーボードに使用され、残りの74%がプライベートリーダーボードに使用されます。

概要セクションでは、時間制限が9時間とされていますが、これはテストセットの74% * 25,000 = 18,500行の推論をノートブックが完了する必要があるという意味でしょうか？それとも、この時間制限はパブリックリーダーボード用であり、プライベートリーダーボードでは行数に応じてスケールされるのでしょうか？

[@addisonhoward](https://www.kaggle.com/addisonhoward) [@mylesoneill](https://www.kaggle.com/mylesoneill) ぜひご説明いただけたら幸いです！

**更新:**

私たちのノートブックは25,000行すべてに対して実行されますが、パブリックリーダーボードには26%のみが表示されます。[@lizhecheng](https://www.kaggle.com/lizhecheng) のコメントありがとうございます。

このコメントもこの問題を明確にしています: [リンク](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/516995#2904512)

---
# 他のユーザーからのコメント

> ## 表示名を入力してください
> 
> パブリックスコアが表示される限り、プライベートスコアも計算されていますが、今は表示されません。そのため、心配する必要はありません。
> 
> 
> 
> > ## jiangli59
> > 
> > それに賛成です。時間予算を9時間以上に延長することは可能でしょうか？あるいは、他に解決策があるのでしょうか？私のコードは推論予算に対して非常に負荷がかかっています。
> > 
> > 
> > 
> > > ## raconionトピック作成者
> > > 
> > > コンペティション主催者が決定しない限り、時間制限を延長することはできないと思います。ただし、効率的な推論技術など、回避策はあります。
> > > 
> > > 
> > > 
---



</div>