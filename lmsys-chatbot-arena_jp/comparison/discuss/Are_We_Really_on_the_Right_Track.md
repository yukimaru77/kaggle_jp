# 要約 
このコンペティションのディスカッションでは、参加者たちがコンペティションの目標である「人間の好みを予測する」ための適切なアプローチについて疑問を呈しています。

コンペティションの説明では、RLHF（人間のフィードバックからの強化学習）を用いることが推奨されていますが、実際には多くの参加者が既存のLLMをファインチューニングするというアプローチを取っています。

CPMPは、RLHFは教師あり学習の一種であり、コンペティションで提供されているラベルと非常に似ているため、参加者が別の方法を試す必要があるのか疑問視しています。

Dlond Mikeは、既存のLLMをファインチューニングすることが非常に効果的である一方で、高価なGPUが必要となるため、金持ちのためのゲームになっていると指摘しています。

chan peterは、RLHFモデルを試してみたものの、実行に時間がかかりすぎてコンペティションの締め切りまでに最適化できなかったと述べています。

このディスカッションは、コンペティションの目標を達成するための最良のアプローチがまだ明確になっていないことを示唆しています。参加者たちは、RLHFや既存のLLMのファインチューニングなど、さまざまなアプローチを試しており、その結果を比較検討しています。


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

# Are We Really on the Right Track?

**Lorry Zou** *Sun Jul 21 2024 23:33:24 GMT+0900 (日本標準時)* (2 votes)

From the competition description:

"This challenge aligns with the concept of "reward models" or "preference models" in reinforcement learning from human feedback (RLHF). Previous research has identified limitations in directly prompting an existing LLM for preference predictions. These limitations often stem from biases such as favoring responses presented first (position bias), being overly verbose (verbosity bias), or exhibiting self-promotion (self-enhancement bias)."

Looks like the competition host encourage us to try reinforcement learning but everyone is still fine-tuning existing LLMs.🙂🙃



---

 # Comments from other users

> ## CPMP
> 
> RLHF is a supervised learning method.  Labels are provided by humans, and are quite similar to the labels we have in this competition.
> 
> Not sure what you suggest we do differently.
> 
> 
> 


---

> ## Dlond Mike
> 
> yep….cause it's really perform great.it's a game for rich.(GPU :))
> 
> 
> 


---

> ## chan peter
> 
> I tried out rlhf model and use the reward score as input and build a simple classifier, it work out great, but running the rlhf model is too time comsuing and I joined comp a bit late, don't have enough time to optimize it to pass the time limit.
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# 私たちは本当に正しい道を歩んでいるのでしょうか？
**Lorry Zou** *2024年7月21日 日曜日 23:33:24 日本標準時* (2票)

コンペティションの説明から：
「このチャレンジは、人間のフィードバックからの強化学習（RLHF）における「報酬モデル」または「選好モデル」の概念と一致しています。以前の研究では、既存のLLMに直接プロンプトを与えて選好予測を行うことには限界があることが分かっています。これらの限界は、最初に提示された応答を好む傾向（位置バイアス）、過度に冗長になる傾向（冗長性バイアス）、自己宣伝を行う傾向（自己強化バイアス）などのバイアスに起因することがよくあります。」

コンペティション主催者は、強化学習を試すように促していますが、誰もが既存のLLMをファインチューニングしていますね。🙂🙃

---
# 他のユーザーからのコメント
> ## CPMP
> 
> RLHFは教師あり学習の方法です。ラベルは人間によって提供され、このコンペティションで私たちが持っているラベルと非常に似ています。
> 
> 私たちが何か違うことをすべきだと提案しているのか、よくわかりません。
> 
> 
> 
---
> ## Dlond Mike
> 
> ええ、だって本当に素晴らしいパフォーマンスを発揮するんだもん。金持ちのためのゲームだよ。（GPU :))
> 
> 
> 
---
> ## chan peter
> 
> RLHFモデルを試して、報酬スコアを入力として使用してシンプルな分類器を構築してみました。うまくいきましたが、RLHFモデルの実行には時間がかかりすぎ、コンペに少し遅れて参加したので、時間制限内に最適化して通過する時間がありませんでした。
> 
> 
> 
---



</div>