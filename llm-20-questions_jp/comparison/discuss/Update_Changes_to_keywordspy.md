# 要約 
以下は、Kaggleのコンペ「LLM 20 Questions」に関するディスカッションの要約です。

2024年6月18日に、コンペティションのキーワード設定を管理しているBovard Doerschuk-Tiberiが、`keywords.py`ファイルが更新されたことを報告しました。変更の内容には、カテゴリが「場所」と「物」に分けられ、「人」カテゴリが削除されたことが含まれています。この変更に伴い、競技の健全性を保つことに注力すると述べています。

複数の参加者からは、更新された`keywords.py`ファイルについての質問が寄せられ、特に更新が既存のデータタブとどのように異なるかに注目が集まりました。また、人に関するカテゴリが全体のコンペティションから除外されるのかとの疑問が提示され、その点についてBovardが確認した結果、全体から削除されることが明言されました。

参加者のloh-maaは、新しいキーワードセットが以前のものより難解であると述べ、抽象的かつ特異な用語が増えているため、成功率が低くなる懸念を示しました。また、エージェントが正しい単語を推測するのが難しい理由として、同義語の不足や特異なキーワードの存在を挙げました。

さらに、Chernov Andreyは、質問者LLMが最終的なキーワードにアクセスできるのか、また最終評価期間中に辞書がどのように利用可能になるかを尋ねました。この質問は、コンペ参加者間で異なる意見があったため確認されました。

全体として、競技中の変更や新たなキーワードセットがもたらす影響についての懸念と疑問が多く議論されています。

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

# Update: Changes to keywords.py

**Bovard Doerschuk-Tiberi** *Tue Jun 18 2024 06:06:24 GMT+0900 (日本標準時)* (11 votes)

keywords.py is now updated in kaggle-environments 1.14.14 which is rolling out now.

For this change we now have two categories: places and things. The people category we discussed has been dropped.

We continue to monitor the health of this competition and will take action to ensure robust competition.



---

 # Comments from other users

> ## tiod0611
> 
> Hello,
> 
> After reading this discussion, I have a question. The contents of the keywords.py file available in the Data tab of this competition differ from the updated keywords.py file available on Kaggle's GitHub([https://github.com/Kaggle/kaggle-environments/blob/master/kaggle_environments/envs/llm_20_questions/keywords.py)](https://github.com/Kaggle/kaggle-environments/blob/master/kaggle_environments/envs/llm_20_questions/keywords.py)).
> 
> When I print(kaggle_environments.envs.llm_20_questions.keywords.KEYWORDS_JSON) in my notebook, it matches the file in the Data tab.
> 
> So, where is the update to the keywords.py file that you mentioned being applied?
> 
> 
> 


---

> ## RS Turley
> 
> Thanks for the update. Is the people category dropped from this update only, or is the category also dropped from the full competition, including the unpublished keywords that will be used after August 13th?
> 
> 
> 
> > ## Kha Vo
> > 
> > That is my question as well
> > 
> > 
> > 
> > ## Bovard Doerschuk-Tiberi
> > 
> > people category is dropped from the full competition. 
> > 
> > 
> > 


---

> ## loh-maa
> 
> It seems the updated set of keywords is way more difficult than the previous one. We're going to see even lower success rate. I recently updated my agents, 44 games in total and not a single guess on any side. I don't mean to complain or suggest any changes, just a few remarks:
> 
> Contrary to some earlier hints, there are abstract/conceptual terms -- "analogy", "interstate", "hearing aid", "vegetation". These are not specific objects and I think more difficult to find out.
> 
> There are keywords which have many synonyms, but alts are not provided, so even if an agent comes close to the concept of "ointment", it could still need many turns to find the right word among words that are difficult to tell apart: lotion, cream, balsam, balm, gel, oil.
> 
> There are keywords that are so specific/rare that I don't think we could expect them to be ever solved if they were not listed, e.g. "pot holder", "sippy cup", "elliptical trainers", "graphic novel". Some of them a normal person would have never used or heard of. Can small LLMs handle them? I bet not in 20 questions, but who knows..
> 
> So the challenge is serious. Perhaps some players would like to make a real effort, however it's a little bit discouraging to hear that the rules and/or types of keywords could change again, possibly rendering the effort a waste of time.
> 
> 
> 
> > ## Kha Vo
> > 
> > Exactly my concern. I think the Kaggle team need to manually look into the keywords and exclude those strange 2-word words. “Bike path” is a composition word and can’t be predicted by an LLM in 20 questions. Even human, how can a human expect to predict the word “elliptical trainers’?
> > 
> > 
> > 


---

