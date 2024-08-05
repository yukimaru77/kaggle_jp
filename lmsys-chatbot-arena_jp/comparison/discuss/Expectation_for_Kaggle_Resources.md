# 要約 
このディスカッションは、Kaggleコンペティションにおけるリソース不足と提出時間の遅延に関するものです。トピック作成者のCody_Nullは、以前は6時間で完了していた提出が、現在タイムアウトしていることを報告しています。これは、コンペティションの締め切りが近づくにつれて、処理速度が大幅に低下しているためです。

他のユーザーは、Cody_Nullの懸念に共感し、同様の問題を経験していることを表明しています。Valentin Wernerは、スクリプトが全く同じであることを確認し、参加率がGPU処理時間を上げるという考えに疑問を呈しています。Rise_Handは、コンテナは同じではなく、一部の提出はより多くのコンピュータリソースを必要とするため、より少ないリソースを必要とする提出よりも早く実行を完了できることを指摘しています。

yechenzhi1は、max-lengthを減らすことを提案し、Attackerは、コンペティションの締め切りが近づくにつれて、参加率が上昇するため、サーバーが不安定になる可能性があると述べています。

Cody_Nullは、このコンペティションで他のコンペティションと何か違う点に気づかないことを認めながらも、提出が50%遅くなったことは一度もなかったため、何が起きているのか、締め切りまでに状況が変わるのか、もう少し詳しく知りたいと考えています。

このディスカッションは、Kaggleコンペティションにおけるリソースの制限と、コンペティションの締め切りが近づくにつれて発生する可能性のある問題を浮き彫りにしています。Cody_Nullの懸念は、他のユーザーからも共有されており、Kaggleチームからの説明を求める声が高まっています。


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

# Expectation for Kaggle Resources?

**Cody_Null** *Thu Aug 01 2024 08:16:38 GMT+0900 (日本標準時)* (11 votes)

Hi all, my team as well as what seems like others seem to be struggling with submission times. Even submissions that we ran in 6 hours before are now timing out? We have significantly raised our CV in the last few days but have been entirely unable to get results for it due to this compute issue. I was hoping some of the Kaggle staff could help speak to what is going on? I am familiar that close to the end of competitions in the last 2 or 3 days things run a bit slower but we are experiencing 2 times longer inference time than 4 days ago and have been ever since 7 days to go! It would be a shame to put in all this work over the last several months and not get to benefit from putting it all together. 



---

 # Comments from other users

> ## Valentin Werner
> 
> Are you 100% sure you are running exactly the same script? We have been struggling with Resources too, but not along the lines of 50%. Eventhough this wastes a submission, if you have time for it, try the old notebook and version again.
> 
> To me it does not seem reasonable that participation rates raise GPU Processing times. It is not like we are all on the same two T4s. Also all the environments are containers, so they should be clean on every run.
> 
> 
> 
> > ## Cody_NullTopic Author
> > 
> > I totally agree, it is not completely identical but it is a small change and identical in simulated run times. It’s not quite a 50% slowdown but it’s fairly close! What once took 5.5 is now 9+
> > 
> > 
> > 
> > ## Rise_Hand
> > 
> > It's not same as container actually. Some sub obviously need more computer source can finish running faster than the one which need less. So it's just a luck game to be allocated to a better machine tbh
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > Agreed, over the lifecycle of every chip performance may vary. This also goes for room temperature at servers etc. 
> > > 
> > > The point, I am making about containerization is that when you submission is over you have a clean GPU, its not like you will share compute etc. - However, you can and will get worse chips. Its impossible for the kaggle team to have all GPUs available perform exactly the same. 
> > > 
> > > 
> > > 


---

> ## yechenzhi1
> 
> Try to reduce your max-length? I've encountered a similar issue, and I suspect that the test data may be longer than what we used for training.
> 
> 
> 


---

