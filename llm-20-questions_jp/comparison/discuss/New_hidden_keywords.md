# 要約 
このディスカッションでは、Kaggleの「LLM 20 Questions」コンペティションにおける隠れたキーワードセットについての情報が交換されています。

主催者のBovard Doerschuk-Tiberiは、隠れたテストセットには500の場所、500の物、および1000の新しい物が含まれており、数週間内に完全なリストを公開する予定であると述べています。また、リーダーボードやエージェントを監視して競技が堅牢であることを確認する意向を示しています。

ユーザーからの質問も多く、新しいキーワードがどのように選ばれるのかや、最終的な単語セットがkeywords.pyファイルに含まれるのかどうかについての疑問が上がっています。特に、私たちの手元にあるデータが最終テストセットにも使われるかどうかが議論されています。一部のユーザーは、キーワードが異なるグループからランダムに選ばれているのか確認したいと考えています。

また、エージェントの設計に影響を与える情報が求められており、最終的な単語セットが追加されるときにどのようにアクセスするかが重要なポイントとなっています。最終キーワードはkeywords.pyには含まれないとBovardは明言していますが、現在のキーワードと同じソースから来ることは確認されています。

質問者の中には、特定の言葉（例：エッフェル塔やピラミッドなど）が場所として考慮されるか、人物がカテゴリーとして追加される可能性について尋ねる声もあり、コンペティションに対する参加者の関心と疑問が高まっている様子が見受けられます。

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

# New hidden keywords

**Bovard Doerschuk-Tiberi** *Thu Jun 27 2024 09:37:42 GMT+0900 (日本標準時)* (10 votes)

As of now, some of the keywords are pulled from a hidden test set. In this set there are 500 location (from keywords.py), 500 things (from keywords.py), and 1000 new things (the hidden set).

We will reveal the full list of these hidden keywords in a few weeks (and possibly add more). That said we hope to minimize changes to the keyword set and keep these as representative as possible of the final dataset.

We will continue to monitor the leaderboard and agents to make sure we have a robust competition. 

Good luck and happy Kaggling!



---

 # Comments from other users

