# 要約 
このディスカッションは、KaggleのTPUの待ち時間が長すぎるという問題についてです。トピック作成者のSaiyan Warriorは、1時間以上待つこともあるTPUの待ち時間の長さに不満を表明し、どこに報告すべきか、Colab以外のTPUの選択肢があるのかを尋ねています。

Valentin Wernerは、LLMの台頭によりTPUのリソースが以前より多く使用されているため、待ち時間が長くなっている可能性を指摘しています。彼は、Kaggleがこれらのリソースを無料で提供していることに感謝し、ユーザーは製品フィードバックで不満を訴えるか、従来のGPUなどの代替手段を利用する必要があると提案しています。

Sparsh Tewatiaは、GoogleのTRCプログラムに応募してTPUへの無料アクセスを得ることを提案しています。

madarshbbは、TPUの待ち時間が長くなっていることを確認し、Kaggleの製品フィードバックで報告することを提案しています。彼は、GCSとAzure Sagemakerを試しましたが、設定が面倒だったと述べています。

Saiyan Warriorは、Kaggleプラットフォームに感謝しているものの、この問題が自分だけなのか、他のユーザーがどのような選択肢を使っているのかを知りたいと述べています。

このディスカッションは、KaggleのTPUの待ち時間の長さに対するユーザーの不満と、その問題に対する解決策を探る内容となっています。


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

# Too long waiting time for TPU

**Saiyan Warrior** *Thu Jul 04 2024 19:11:11 GMT+0900 (日本標準時)* (1 votes)

Hi Kaggler, 

Are you also facing too long waiting time/queue( sometimes more than 1 hour) for TPU usage? 
To whom should we raise this issue? 
What other options are you trying for TPU besides colab?


---

 # Comments from other users

> ## Valentin Werner
> 
> Not sure about many other options. With the rise of LLMs, these resources have been used a lot more. You can raise feature requests and complain about stuff like this in Product Feedback: [https://www.kaggle.com/discussions/product-feedback?sort=published](https://www.kaggle.com/discussions/product-feedback?sort=published)
> 
> However, Kaggle provides these resources for free so you dont have to provide them yourself and to even out the playing field for these competitions a bit. I think its important to either be grateful for what Kaggle provides (of course you can still raise it in product feedback), or adapt & overcome and find a solution that works for you. There are many alternatives for the goold old GPU - which still works well 😉
> 
> 
> 
> > ## Saiyan WarriorTopic Author
> > 
> > [@valentinwerner](https://www.kaggle.com/valentinwerner) 
> > 
> > I am not only grateful for computing but also for the kaggle platform itself I have learned a lot from this platform.
> > I just wanted to check whether this happening to me only or in general and what option others are using.
> > 
> > 
> > > ## Sparsh Tewatia
> > > 
> > > Try applying for TRC google program , they give I think 1 month of free access to TPUs
> > > 
> > > 
> > > 


---

> ## madarshbb
> 
> 1) Yes, it is an issue for quite some time now.
> 
> 2) You can raise this in kaggle's product feedback
> 
> 3) I tried GCS and azure sagemaker. But they have quite a cumbersome setup process. Would much rather wait for kaggle's TPU for a few hours, but less TPU waiting time would be a blessing.
> 
> 
> 
> > ## Saiyan WarriorTopic Author
> > 
> > Thanks [@madarshbb](https://www.kaggle.com/madarshbb) 
> > 
> > 
> > 


---



</div>
<div class="column-right">

# 日本語訳

# TPUの待ち時間が長すぎる

**Saiyan Warrior** *2024年7月4日 19:11:11 (日本標準時)* (1票)
皆さん、こんにちは。

TPUの使用待ち時間が長すぎる（1時間以上かかる場合もあります）という問題に直面していませんか？

この問題をどこに報告すればよいのでしょうか？

Colab以外のTPUの選択肢として、他にどのようなものがありますか？

---
# 他のユーザーからのコメント

> ## Valentin Werner
> 
> 他の選択肢についてはよくわかりません。LLMの台頭により、これらのリソースは以前よりはるかに多く使用されています。機能リクエストを提出したり、このような問題について[https://www.kaggle.com/discussions/product-feedback?sort=published](https://www.kaggle.com/discussions/product-feedback?sort=published)の製品フィードバックで不満を訴えたりすることができます。
> 
> しかし、Kaggleはこれらのリソースを無料で提供しているので、自分で用意する必要がなく、これらのコンペティションの競技場をある程度公平にすることができます。Kaggleが提供してくれることに感謝するか、あるいは適応して克服し、自分に合った解決策を見つけることが重要だと思います。従来のGPUには多くの代替手段があり、それでもうまく機能します😉
> 
> 
> 
> > ## Saiyan Warriorトピック作成者
> > 
> > [@valentinwerner](https://www.kaggle.com/valentinwerner) 
> > 
> > 私は、コンピューティングだけでなく、Kaggleプラットフォーム自体にも感謝しています。このプラットフォームから多くのことを学びました。
> > これは私だけなのか、それとも一般的に起こっているのか、そして他のユーザーがどのような選択肢を使っているのかを知りたかっただけです。
> > 
> > 
> > > ## Sparsh Tewatia
> > > 
> > > GoogleのTRCプログラムに応募してみてください。彼らは、TPUへの1か月間の無料アクセスを提供していると思います。
> > > 
> > > 
> > > 
---
> ## madarshbb
> 
> 1) はい、これはしばらく前から問題になっています。
> 
> 2) Kaggleの製品フィードバックで報告することができます。
> 
> 3) GCSとAzure Sagemakerを試してみました。しかし、設定プロセスが非常に面倒です。数時間待ってもKaggleのTPUを使いたいですが、TPUの待ち時間が短くなれば幸いです。
> 
> 
> 
> > ## Saiyan Warriorトピック作成者
> > 
> > [@madarshbb](https://www.kaggle.com/madarshbb) 
> > 
> > 
> > 
---



</div>