> ## Attacker
> 
> People's participation rate rises before the competition closes, so the server becomes unstable.
> 
> 
> 
> > ## Cody_NullTopic Author
> > 
> > That is true but I don’t notice anything different from this comp than others but I have never seen a 50% slowdown of submissions before :/ Of course we can’t expect Kaggle to have it be seamless especially when they are providing these GPUs for free but I would like a little more clarity on what is going on and if we should expect it to change before the deadline.
> > 
> > 
> > 


---

> ## Korey Ma
> 
> I am afraid that my new submissions will time out🫠
> 
> 
> 
> > ## Valentin Werner
> > 
> > 
> > 
> > 
> > 


---



</div>
<div class="column-right">

# 日本語訳

## Kaggleリソースに関する期待

**Cody_Null** *2024年8月1日 木曜日 08:16:38 GMT+0900 (日本標準時)* (11票)
皆さん、私のチームだけでなく、他のチームも提出時間の遅延に苦労しているようです。以前は6時間で完了していた提出が、現在タイムアウトしています。ここ数日でCVは大幅に改善しましたが、この計算上の問題のため、その成果を全く得ることができません。Kaggleのスタッフの方々に、何が起きているのか説明していただけないでしょうか？コンペティションの締め切りが2、3日前に近づくと、処理速度が少し遅くなることは承知していますが、7日前から、4日前と比べて推論時間が2倍になっています！数ヶ月かけて努力してきた成果をまとめることができず、非常に残念です。

---
## 他のユーザーからのコメント

> ## Valentin Werner
> 
> スクリプトが全く同じであることを100%確信していますか？私たちもリソースに苦労していますが、50%というレベルではありません。たとえ提出が無駄になっても、時間があれば、古いノートブックとバージョンをもう一度試してみてください。
> 
> 参加率がGPU処理時間を上げるというのは、理にかなっているとは思えません。私たち全員が同じ2つのT4を使用しているわけではありません。また、すべての環境はコンテナなので、実行するたびにクリーンになるはずです。
> 
> 
> 
> > ## Cody_Nullトピック作成者
> > 
> > 同意します。全く同じではありませんが、小さな変更であり、シミュレーション実行時間では同じです。50%の遅延ではありませんが、かなり近い数字です！以前は5.5分かかっていたものが、今は9分以上かかっています。
> > 
> > 
> > 
> > ## Rise_Hand
> > 
> > 実は、コンテナは同じではありません。一部の提出は、より多くのコンピュータリソースを必要とするため、より少ないリソースを必要とする提出よりも早く実行を完了できます。そのため、より良いマシンに割り当てられるかどうかは、運任せです。
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > 同意します。すべてのチップのライフサイクルにおいて、パフォーマンスは変化する可能性があります。これは、サーバーの室温などにも当てはまります。
> > > 
> > > コンテナ化について私が言いたいのは、提出が完了すると、クリーンなGPUが得られるということです。計算を共有するわけではありません。ただし、より性能の低いチップが割り当てられる可能性はあります。Kaggleチームが、すべてのGPUが全く同じパフォーマンスを発揮するようにすることは不可能です。
> > > 
> > > 
> > > 
---
> ## yechenzhi1
> 
> max-lengthを減らしてみてください。同様の問題に遭遇しましたが、テストデータがトレーニングで使用したものよりも長い可能性があります。
> 
> 
> 
---
> ## Attacker
> 
> コンペティションの締め切りが近づくにつれて、参加率が上昇するため、サーバーが不安定になります。
> 
> 
> 
> > ## Cody_Nullトピック作成者
> > 
> > 確かに、それは事実ですが、このコンペティションで他のコンペティションと何か違う点に気づきません。しかし、これまで提出が50%遅くなったことは一度もありませんでした。もちろん、Kaggleが無料でGPUを提供していることを考えると、完璧に動作することを期待することはできませんが、何が起きているのか、締め切りまでに状況が変わるのか、もう少し詳しく知りたいです。
> > 
> > 
> > 
---
> ## Korey Ma
> 
> 新しい提出がタイムアウトするのではないかと心配です。🫠
> 
> 
> 
> > ## Valentin Werner
> > 
> > 
> > 
> > 
> > 
---



</div>