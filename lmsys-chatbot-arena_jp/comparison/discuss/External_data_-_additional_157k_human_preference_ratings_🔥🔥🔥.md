# 要約 
このディスカッションは、KaggleのLMSYS - Chatbot Arena 人間による好み予測チャレンジの参加者によって共有された、157,000件の追加の人間による好み評価データセットに関するものです。

データセットの作成者であるDarek Kłeczekは、このデータセットが、より小さなモデルがより大きなLLMからの応答を効果的に評価できるかどうかを調べるのに役立つと述べています。このデータセットは、ArgillaによってHFに公開されたUltrafeedbackデータセットに基づいており、コンペティションのトレーニングデータ形式に変換されています。

しかし、このデータセットは、人間の評価者の代理としてGPT-4を判定者として使用していることが判明しました。また、Ultrafeedbackは意図的に同点をフィルターアウトしていますが、LMSYSデータセットでは、モデルaの勝利、bの勝利、同点の割合がほぼ均等に分布しています。

このデータセットの有効性については、いくつかの議論があります。Rich Olsonは、このデータセットを自分のノートブックに追加しても、リーダーボードのスコアが向上しなかったと述べています。一方、他の参加者は、このデータセットが事前トレーニングや疑似ラベル付けに役立つ可能性があると述べています。

全体として、このディスカッションは、このコンペティションの参加者にとって貴重なリソースとなる可能性のある、新しいデータセットの発表と、そのデータセットの有効性に関する議論についてです。


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

# External data - additional 157k human preference ratings 🔥🔥🔥

**Darek Kłeczek** *Fri May 03 2024 07:09:30 GMT+0900 (日本標準時)* (96 votes)

I'm super excited to see if smaller models (Kaggle GPU compatible) can effectively rate responses from much larger LLMs. To help you improve your models, I published a dataset with external data:

