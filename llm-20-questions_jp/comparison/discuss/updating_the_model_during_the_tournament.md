# 要約 
**ディスカッション要約:**

ユーザーAfordancjaは、トーナメント中にモデルがデータを保存・更新できるか、そして次の試合でもそのデータが利用可能かについて質問しました。彼は、モデルがゼロ状態で新しい試合を開始する必要があるのか疑問に思っています。

それに対して、Chris Deotteは、提出したモデルは一度提出されると変更できないと説明しました。ゲームの履歴はダウンロード可能で、過去のゲームを基にローカルで新しいモデルをトレーニングし、新バージョンを提出することはできると述べています。

Bovard Doerschuk-Tiberiは、試合中のローカルファイルや変更は試合終了時に破棄されるため、試合を跨いで自分自身を更新することはできないと強調しました。

さらに、loh-maaは、エージェントは環境からの応答を得るために呼び出されるだけで、オンライン学習は彼らのターン中に行なわれる必要があると指摘し、事前にロードされたデータ以外にはアクセスできないため、オンライン経験は限られると述べています。

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

# updating the model during the tournament

**Afordancja** *Thu May 30 2024 22:11:48 GMT+0900 (日本標準時)* (0 votes)

Can the model save data/update the mode during the tournament and will this data be available during subsequent fights?

whether the model must be completely trained locally and after uploading each new fight starts in the same zero state



---

 # Comments from other users

> ## Chris Deotte
> 
> My understanding is that we cannot change a submitted model. Once it is submitted, the weights are fixed.
> 
> We can however, download all the game history, train a new model locally to use past games, and then submit a new version of our model.
> 
> 
> 
> > ## AfordancjaTopic Author
> > 
> > 
> > My understanding is that we cannot change a submitted model. Once it is submitted, the weights are fixed.
> > 
> > yes, we cant, but questions is that the model can do it byself.
> > 
> > 
> > 
> > > ## Bovard Doerschuk-Tiberi
> > > 
> > > Any local files or changes made during a match will be discarded at the end of a match. The only thing that is loaded into a match is your submission bundle. So no, your model can't update itself across matches.
> > > 
> > > 
> > > 


---

> ## loh-maa
> 
> I think agents are called by the environment only to get responses, so any online training would have to take place during their turns/moves… on top of that, I don't think agents can have access to anything but their pre-loaded data, and their online experience, which probably would be too short to be useful..
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# トーナメント中のモデルの更新
**Afordancja** *2024年5月30日 22:11:48 (日本標準時)* (0票)
モデルはトーナメント中にデータを保存/更新できますか？ そのデータは次の試合でも利用可能ですか？ モデルは完全にローカルでトレーニングされる必要があり、その後アップロード後に各新しい試合が同じゼロ状態で開始されるのですか？

---
# 他のユーザーからのコメント
> ## Chris Deotte
> 
> 私の理解では、提出したモデルは変更できません。一度提出されると、重みは固定されます。
> 
> ただし、ゲームの履歴はすべてダウンロードできるので、過去のゲームを使ってローカルで新しいモデルをトレーニングし、新しいバージョンのモデルを提出することはできます。

> > ## Afordancja トピック作成者
> > 
> > 私の理解では、提出したモデルは変更できません。一度提出されると、重みは固定されます。
> > 
> > そうですね、変更できませんが、問題はモデルが自分自身で更新できるかどうかです。

> > > ## Bovard Doerschuk-Tiberi
> > > 
> > > 試合中に行われたローカルファイルや変更は、試合終了時に破棄されます。試合に読み込まれるのは、あなたの提出パッケージのみです。したがって、モデルは試合を跨いで自分自身を更新することはできません。
> > > 
> > > 

---
> ## loh-maa
> 
> エージェントは環境から応答を得るために呼び出されるだけだと思うので、オンライン学習は彼らのターン/ムーブ中に行なわれる必要があります…それに加えて、エージェントは事前にロードされたデータ以外にはアクセスできないと思うので、彼らのオンライン経験はおそらく、有益なくらいの長さにはならないでしょう。


</div>