> ## Sumo
> 
> [@bovard](https://www.kaggle.com/bovard) Sorry if this is already answered somewhere, I've checked all other threads and I'm still confused. So I figured asking this here for me + other people reading this in the future:
> 
> Can you confirm to us which of this is the case for this competition?
> 
> - public LB is from keywords.py + a hidden set of keywords. Private LB is from this same set of hidden keywords
> 
> - public LB is from keywords.py + a hidden set of keywords. Private LB is from a totally different of hidden keywords
> 
> - other?
> 
> Thank you
> 
> 
> 
> > ## Naive Experimentalist
> > 
> > i would bet for the 2nd option
> > 
> > 
> > 
> > ## Bovard Doerschuk-Tiberi
> > 
> > The private LB is from the same set of hidden keywords. Though none of them will be re-used for the final evaluation
> > 
> > 
> > 


---

> ## DJ Sterling
> 
> We've removed the large majority of location keywords due to typos, obscurity, and to help address existing stale agents which were hardcoded for those targets.  We will consider adding new entries to the place category soon as well.
> 
> 
> 


---

> ## Max Brown
> 
> If you've already added these 'hidden set' keywords to the set of keywords that are currently being used during matchups, then what stops us from gleaning them by looking at/scraping the episode replays? Thanks!
> 
> edit: also, the keywords.py file in the "Data" section of this competition only has categories for countries, cities, and landmarks. Where can we see the list of "things"? EDIT: Here is a link to a version of keywords.py that is more complete than the one currently in the Data section of this competition:
> 
> [https://github.com/Kaggle/kaggle-environments/blob/master/kaggle_environments/envs/llm_20_questions/keywords.py](https://github.com/Kaggle/kaggle-environments/blob/master/kaggle_environments/envs/llm_20_questions/keywords.py)
> 
> 
> 
> > ## Matthew S Farmer
> > 
> > Check out the kaggle environment GitHub repo. 
> > 
> > 
> > 


---

> ## Jasper Butcher
> 
> Does this mean once these new keywords are released, the final test set will be the same?
> 
> 
> 


---

> ## VassiliPh
> 
> how the current keyword list was obtained from the full future keyword list?
> 
> I could imagine at least four possible situations:
> 
> Situation 1: Random sampling
> 
> You had a full list of keywords for the future final validation you you randlomly sampled 1000 keywords from it to make the currently used list of keywords.
> 
> It means we can assume that ratio of different groups (countries, cities, mountains, rivers, houshold items, etc) in the final keyword list will be the same as in the currently used 1000 keywords.
> 
> Situation 2: Random sampling from different groups
> 
> You had a full list of keywords for the future final validation as a list of groups (countries, cities, mountains, rivers, houshold items, etc) and you randomly sampled some amoung from each group to get the currently used 1000 keywords.
> 
> It means we can assume that all main groups that will be used in the final keyword list are represented in the current used 1000 keywords but their ratio can be different.
> 
> Situation 3: Taking some groups
> 
> You had a full list of keywords for the future final validation as a list of groups (countries, cities, mountains, rivers, houshold items, etc) and you took come of those groups to get the currently used 1000 keywords.
> 
> It means that groups used in the current keyword list will be taken as it for the future final keyword list but some new groups can be added.
> 
> Situation 4: Soemthing else
> 
> Thank you for answering, this information is indeed critically important to design any reasonable solution.
> 
> 
> 


---

> ## riju3107
> 
> Hey wanted to ask, what are we guessing? Is it limited to places and locations? or are we guessing people? This would be helpful for designing the chatbot. 
> 
> 
> 


---

> ## Marcel0.
> 
> When the final set of words is added and the submissions closed, will they be accessible on the keyword.py file? If so, even if I couldn't modify my code, I could build it to consider only the possibilities in this file.
> 
> 
> 
> > ## Naive Experimentalist
> > 
> > As per my understanding the hidden set of keywords will not be accessible on the keyword. However as more and more people doubt, it is more and more important to answer it clearly by Kaggle team. Their answer may have a great impact on how people implement their solutions.
> > 
> > 
> > 
> > ## Bovard Doerschuk-Tiberi
> > 
> > No, they will not be accessible in the keywords.py file
> > 
> > 
> > 
> > > ## sayoulala
> > > 
> > > Let me confirm my understanding: this means we will not have access to the final keywords, but the final keywords come from the same source as the current leaderboard keywords, correct?
> > > 
> > > 
> > > 


---

> ## Muhammad
> 
> Can we consider the Temple, Effil Tower, Pyramids, etc as a place?
> 
> 
> 


---

> ## Matthew S Farmer
> 
> Will 'person' be added as a category at some point? 
> 
> 
> 
> > ## Matthew S Farmer
> > 
> > Nevermind, I saw this answered elsewhere. 
> > 
> > 
> > 
> > > ## Naive Experimentalist
> > > 
> > > What answer have you found? As per my observation, persons appear in the competition, despite it has been said they would not.
> > > 
> > > 
> > > 
> > > ## OminousDude
> > > 
> > > I saw your discussion about this is just a typo or mistake
> > > 
> > > 
> > > 


---



</div>
<div class="column-right">

# 日本語訳

# 新しい隠れたキーワード
**Bovard Doerschuk-Tiberi** *2024年6月27日 木曜日 09:37:42 JST* (10票)
現在、一部のキーワードは隠れたテストセットから引き出されています。このセットには、500の場所（keywords.pyから）、500の物（keywords.pyから）、および1000の新しい物（隠れたセット）が含まれています。数週間内にこれらの隠れたキーワードの完全なリストを公開する予定です（さらに追加する可能性もあります）。それにもかかわらず、キーワードセットの変更は最小限に抑え、最終データセットをできるだけ代表するものに保ちたいと考えています。リーダーボードやエージェントを引き続き監視し、競技が堅牢であることを確認します。
幸運を祈ります。カグルを楽しんでください！

---
# 他のユーザーからのコメント
> ## Sumo
> 
> [@bovard](https://www.kaggle.com/bovard) すでにどこかで答えが出ているかもしれませんが、すべてのスレッドを確認した結果、私はまだ混乱しています。将来このスレッドを読む他の人のためにも、ここで尋ねることにしました：
> 
> このコンペティションについて、どちらのケースが正しいか確認できますか？
> 
> - 公開LBはkeywords.pyと隠れたキーワードセットから。プライベートLBもこの隠れたキーワードのセットから。
> 
> - 公開LBはkeywords.pyと隠れたキーワードセットから。プライベートLBは全く異なる隠れたキーワードのセットから。
> 
> - その他？
> 
> ありがとう
> 
> >
> > ## Naive Experimentalist
> > 
> 2番目の選択肢だと思います。
> >
> >
> > ## Bovard Doerschuk-Tiberi
> >
> > プライベートLBは同じ隠れたキーワードのセットからです。ただし、最終評価のためには再利用されることはありません。
> >
> >

---
> ## DJ Sterling
> 
> 大多数の場所に関するキーワードは、誤字や曖昧さのために削除しました。また、ハードコーディングされたエージェントに対処するためにも役立ちます。今後、新しいエントリーを場所のカテゴリーに追加することを検討しています。
> 
> 

---
> ## Max Brown
> 
> もしこれらの「隠れたセット」のキーワードを現在のマッチアップで使われているキーワードセットにすでに追加しているなら、エピソードの再生を見たりスクレイピングしたりすることでそれらを得ることができるのを防ぐものは何ですか？ありがとう！
> 
> 編集：また、コンペティションの「データ」セクションにあるkeywords.pyファイルには国、都市、ランドマークのカテゴリーしかありません。「物」のリストはどこで見ることができますか？ 編集：こちらは、コンペティションのデータセクションにあるものよりも完全なバージョンのkeywords.pyへのリンクです：
> 
> [https://github.com/Kaggle/kaggle-environments/blob/master/kaggle_environments/envs/llm_20_questions/keywords.py](https://github.com/Kaggle/kaggle-environments/envs/llm_20_questions/keywords.py)
> 
> >
> > ## Matthew S Farmer
> > 
> > Kaggle環境のGitHubリポジトリを確認してください。
> > 
> >

---
> ## Jasper Butcher
> 
> 新しいキーワードが公開されると、最終テストセットは同じものになるということでしょうか？
> 
> 
> 
---
> ## VassiliPh
> 
> 現在のキーワードリストは、将来の完全なキーワードリストからどのように得られたのですか？
> 
> 少なくとも4つの可能性があると考えられます：
> 
> 状況1：ランダムサンプリング
> 
> 将来の最終検証のための完全なキーワードリストを持っていて、その中からランダムに1000個のキーワードをサンプリングして現在の使用されているキーワードリストを作成しました。
> 
> これは、最終キーワードリストにおける異なるグループ（国、都市、山、川、家庭用品など）の比率が、現在使用されている1000のキーワードと同じであることを意味します。
> 
> 状況2：異なるグループからのランダムサンプリング
> 
> 将来の最終検証のための完全なキーワードリストをグループ（国、都市、山、川、家庭用品など）のリストとして持っていて、それぞれのグループからランダムに一部をサンプリングして現在使用されている1000のキーワードを作成しました。
> 
> これは、最終キーワードリストで使用されるすべての主なグループが現在使用されている1000のキーワードに含まれていることを意味しますが、その比率は異なる可能性があります。
> 
> 状況3：いくつかのグループの取得
> 
> 将来の最終検証のための完全なキーワードリストをグループ（国、都市、山、川、家庭用品など）のリストとして持っていて、いくつかのグループを取り出して現在使用されている1000のキーワードを作成しました。
> 
> これは、現在のキーワードリストに使用されているグループが最終キーワードリストにそのまま採用されることを意味しますが、新しいグループが追加される可能性があります。
> 
> 状況4：その他の何か
> 
> ありがとうございました。この情報を理解することは、合理的なソリューションを設計するために非常に重要です。
> 
> 
---
> ## riju3107
> 
> 何を推測しているのか知りたかったです。場所や地理に限られたものか、それとも人物も含まれるのか？これがチャットボットの設計に役立つと思います。
> 
> 
---
> ## Marcel0.
> 
> 最終的な単語セットが追加され、提出が閉じられた場合、それらはkeywords.pyファイルでアクセス可能になりますか？そうであれば、私はコードを修正できなくても、このファイルにある可能性だけを考慮するように構築できます。
> 
> >
> > ## Naive Experimentalist
> > 
> > 私の理解では、隠れたキーワードのセットはkeywords.pyにはアクセスできません。ただし、多くの人が疑問を抱くにつれて、Kaggleチームが明確に答えることがますます重要になっています。その回答は、参加者のソリューションの実装方法に大きな影響を与えるかもしれません。
> >
> >
> > >
> > ## Bovard Doerschuk-Tiberi
> > 
> > いいえ、最終キーワードはkeywords.pyファイルにはアクセスできません。
> >
> >
> > >
> > > ## sayoulala
> > > > 私の理解を確認させてください：これは、最終キーワードにアクセスできないが、最終キーワードが現在のリーダーボードキーワードと同じソースから来るということでしょうか？
> > > >
> > >
> > >
---
> ## Muhammad
> 
> テンプレート、エッフェル塔、ピラミッドなどは場所として考慮できますか？
> 
> 
---
> ## Matthew S Farmer
> 
> 「人物」はいつかカテゴリーとして追加されますか？
> 
> >
> > ## Matthew S Farmer
> > 
> > まあ、他の場所で回答が出ているのを見ました。
> > >
> > > ## Naive Experimentalist
> > > 
> > > あなたが見つけた答えは何ですか？私の観察では、人物もコンペティションに現れるが、それが言われたにも関わらずです。
> > >
> > > > ## OminousDude
> > > > あなたの議論を見ましたが、これは単なる誤字や間違いかもしれません。
> > > >
> > > >


</div>