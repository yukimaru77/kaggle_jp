# 要約 
このコンペティションのディスカッションでは、最終週に向けた重要な更新情報が発表されました。以下の変更が実施されます：

1. アクティブエージェントが3から2に減少し、これによりゲームのペースが速くなります。
2. 質問の文字数制限が2000から750に引き下げられることが決定しました。これは、「バイナリサーチ」タイプ以外では、この追加の文字数制限が使用されないためです。
3. キーワードセットから「ロケーション」が削除されます。この変更は、今週から適用され、問題空間が小さすぎるためです。

最終評価期間中には、見えない「物体」のキーワードリストが利用され、リーダーボードはリセットされます。評価後の期間は初めは2週間ですが、延長の可能性もあります。

ディスカッションには多くの質問や確認が寄せられ、主催者はそれに対して適宜回答しています。「ロケーション」キーワードの削除に関しては敏感な反応があり、参加者に混乱を引き起こす可能性があると指摘されています。また、エージェントの使用についての提案も行われていますが、主催者はルールを明確にし、今後のコンペティションの改善に努める意向を示しています。

全体として、このディスカッションはコンペティションの進行状況とルールの変更についての重要な情報共有の場となっています。また、参加者同士の相互作用が活発であり、コミュニティとしての結束感が感じられる内容となっています。

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

# Competition Update

**Bovard Doerschuk-Tiberi** *Wed Jul 31 2024 05:47:37 GMT+0900 (日本標準時)* (21 votes)

Hey all,

Here is an update on what to expect from the final weeks of the competition.

- Active agents reduced from 3 to 2 (starting this week, which will increase the game rate)

- Question character length limit reduced from 2000 to 750 (the extra character limit was unused other than for “binary search” type questions)

- Remove “Locations” from the keyword set. (starting this week, the “locations” problem space it too small)

When the competition closes:

- The unseen secret “things” keyword list will be swapped in

- The leaderboard will be reset

- The post-evaluation period will start at 2 weeks, but will likely be extended.

Thank you all for participating! This competition is the first of its kind and we appreciate your patience while we learned along the way. We’ll take what we learned in this competition to make future competitions even better!

Happy Kaggling!

Bovard

EDIT: 

On the secret "things" keyword list

- it is taken from roughly same keyword list as the current list. 

- it will not re-use any of the current words in the keyword list

- it will not be accessible in keywords.py



---

 # Comments from other users

> ## Chernov Andrey
> 
> Hello! I still see in today's simulations locations keyword, namely Norway. Are you going to exclude locations or not?
> 
> Thank you for your clarification!
> 
> 
> 


---

> ## BORAHMLEE
> 
> Hi, Do you use purely secret keywords in your final evaluation? Or do you combine them with current keywords to make the evaluation?
> 
> 
> 


---

