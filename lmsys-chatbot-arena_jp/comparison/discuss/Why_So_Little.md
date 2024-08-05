# 要約 
このディスカッションは、Kaggleコンペティション「LMSYS - Chatbot Arena 人間による好み予測チャレンジ」のデータセットのサイズに関するものです。

投稿者は、コンペティション主催者が、LMSYSアリーナには90万件以上の投票があるにもかかわらず、なぜわずか6万件のデータしか提供していないのか疑問に思っています。

他のユーザーからのコメントでは、企業がすべてのデータを公開したくない理由はいくつかあると説明されています。6万件のサンプルは、多くのチャレンジで見られるよりも多いサイズであり、最初にテストするために小さなサブセットを使用するのに適しています。

また、企業がチャレンジを行う動機は様々であり、概念実証を行いたい、または何かが実現可能かどうかを調査したいと考えている場合もあると説明されています。Kaggleにこのようなチャレンジを開放することは、社内で同じことを行うよりも、コストが低く、解決策のアプローチの多様性が高いという利点があります。

さらに、企業は優勝したソリューションのライセンスを取得しており、独自のデータに移行できる可能性があると説明されています。

このディスカッションは、コンペティション主催者がデータセットのサイズを制限した理由について、いくつかの洞察を提供しています。


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

# Why So Little

**eli plutchok** *Wed May 08 2024 13:44:26 GMT+0900 (日本標準時)* (4 votes)

Hello Everyone, 

I'm new to kaggle. I'm wondering why the competition organizers gave us a data set of just ~60K items when they surely must have a lot more from the same place. Should I expect them to release more at a later date, or are they just trying to make it extra challenging for us?

(The LMSYS arena leaderboard is based on over 900k votes: [https://chat.lmsys.org/?leaderboard](https://chat.lmsys.org/?leaderboard))



---

 # Comments from other users

> ## Valentin Werner
> 
> There are many reasons why a company may not want to disclose all of their data. I think 60k samples are more than what we often see for challenges. This is already a size where you are taking a small subset to test things first.
> 
> 
> 
> > ## eli plutchokTopic Author
> > 
> > Ok, I get it. They don't want people to have their proprietary data. But still, they won't get the best pre-trained models by withholding the data. Do they care mainly about the code used to train the models? I guess, my dumb question is: what is the primary objective of, LMSYS, the company sponsoring this? 
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > They are licensed the winning solutions (see Rules #A1). These companies are often able to transfer solutions to their own data themselves. 
> > > 
> > > However, company motivation for challenges may vary: For example, they maybe want to proof a concept or make a study whether things are achievable. Opening such a challenge to kaggle is smart because doing the same thing internally will often be more expensive and less diverse in solution approaches.
> > > 
> > > 
> > > 


---



</div>
<div class="column-right">

# 日本語訳

# なぜデータが少ないのか？
**eli plutchok** *2024年5月8日 水曜日 13:44:26 日本標準時* (4票)

皆さん、こんにちは！

Kaggle初心者です。なぜコンペティション主催者は、同じ場所からもっと多くのデータがあるはずなのに、わずか6万件ほどのデータセットしか提供していないのでしょうか？後で追加でデータが公開されるのでしょうか、それとも単に私たちを困らせるためでしょうか？

（LMSYSアリーナのリーダーボードは90万件以上の投票に基づいています：[https://chat.lmsys.org/?leaderboard](https://chat.lmsys.org/?leaderboard)）

---
# 他のユーザーからのコメント
> ## Valentin Werner
> 
> 企業がすべてのデータを公開したくない理由はたくさんあります。6万件のサンプルは、多くのチャレンジで見られるよりも多いと思います。これは、最初にテストするために小さなサブセットを使用するサイズです。
> 
> 
> 
> > ## eli plutchokトピック作成者
> > 
> > わかりました。彼らは、独自のデータを公開したくないのでしょう。しかし、それでも、彼らはデータを隠すことで最良の事前学習済みモデルを得ることができません。彼らは、モデルをトレーニングするために使用されるコードを主に気にかけているのでしょうか？私の愚かな質問は、このコンペティションをスポンサーしているLMSYSという会社の主な目的は何ですか？
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > 彼らは、優勝したソリューションのライセンスを取得しています（ルール#A1参照）。これらの企業は、多くの場合、ソリューションを独自のデータに移行することができます。
> > > 
> > > しかし、企業がチャレンジを行う動機は様々です。例えば、概念実証を行いたい、または何かが実現可能かどうかを調査したいと考えているかもしれません。Kaggleにこのようなチャレンジを開放することは賢明です。なぜなら、社内で同じことを行うことは、多くの場合、より高価で、解決策のアプローチの多様性が低いからです。
> > > 
> > > 
> > > 
--- 



</div>