[https://www.kaggle.com/datasets/thedrcat/llm-human-preference-data-ultrafeedback/data](https://www.kaggle.com/datasets/thedrcat/llm-human-preference-data-ultrafeedback/data)

This is based on Ultrafeedback dataset published on HF by Argilla. I additionally converted it into the competition train data format. 

EDIT: Note that Ultrafeedback uses GPT4 as a judge as a proxy for human raters. I also added ties between models in version 2 that were previously filtered out. See original dataset paper [here](https://arxiv.org/pdf/2310.01377). Thanks [@nbroad](https://www.kaggle.com/nbroad) for catching this. 

Enjoy ❤️🙏👍



---

 # Comments from other users

> ## Dlond Mike
> 
> no use…but just for my notebook
> 
> 
> 


---

> ## Rich Olson
> 
> I added 50k of the items from this to my "Deberta + TF-IDF + Word2Vec + Length" notebook (it's public - I'd post a link - but Kaggle thinks I'm spamming).
> 
> got an identical 1.011 on the LB.  Had same experience with [this dataset](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/500973).
> 
> I take this as indication the data is probably good (or at least not bad) - it's just my notebook isn't able to benefit from the extra data.
> 
> 
> 


---

> ## Nicholas Broad
> 
> How do you think the tie should be handled? If the scores are equal, it should be a tie? (Your dataset only has "model a" winning)
> 
> Update:
> 
> I read more into how they processed the dataset and I noticed a few things:
> 
> I don't think this is human preferences. I think this is using [GPT-4 to rate the responses](https://github.com/OpenBMB/UltraFeedback/tree/main?tab=readme-ov-file#introduction)
> [Ultrafeedback intentionally filters out ties](https://huggingface.co/datasets/argilla/ultrafeedback-binarized-preferences/blob/main/README.md#dataset-processing), whereas the LMSYS dataset has roughly even split between model a winning, b winning, and ties.  
> 
> 
> > ## Darek KłeczekTopic Author
> > 
> > Great catch, thanks! I'll update the thread. I think this can be still useful for pretraining or pseudolabeling. Also found the paper here: [https://arxiv.org/pdf/2310.01377](https://arxiv.org/pdf/2310.01377)
> > 
> > 
> > 
> > > ## Darek KłeczekTopic Author
> > > 
> > > I'll see if I can reproduce the binarization while keeping ties too. 
> > > 
> > > 
> > > 
> > > ## Darek KłeczekTopic Author
> > > 
> > > Version 2 of the [dataset](https://www.kaggle.com/datasets/thedrcat/llm-human-preference-data-ultrafeedback) has ties between models added now. 
> > > 
> > > 
> > > 
> > > ## Turbo
> > > 
> > > Intersting dataset.
> > > 
> > > Did you use this dataset and boost your score?
> > > 
> > > 
> > > 


---

> ## eli plutchok
> 
> Wouldn't you expect gpt-4 rankings to be very different than human rankings? 
> 
> 
> 
> > ## Darek KłeczekTopic Author
> > 
> > There's research pointing that GPT-4 correlates well with human ratings, for example [here](https://arxiv.org/pdf/2306.05685):
> > 
> > The agreement […] between GPT-4 and humans reaches 85%, which is even higher than the agreement among humans (81%). This means GPT-4’s judgments closely align with the majority of humans.
> > 
> > 
> > 
> > > ## eli plutchok
> > > 
> > > Wow. Have you tested GPT4 on the training examples to see how well it scores?
> > > 
> > > 
> > > 


---

> ## justin1357
> 
> Is any data from kaggle covered in this dataset?
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# 外部データ - 157,000件の追加の人間による好み評価 🔥🔥🔥
**Darek Kłeczek** *2024年5月3日 金曜日 07:09:30 GMT+0900 (日本標準時)* (96票)

より小さなモデル（KaggleのGPUに対応）が、はるかに大きなLLMからの応答を効果的に評価できるかどうか、とても楽しみです。モデルの改善に役立つよう、外部データを含むデータセットを公開しました。
[https://www.kaggle.com/datasets/thedrcat/llm-human-preference-data-ultrafeedback/data](https://www.kaggle.com/datasets/thedrcat/llm-human-preference-data-ultrafeedback/data)
これは、ArgillaによってHFに公開されたUltrafeedbackデータセットに基づいています。さらに、コンペティションのトレーニングデータ形式に変換しました。
編集：Ultrafeedbackは、人間の評価者の代理としてGPT4を判定者として使用していることに注意してください。また、バージョン2では、以前はフィルターされていたモデル間の同点も追加しました。元のデータセットの論文は[こちら](https://arxiv.org/pdf/2310.01377)をご覧ください。 [@nbroad](https://www.kaggle.com/nbroad)さん、指摘していただきありがとうございます。
楽しんでください ❤️🙏👍
---
# 他のユーザーからのコメント
> ## Dlond Mike
> 
> 役に立たない…でも、自分のノートブックのためだけに
> 
> 
> 
---
> ## Rich Olson
> 
> このデータセットから50,000件を自分の「Deberta + TF-IDF + Word2Vec + Length」ノートブックに追加しました（公開されています - リンクを貼りたいのですが、Kaggleはスパムだと考えています）。
> 
> LBで1.011という同一のスコアを得ました。[このデータセット](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/500973)でも同じ経験をしました。
> 
> これは、データがたぶん良い（少なくとも悪いわけではない）という兆候だと考えています - ただ、私のノートブックは追加データから恩恵を受けることができないだけです。
> 
> 
> 
---
> ## Nicholas Broad
> 
> 同点はどのように処理すべきだと思いますか？スコアが同じ場合は、同点になるべきですか？（あなたのデータセットには「モデルa」の勝利しかありません）
> 
> 更新：
> 
> データセットの処理方法について詳しく調べたところ、いくつかのことに気づきました。
> 
> これは人間の好みではないと思います。これは[GPT-4を使用して応答を評価している](https://github.com/OpenBMB/UltraFeedback/tree/main?tab=readme-ov-file#introduction)と思います。
> [Ultrafeedbackは意図的に同点をフィルターアウトしています](https://huggingface.co/datasets/argilla/ultrafeedback-binarized-preferences/blob/main/README.md#dataset-processing)が、LMSYSデータセットでは、モデルaの勝利、bの勝利、同点の割合がほぼ均等に分布しています。
> 
> 
> > ## Darek Kłeczekトピック作成者
> > 
> > 素晴らしい指摘ですね、ありがとうございます！スレッドを更新します。これは、事前トレーニングや疑似ラベル付けに役立つ可能性があります。論文もこちらで見つかりました：[https://arxiv.org/pdf/2310.01377](https://arxiv.org/pdf/2310.01377)
> > 
> > 
> > 
> > > ## Darek Kłeczekトピック作成者
> > > 
> > > 同点も維持しながら、二値化を再現できるかどうか調べてみます。
> > > 
> > > 
> > > 
> > > ## Darek Kłeczekトピック作成者
> > > 
> > > [データセット](https://www.kaggle.com/datasets/thedrcat/llm-human-preference-data-ultrafeedback)のバージョン2では、モデル間の同点が追加されました。
> > > 
> > > 
> > > 
> > > ## Turbo
> > > 
> > > 興味深いデータセットですね。
> > > 
> > > このデータセットを使ってスコアを向上させましたか？
> > > 
> > > 
> > > 
---
> ## eli plutchok
> 
> GPT-4のランキングは、人間のランキングとは大きく異なると思いませんか？
> 
> 
> 
> > ## Darek Kłeczekトピック作成者
> > 
> > GPT-4は人間の評価とよく相関していることを示す研究があります。例えば[こちら](https://arxiv.org/pdf/2306.05685):
> > 
> > GPT-4と人間の合意[…]は85%に達し、これは人間同士の合意（81%）よりも高いです。これは、GPT-4の判断が、大多数の人間の判断とよく一致することを意味します。
> > 
> > 
> > 
> > > ## eli plutchok
> > > 
> > > わお。GPT4をトレーニング例でテストして、スコアがどのくらいになるか確認しましたか？
> > > 
> > > 
> > > 
---
> ## justin1357
> 
> このデータセットには、Kaggleのデータが含まれていますか？
> 
> 
> 
---


</div>