> ## torino
> 
> [@Hi](https://www.kaggle.com/Hi) [@bovard](https://www.kaggle.com/bovard) ,
> 
> Remove “Locations” from the keyword set. (starting this week, the “locations” problem space it too small)
> 
> That means in private keywords, the keywords will not have locations(place, landmark, mountain, river...) and only thing keywords, right?
> 
> Then agents reduced from 3 -> 2, is it keep 2 newest agents or 2 highest score agents?
> 
> 
> 
> > ## Bovard Doerschuk-Tiberi
> > 
> > Yes, keep only the "things" keywords.
> > 
> > It will be the 2 newest agents
> > 
> > 
> > 


---

> ## Ariocx
> 
> So keywords can only be “things”？
> 
> 
> 
> > ## Bovard Doerschuk-Tiberi
> > 
> > yes, that is correct
> > 
> > 
> > 
> > > ## Gavin Cao
> > > 
> > > Then will obs.category be all "things" or empty or have new subcategories within things?
> > > 
> > > 
> > > 


---

> ## Nicholas Broad
> 
> Is [this comment](https://www.kaggle.com/competitions/llm-20-questions/discussion/512358#2872495) no longer relevant?
> 
> Yes, the current leaderboard will be the seed of your agent going into the final evaluation period. We will ensure that agents receive enough games for the leaderboard to stabilize under the new set of words, so even if your agent is severly under ranked it should not be an issue.
> 
> 
> 
> > ## Bovard Doerschuk-Tiberi
> > 
> > Yes, that will no longer be the case.
> > 
> > 
> > 


---

> ## Bhanu Prakash M
> 
> Are all the items in the things category physical objects?
> 
> Can I rule out the possibility of there being virtual or abstract things?
> 
> 
> 
> > ## Bovard Doerschuk-Tiberi
> > 
> > The current list of words is roughly representative of the final list. 
> > 
> > 
> > 


---

> ## Andrew Tratz
> 
> A suggestion, for this or for other simulations in the future: allow participants to permanently inactivate specific bots, reducing their bot quota usage. This way, there's no need to inactivate high-scoring bots in order to continue experimenting, and if they are permanently disabled then there's no risk of anyone sandbagging by temporarily disabling and later re-enabling a strong bot. I think this would create a more robust competition with few downsides.
> 
> 
> 
> > ## Fayez Siddiqui
> > 
> > Great suggestion, I also think having the freedom of Agent selection would be great.
> > 
> > 
> > 
> > > ## OminousDude
> > > 
> > > Not a good idea as people could just enable a high-scoring old agent
> > > 
> > > 
> > > 


---

> ## Tran Anh Quan
> 
> So in the final leaderboard are there only “Things” keywords used for evaluation? Will there be no “Person” or “Place” keywords at all?
> 
> 
> 
> > ## Bovard Doerschuk-Tiberi
> > 
> > yes, only "things"
> > 
> > 
> > 


---

> ## Marcel0.
> 
> 
> Hey all,
> 
> Here is an update on what to expect from the final weeks of the competition.
> 
> - Active agents reduced from 3 to 2 (starting this week, which will increase the game rate)
> 
> - Question character length limit reduced from 2000 to 750 (the extra character limit was unused other than for “binary search” type questions)
> 
> - Remove “Locations” from the keyword set. (starting this week, the “locations” problem space it too small)
> 
> I noticed that the number of active agents is already 2, but I still see locations appearing in the keywords. Will they still be removed or is it a mistake in the removal?
> 
> 
> 
> > ## torino
> > 
> > Hi [@marceloluizgonalves](https://www.kaggle.com/marceloluizgonalves) ,
> > 
> > Remove “Locations” from the keyword set. (starting this week, the “locations” problem space it too small)
> > 
> > starting this week means it will be removed from the start of the final 14 days, not the current lb.
> > 
> > 
> > 
> > > ## Marcel0.
> > > 
> > > If that were the case, the number of agents should not have been already reduced.
> > > 
> > > 
> > > 
> > > ## Fayez Siddiqui
> > > 
> > > I agree with [@marceloluizgonalves](https://www.kaggle.com/marceloluizgonalves) here i also launched an agent with specific instructions to not guess place 😭😂
> > > 
> > > 
> > > 
> > > ## torino
> > > 
> > > [@bovard](https://www.kaggle.com/bovard), is a problem will be solved in the final lb?
> > > 
> > > 
> > > 


---

> ## francesco fiamingo
> 
> Thanks a lot! I think we are building the best community in the world, amazed to be part of it, one technical question , i need to decide to merge with other teams, if i will do, how many agents the team can use? 2 per component of the team or two for whole team? 
> 
> 
> 
> > ## torino
> > 
> > I guess we will have only have 2 agents for whole team.
> > 
> > 
> > 
> > > ## francesco fiamingo
> > > 
> > > Wow…but this means that is better not to merge….
> > > 
> > > 
> > > 
> > > ## torino
> > > 
> > > As author said 
> > > 
> > > Active agents reduced from 3 to 2 (starting this week, which will increase the game rate)
> > > 
> > > assume if we have 10 agents for team 5 members, maybe game rate will divide from 2 agents to 10 agents, It also means less opportunity for each agent.
> > > 
> > > 
> > > 
> > ## Bovard Doerschuk-Tiberi
> > 
> > Only 2 agents per team. Once you merge together two teams they only count as a single team so they would only have 2 active agents
> > 
> > 
> > 


---

> ## Duc-Vu Nguyen
> 
> Dear [@bovard](https://www.kaggle.com/bovard),
> 
> I have a question about "It will not be accessible in keywords.py". Does this mean that we cannot know secret words by reading keywords.py or any other sources provided by the organizer?
> 
> Best regards,
> 
> 
> 
> > ## mxmm2123
> > 
> > yes, keyword.py in final lb can't access.
> > 
> > 
> > 
> > ## Bovard Doerschuk-Tiberi
> > 
> > 
> > Does this mean that we cannot know secret words by reading keywords.py or any other sources provided by the organizer?
> > 
> > That is correct. You will not be able to see the keyword list by any means.
> > 
> > 
> > 


---

> ## FullEmpty
> 
> Thank you for your update. I've walked through discussions, but this doesn't seem to be discussed.
> 
> Questions are limited to 2000  750 characters
> 
>   Guesses are limited to 100 characters
> 
> Is the limit applied per round or for total questions throughout the rounds?
> 
> Agents are given 60 seconds per round to answer
> 
>   Agents have an additional 300 overage seconds to use throughout the game
> 
> I think this means each of the questioning/guessing agent and the answering agent has 60 seconds. But when does the 60 seconds for the questioning/guessing agent start — at the point when the round begins, when the agent asks a question, or right after the answering agent responds for guessing?
> 
> 
> 
> > ## FullEmpty
> > 
> > Can anyone help???
> > 
> > 
> > 
> > > ## torino
> > > 
> > > Hi [@gowillgo](https://www.kaggle.com/gowillgo) ,
> > > 
> > > ```
> > > Questions are limited to 2000 750 characters
> > > Guesses are limited to 100 characters
> > > 
> > > ```
> > > 
> > > it apply for each question, and each guess, not cumulative across entire game.
> > > 
> > > then game work as below:
> > > 
> > > 60s first - agent 1(ask/guess)
> > > 
> > > - load model(only in step 1, ~40s for model 8b 8bit)
> > > 
> > > - return first question
> > > 
> > > - if > 60s, subtract to budget 300s
> > > 
> > > -> agent 1 stop
> > > 
> > > immediately count 60s of agent 2(answer)
> > > 
> > > - load model(~40s)
> > > 
> > > - answer question or anything you want
> > > 
> > > - if > 60s, subtract to budget 300s
> > > 
> > > -> agent 2 stop
> > > 
> > > immediately count 60s of agent 1(ask/guess)
> > > 
> > > - return guess(model was load in step 1)
> > > 
> > > …
> > > 
> > > 
> > > 
> > > ## FullEmpty
> > > 
> > > [@pnmanh2123](https://www.kaggle.com/pnmanh2123) That's so crisp clear to understand - many thanks!!! 
> > > 
> > > 
> > > 
> > > ## torino
> > > 
> > > You are welcome!
> > > 
> > > 
> > > 


---



</div>
<div class="column-right">

# 日本語訳

# コンペティションの更新
**Bovard Doerschuk-Tiberi** *2024年7月31日水曜日 05:47:37 GMT+0900 (日本標準時)* (21票)
皆さん、こんにちは。
コンペティションの最終週に向けての更新があります。
- アクティブエージェントが3から2に減少します（今週から開始、ゲームのペースが上がります）
- 質問の文字数制限が2000から750に引き下げられます（追加の文字制限は「バイナリサーチ」タイプの質問以外では使用されていませんでした）
- キーワードセットから「ロケーション」を削除します（今週から開始、「ロケーション」の問題空間は小さすぎます）

コンペティションが終了する際には：
- 見えない秘密の「物体」キーワードリストが交換されます
- リーダーボードがリセットされます
- 評価後の期間は最初は2週間ですが、延長される可能性があります。

皆さんの参加に感謝します！このコンペティションはこれまでにない初めての取り組みであり、私たちの学びの過程を通じてあなたのご理解に感謝します。今後のコンペティションをより良くするために、この経験を活かします！

ハッピーカグリング！
Bovard

編集：
秘密の「物体」キーワードリストについて
- 現在のリストとほぼ同様のキーワードリストから取られています。
- 現在のキーワードリストに含まれる単語は再利用されません。
- keywords.py ではアクセスできません。

---

## 他のユーザーからのコメント
> ## Chernov Andrey
> 
> こんにちは！今日のシミュレーションで「ロケーション」キーワード、特にノルウェーがまだ見えます。ロケーションは除外されるのでしょうか、それともそのままなのでしょうか？
> 
> ご確認ありがとうございます！

---

> ## BORAHMLEE
> 
> こんにちは、最終評価においては純粋に秘密のキーワードを使用するのでしょうか？それとも現在のキーワードと組み合わせて評価を行うのでしょうか？

---

> ## torino
> 
> [@Hi](https://www.kaggle.com/Hi) [@bovard](https://www.kaggle.com/bovard) ,
> 
> 「ロケーション」をキーワードセットから削除します（今週から開始、「ロケーション」の問題空間は小さすぎます）
> 
> ということは、プライベートなキーワードにはロケーション（場所、名所、山、川…）はなく、物体のキーワードだけになるということですね？
> 
> また、アクティブエージェントが3から2に減った場合、2つは最新のエージェントを保持するのでしょうか、それとも最高スコアのエージェントを保持するのでしょうか？
> 
> > ## Bovard Doerschuk-Tiberi
> > 
> > はい、「物体」キーワードのみを保持します。
> > > 
> > > それは最新の2つのエージェントです。
> > > 
> > > 
> > 

---

> ## Ariocx
> 
> つまりキーワードは「物体」のみということですか？

> ## Bovard Doerschuk-Tiberi
> 
> はい、その通りです。

> > ## Gavin Cao
> > > それでは、obs.categoryはすべて「物体」になりますか、それとも空になるか、物体の中に新しいサブカテゴリーが含まれるのでしょうか？

---

> ## Nicholas Broad
> 
> こちらのコメントはもはや関連性がないのですか？
> 
> 現在のリーダーボードは、最終評価期間に入る際のエージェントの基準となります。新しい単語のセットのもとでもリーダーボードが安定するために、エージェントには十分なゲームを提供するので、たとえエージェントのランクがかなり低くても問題にはなりません。

> > ## Bovard Doerschuk-Tiberi
> > 
> > はい、それはもはや問題ではありません。

> > 

---

> ## Bhanu Prakash M
> 
> 「物体」カテゴリーのすべての項目は物理的なオブジェクトですか？
> 
> 仮想的または抽象的なものが含まれる可能性は排除できますか？

> ## Bovard Doerschuk-Tiberi
> 
> 現在の単語リストは、最終リストを大まかに代表しています。

---

> ## Andrew Tratz
> 
> 提案ですが、今回または今後のシミュレーションにおいて：参加者が特定のボットを永久に非アクティブ化できるようにして、ボットのクオータ使用を減らすことを許可してください。これにより、高スコアのボットを一時的に非アクティブ状態にして後で再アクティブ化するリスクがなくなり、より健全な競技を構築できると思います。

> > ## Fayez Siddiqui
> > > 素晴らしい提案ですね、自由にエージェントを選択できるのは更に良いことだと思います。

> > > > ## OminousDude
> > > > 良い考えではないと思います。なぜなら、誰でも高スコアの古いエージェントを再度有効にできてしまう可能性があるからです。

---

> ## Tran Anh Quan
> 
> 最終リーダーボードでは「物体」キーワードのみが評価に使用されますか？「人」や「場所」のキーワードは全く存在しないということですか？

> ## Bovard Doerschuk-Tiberi
> 
> はい、「物体」だけです。

---

> ## Marcel0.
> 
> 皆さん、こんにちは。
> 
> コンペティションの最終週に向けての更新があります。
> 
> - アクティブエージェントが3から2に減少します（今週から開始、ゲームのペースが上がります）
> 
> - 質問の文字数制限が2000から750に引き下げられます（追加の文字制限は「バイナリサーチ」タイプの質問以外では使用されていませんでした）
> 
> - キーワードセットから「ロケーション」を削除します（今週から開始、「ロケーション」の問題空間は小さすぎます）
> 
> アクティブエージェントの数はすでに2になっていますが、それでもキーワードにロケーションが現れています。ロケーションはまだ削除されるのか、それとも削除に関する間違いがあるのですか？

> > ## torino
> > > こんにちは[@marceloluizgonalves](https://www.kaggle.com/marceloluizgonalves) ,
> > > 
> > > 「ロケーション」をキーワードセットから削除します（今週から開始、「ロケーション」の問題空間は小さすぎます）
> > > 
> > > 今週から開始するということは、最終的な14日間の開始時点から削除されるという意味で、現在のリーダーボードには未だ残ります。
> > > 
> > > 
> > > > ## Marcel0.
> > > > もしそれが正しければ、すでにアクティブエージェントの数が減少していてはいけないはずです。
> > > > 
> > > 
> > > > ## Fayez Siddiqui
> > > > はい[@marceloluizgonalves](https://www.kaggle.com/marceloluizgonalves)の言うことに同意します。私も具体的に「場所」を推測しないように指示してエージェントを起動しました 😭😂

> > > > > ## torino
> > > > > [@bovard](https://www.kaggle.com/bovard)、これは最終リーダーボードで解決される問題ですか？

---

> ## francesco fiamingo
> 
> ありがとうございます！私はこの世界で最高のコミュニティを構築していると思います、その一員であることを嬉しく思います。一つ技術的な質問がありますが、他のチームと統合することに決めた場合、チームは何人のエージェントを使用できますか？チームの各構成員ごとに2人、もしくは全体で2人ですか？

> > ## torino
> > > チーム全体で2人のエージェントになると思います。

> > > > ## francesco fiamingo
> > > > それは驚きですが、つまり統合しない方が良いということになるのですね……。

> > > > > ## torino
> > > > > 著者が言ったように、 
> > > > > 
> > > > > アクティブエージェントは3から2に減少します（今週から開始、ゲームのペースが上がります）
> > > > > 
> > > > > もしチームメンバーが10人いてエージェントが10人いた場合、ゲームのペースは2エージェントから10エージェントに分割されるかもしれません。つまり、各エージェントにとっての機会が少なくなるということです。
> > > > 
> > > ## Bovard Doerschuk-Tiberi
> > > > > チームあたり2人のエージェントのみです。2つのチームが統合すると、単一のチームとしてカウントされ、2つのアクティブエージェントしか持ちません。

---

> ## Duc-Vu Nguyen
> 
> 親愛なる[@bovard](https://www.kaggle.com/bovard)、
> 
> 「keywords.pyでアクセスできない」ということは、主催者が提供する他のいかなるソースからも秘密の単語を確認できないということを意味しますか？
> 
> 敬具、

> ## mxmm2123
> > はい、最終リーダーボードではkeywords.pyにはアクセスできません。

> > > ## Bovard Doerschuk-Tiberi
> > >
> > > このことは、主催者が提供する他のいかなるソースからも秘密の単語を確認できないということを意味しますか？
> > > 
> > > それは正しいです。あなたはキーワードリストを確認することはできません。

---

> ## FullEmpty
> 
> 更新ありがとうございます。ディスカッションを通り抜けましたが、これは議論されていないようです。
> 
> 質問は2000 750文字に制限されています。
> 
> 推測は100文字に制限されています。
> 
> これはラウンドごとに適用されるのか、ラウンド全体の合計質問に対して適用されるのか？
> 
> エージェントには、各ラウンドに60秒が与えられます。
> 
> エージェントは、ゲーム全体で使用できる追加の300秒の超過時間を持っています。
> 
> これは、おそらく質問するエージェントと回答するエージェントのそれぞれに60秒があることを意味します。しかし、質問するエージェントの60秒はいつ開始されるのでしょうか？ラウンドが始まった時点、質問をする時点、または回答エージェントが推測するための回答を行った後の時点ですか？

> > ## FullEmpty
> > > 誰か助けてくれる人はいませんか？？？

> > > > ## torino
> > > > こんにちは[@gowillgo](https://www.kaggle.com/gowillgo) ,
> > > > 
> > > > 質問は2000 750文字に制限されています。
> > > > 推測は100文字に制限されています。
> > > > 
> > > > これは各質問および各推測ごとに適用され、ゲーム全体に累積されるものではありません。
> > > >  
> > > > ゲームは次のように進行します：
> > > >  
> > > > 最初の60秒 - エージェント1（質問/推測）
> > > > 
> > > > - モデルをロード（ステップ1では約40秒、8ビットモデルの場合）
> > > > 
> > > > - 最初の質問を返す
> > > > 
> > > > - 60秒を超えた場合、バジェット300秒から差し引かれます。
> > > > 
> > > > -> エージェント1が停止
> > > > 
> > > > すぐにエージェント2（回答）の60秒がカウントされます。
> > > > 
> > > > - モデルをロード（約40秒）
> > > > 
> > > > - 質問に答える、または他のことをする
> > > > 
> > > > - 60秒を超えた場合、バジェット300秒から差し引かれます。
> > > > 
> > > > -> エージェント2が停止
> > > > 
> > > > すぐにエージェント1（質問/推測）の60秒がカウントされます。
> > > > 
> > > > - (モデルはステップ1でロードされているので)推測を返します。
> > > > 
> > > > …
> > > 

> > > ## FullEmpty
> > > > [@pnmanh2123](https://www.kaggle.com/pnmanh2123)、非常にわかりやすいです。ありがとうございました！！！

> > > ## torino
> > > > どういたしまして！
> > > 

---


</div>