# 要約 
このディスカッションは、Kaggleコンペティション「LMSYS - Chatbot Arena 人間による好み予測チャレンジ」において、ある参加者（Roschild.Rui）が1時間で0.707という驚異的なスコアを達成したことに対する疑問と懸念が表明されています。

多くの参加者は、このスコアがデータセットの漏洩によって達成された可能性が高いと考えています。なぜなら、彼らのトレーニングセットの損失は、そのスコアにすら届いていないからです。また、1時間で推論を実行できるモデルが、これほど複雑な問題でこれほどまでに過学習できるのか疑問視する声も上がっています。

参加者たちは、この参加者が何らかの抜け穴を利用しているのではないかと疑い、コンペティションが終了する前にその方法を共有しないことを願っています。もし共有された場合、コンペティションは台無しになってしまうと懸念されています。

このディスカッションは、コンペティションの公正性に対する懸念と、参加者間の不正行為に対する警戒感を示しています。Kaggle運営チームが公正にこの問題に対処してくれることを期待する声も上がっています。 


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

# 1h -> .707! Is the dataset leaked?

**Roschild.Rui** *Sun Aug 04 2024 04:36:14 GMT+0900 (日本標準時)* (1 votes)

Unbelievable! I have great desire to know what’s really help and how could the master achieve this after the competition ending



---

 # Comments from other users

> ## sayoulala
> 
> I believe it's very likely. My training set loss couldn't even reach that score. As of now, his score has risen to 0.6 again… I hope Kaggle officials can handle this matter fairly.
> 
> 
> 
> > ## Valentin Werner
> > 
> > Training loss doesn't even get close to it. Even ignoring all remarks on speed of submission, I dont think a model that could run inference in an hour (likely the size of deberta Base or smaller), is even  able to overfit this hard on a problem this complex. 
> > 
> > Not going to lie, I would love him to have come up with some insane solution.
> > 
> > 
> > 
> > > ## Cody_Null
> > > 
> > > I feel the same way but I would be completely shocked haha
> > > 
> > > 
> > > 
> > > ## sayoulala
> > > 
> > > If he can come up with a better solution, the whole world will thank him. But if he's exploiting some loopholes, that would be truly disappointing.
> > > 
> > > 
> > > 


---

> ## Cody_Null
> 
> I hope he doesn’t share before competition end. Because if he does the comp is ruined lol 
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# 1時間で0.707！ データセットが漏洩したのか？
**Roschild.Rui** *2024年8月4日 日曜日 4:36:14 JST* (1票)
信じられない！ どんな方法で、そしてどのようにしてマスターはこのようなスコアを達成できたのか、本当に知りたいです。コンペティションが終わった後でも。
---
# 他のユーザーからのコメント
> ## sayoulala
> 
> データセットが漏洩した可能性は非常に高いと思います。私のトレーニングセットの損失は、そのスコアにすら届きませんでした。今のところ、彼のスコアは再び0.6に上昇しています… カグルの運営チームが公正にこの問題に対処してくれることを願っています。
> 
> 
> 
> > ## Valentin Werner
> > 
> > トレーニング損失は、それに近づくことすらできません。提出速度に関するすべてのコメントを無視しても、1時間で推論を実行できるモデル（おそらくDeBERTa Baseかそれ以下のサイズ）が、これほど複雑な問題でこれほどまでに過学習できるかどうかは疑問です。
> > 
> > 嘘ではありませんが、彼が何らかの驚くべき解決策を思いついたことを願っています。
> > 
> > 
> > > ## Cody_Null
> > > 
> > > 私も同じように思います。しかし、彼がそれを実現できたとしたら、本当に驚きます。
> > > 
> > > 
> > > 
> > > ## sayoulala
> > > 
> > > もし彼がより良い解決策を思いついたなら、世界中の人々が彼に感謝するでしょう。しかし、彼が何らかの抜け穴を利用しているのなら、それは本当に残念です。
> > > 
> > > 
> > > 
---
> ## Cody_Null
> 
> コンペティションが終了する前に、彼がその方法を共有しないことを願っています。もし彼が共有したら、コンペティションは台無しになってしまいます。
> 
> 
> 
--- 



</div>