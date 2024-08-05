# 要約 
このディスカッションでは、コンペ「LLM 20 Questions」におけるキーワードとカテゴリに関する質問が行われています。参加者のsakuraが、keywords.pyファイルから提供されるキーワードのリストについて、オンライン評価にプライベートキーワードが含まれるのか確認しようとしています。

Chris Deotteが回答し、プライベートリーダーボードには異なるキーワードが含まれること、さらにプライベートキーワードリストにはアクセスできないため、最終的なソリューションではkeywords.pyを使わない方が良いと説明しています。彼はまた、現在のパブリックリーダーボードリストが変更される予定であることにも言及しています。

その後、sakuraは自分の理解を確認し、競技全体を通じてキーワードが変更される一方、カテゴリ（「人」「場所」「物」）は安定していると理解したか確認します。Bovard Doerschuk-Tiberiが再確認し、カテゴリに関する情報を提供しました。またMuhammadが、なぜ国に関する質問があるのか、国が第四のカテゴリと見なされるのか尋ねています。

全体として、ディスカッションはキーワードとカテゴリの安定性に関する疑問と情報の交換を中心に進行しています。

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

# Questions about the data

**sakura** *Thu Jun 06 2024 21:12:54 GMT+0900 (日本標準時)* (1 votes)

Hi, I've noticed that keywords.py gives a list of keywords. I'm wondering that whether there will be private keywords in the online evaluation? Will the categories and keywords all come from the given keywords.py through the whole competition?



---

 # Comments from other users

> ## Chris Deotte
> 
> Hi. No, the private LB will have different keywords. Furthermore, we will not have access to the private keyword list. So our final solution should not use the keywords.py file.
> 
> Also the current public LB list will change very soon, explained [here](https://www.kaggle.com/competitions/llm-20-questions/discussion/509035)
> 
> 
> 
> > ## sakuraTopic Author
> > 
> > Thank you! I didn't see [this pose](https://www.kaggle.com/competitions/llm-20-questions/discussion/509035) before. According to my understanding, the categories will be stable, but the keywords will change across the whole competition, and a private word set will be used in the final period. Is that correct?
> > 
> > 
> > 
> > > ## Bovard Doerschuk-Tiberi
> > > 
> > > yes, categories will be person, place or thing
> > > 
> > > 
> > > 
> > > ## Muhammad
> > > 
> > > Then why are the questions asked about the country? As in the starter notebook, the few_shot_examples variable contains questions about the country. Is the country considered as the fourth category? 
> > > 
> > > 
> > > 


---



</div>
<div class="column-right">

# 日本語訳

# データに関する質問
**sakura** *2024年6月6日木曜日 21:12:54 JST* (1票)
こんにちは、keywords.pyがキーワードのリストを提供していることに気づきました。オンライン評価にプライベートキーワードが含まれるのか気になっています。競技全体を通して、カテゴリやキーワードはすべてkeywords.pyから提供されるのでしょうか？

---
 # 他のユーザーからのコメント
> ## Chris Deotte
> 
> こんにちは。いいえ、プライベートリーダーボードには異なるキーワードが含まれます。さらに、プライベートキーワードリストにはアクセスできないため、最終的なソリューションはkeywords.pyファイルを使用しないほうが良いでしょう。
> 
> 現在のパブリックリーダーボードリストはまもなく変更される予定です。詳細は[こちら](https://www.kaggle.com/competitions/llm-20-questions/discussion/509035)で説明されています。

> > ## sakura トピック作成者
> > 
> > ありがとうございます！以前に[この投稿](https://www.kaggle.com/competitions/llm-20-questions/discussion/509035)を見ていませんでした。私の理解によれば、カテゴリは安定しているものの、キーワードは競技全体を通じて変更され、最終的にはプライベートな単語セットが使用されるのですね。その理解で合っていますか？

> > > ## Bovard Doerschuk-Tiberi
> > > 
> > > はい、カテゴリは「人」「場所」「物」となります。

> > > > ## Muhammad
> > > > 
> > > > では、なぜ国に関する質問がされているのでしょうか？スターターノートブックのfew_shot_examples変数には国に関する質問が含まれています。国は第四のカテゴリと見なされますか？


</div>