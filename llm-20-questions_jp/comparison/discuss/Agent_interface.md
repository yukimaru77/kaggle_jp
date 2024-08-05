# 要約 
コンペのディスカッションでは、参加者の**alekh**がエージェントインターフェースの実装方法について質問を投げかけています。彼はコンペの進行状況が不明であることを示しています。これに対して、**VolodymyrBilyachat**がピン留めされたノートブックへのリンクを提供し、エージェントの実装に必要な情報を共有しています。**alekh**はノートブックを確認したものの、最小限の要件やエントリーポイントを把握するのが難しかったと述べ、重要な情報が隠れていることに不満を抱いています。**Bovard Doerschuk-Tiberi**は、エントリーポイントについて適切にフォローアップし、main.pyファイルの最後の関数が観察と応答のやり取りに関与していることを確認しています。

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

# Agent interface

**alekh** *Mon May 20 2024 08:34:21 GMT+0900 (日本標準時)* (1 votes)

Is there some kind of agent interface we can implement? Right now it's kinda unclear how this whole competition works.



---

 # Comments from other users

> ## VolodymyrBilyachat
> 
> Have you seen pinned notebook ? [https://www.kaggle.com/code/ryanholbrook/llm-20-questions-starter-notebook](https://www.kaggle.com/code/ryanholbrook/llm-20-questions-starter-notebook)
> 
> 
> 
> > ## alekhTopic Author
> > 
> > Yes, I've seen it, but it's a bit hard to parse what is the minimal requirement and where the entry point is etc. But I found some usefull information hidden away in the submission modal.  Basically the last function of your main.py file should take an observation and return the response. - I think that is important information and shouldn't have been hidden away like that.
> > 
> > 
> > 
> > > ## Bovard Doerschuk-Tiberi
> > > 
> > > Apologies, and yes, the entry point is the last function of main.py
> > > 
> > > 
> > > 


---



</div>
<div class="column-right">

# 日本語訳

# エージェントインターフェース
**alekh** *2024年5月20日 08:34:21 (日本標準時)* (1票)
エージェントインターフェースを実装するための何かがありますか？今のところ、このコンペティションがどう進行するのかがよく分かりません。

---
# 他のユーザーからのコメント
> ## VolodymyrBilyachat
> 
> ピン留めされたノートブックを見ましたか？ [https://www.kaggle.com/code/ryanholbrook/llm-20-questions-starter-notebook](https://www.kaggle.com/code/ryanholbrook/llm-20-questions-starter-notebook)
> 
> 
> > ## alekh トピック作成者
> > 
> > はい、見ましたが、最小限の要件やエントリーポイントがどこにあるのかを把握するのが少し難しいです。しかし、提出モーダルに隠れている有用な情報を見つけました。基本的に、main.pyファイルの最後の関数は観察を受け取り、応答を返す必要があります。これは重要な情報で、こんな風に隠れているべきではないと思います。
> > 
> > > ## Bovard Doerschuk-Tiberi
> > > > お詫び申し上げます。その通り、エントリーポイントはmain.pyの最後の関数です。
> > > > 
> > > > 


</div>