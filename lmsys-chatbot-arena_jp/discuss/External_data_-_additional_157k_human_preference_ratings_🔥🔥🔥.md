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