> ## Chernov Andrey
> 
> Hello! Thanks for conducting the competition!
> 
> I would like to clarify whether will the questioner llm have an access to the FINAL keywords during the runtime or not? Can we do some calculations to find optimal question in runtime relying on the keywords.py file? Or will the final dictionary be complitely unavailable in runtime during the final evaluation?
> 
> Sorry, if you already answered it, but I found the different opinions in the discussion thread
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# 更新: keywords.pyの変更について
**Bovard Doerschuk-Tiberi** *2024年6月18日（火）06:06:24 GMT+0900 (日本標準時)* (11票)
kaggle-environments 1.14.14でkeywords.pyが更新され、現在展開中です。
この変更により、カテゴリが「場所」と「物」に分かれました。話し合っていた「人」に関するカテゴリは削除されました。
このコンペティションの健康状態について引き続き監視し、しっかりとした競技が行われるよう調整します。
---
# 他のユーザーからのコメント
> ## tiod0611
> 
> こんにちは、
> 
> このディスカッションを読んで、1つ質問があります。このコンペティションのデータタブにあるkeywords.pyファイルの内容が、KaggleのGitHubにある更新されたkeywords.pyファイル（[https://github.com/Kaggle/kaggle-environments/blob/master/kaggle_environments/envs/llm_20_questions/keywords.py](https://github.com/Kaggle/kaggle-environments/blob/master/kaggle_environments/envs/llm_20_questions/keywords.py)）と異なっています。
> 
> ノートブックでprint(kaggle_environments.envs.llm_20_questions.keywords.KEYWORDS_JSON)を実行すると、データタブのファイルと一致します。
> 
> では、どこで言及されていたkeywords.pyファイルの更新が行われているのでしょうか？
> 
> ---
> ## RS Turley
> 
> 更新をありがとう。この人に関するカテゴリは今回の更新だけ削除されたのか、それとも8月13日以降に使用される未公開のキーワードを含む全体のコンペティションからも削除されるのかが気になります。
> 
> > ## Kha Vo
> > 
> > 私も同じ質問です。
> > 
> > 
> > 
> > ## Bovard Doerschuk-Tiberi
> > 
> > 人に関するカテゴリは全体のコンペティションから削除されました。
> > 
> > 
> > 
---
> ## loh-maa
> 
> 新しいキーワードのセットは以前のものよりもずっと難しいようです。成功率もさらに低くなるでしょう。最近、エージェントを44ゲーム更新しましたが、どちらの側も一度も推測できませんでした。不満を言ったり変更を提案したりするつもりはありませんが、いくつかの見解を述べさせてください。
> 
> 一部の早い段階のヒントとは逆に、抽象的・概念的な用語が含まれています。「アナロジー」、「州間」、「補聴器」、「植生」などです。これらは特定の物体ではなく、見つけるのが難しいと思います。
> 
> 多くの同義語を持つキーワードもあり、代替語は提供されていないので、エージェントが「軟膏」という概念に近づいても、同じようなものから正しい単語を見つけるのに多くのターンが必要になるかもしれません: ローション、クリーム、バルサム、バーム、ジェル、オイルなどです。
> 
> それから、あまりにも特異で珍しいキーワードもあり、それらがリストされていなければ解決されることはないだろうと思います。「鍋つかみ」、「スippyカップ」、「エリプティカルトレーナー」、「グラフィックノベル」などです。普通の人はそれらを使ったり聞いたりすることはないでしょう。小さなLLMはそれらを扱えるでしょうか？20の質問では無理だと思いますが、誰が知っていますか…
> 
> 挑戦は大変です。おそらく、一部のプレイヤーは本気で取り組みたいと思うでしょうが、ルールやキーワードの種類が再度変更される可能性があると聞くと、努力が無駄になるのではと少し discouragingです。
> 
> > ## Kha Vo
> > 
> > まさに私の懸念です。Kaggleチームがキーワードを手動で確認し、奇妙な2語のキーワードを除外する必要があると思います。「バイクパス」は合成語であり、20の質問でLLMが予測することはできません。人間でも、「エリプティカルトレーナー」という言葉を推測するのは難しいでしょう。
> 
> > 
> > 
---
> ## Chernov Andrey
> 
> こんにちは！コンペティションを開催してくれてありがとう！
> 
> 質問者LLMは実行時に最終的なキーワードにアクセスできるのでしょうか？それとも、keywords.pyファイルに基づいて最適な質問を計算することはできないのでしょうか？最終評価中に最終的な辞書は完全に利用できなくなるのでしょうか？
> 
> すでに回答されている場合は申し訳ありませんが、ディスカッションスレッドには異なる意見があったので確認させてください。


</div>