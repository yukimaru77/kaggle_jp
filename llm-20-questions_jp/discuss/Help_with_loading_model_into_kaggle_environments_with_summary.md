# 要約 
このディスカッションは、KaggleのLLM 20 Questionsコンペティションにおいて、参加者であるMatthew S Farmer氏が、ローカルに保存したモデルを提出後の検証フェーズで読み込む方法について質問しているものです。

Matthew氏は、モデル、重み、トークナイザーを提出用tarballに含めて提出しているものの、検証に失敗し続けていると説明しています。彼は、Gemma以外のLLMを試したいと考えており、HFスナップショットの読み込み、Gitリポジトリのクローン作成、公開コードからの手順のコピーなど、さまざまな方法を試したものの、うまくいっていないとのことです。

この質問に対して、Chris Deotte氏は、モデル読み込みに関する手順を説明した別のディスカッションへのリンクを共有しています。Gnidnatsuot氏は、Matthew氏のコードの一部を見せてもらうことを提案しています。

このディスカッションは、Kaggleコンペティションにおけるモデル読み込みに関する問題と、その解決策を探るためのコミュニティの協力的な姿勢を示しています。


---
# Kaggle 環境でのモデル読み込みに関するヘルプ

**Matthew S Farmer** *木曜日 6月 27日 2024 11:22:36 日本標準時* (0 票)

皆さん、こんにちは！

ローカルにモデルを保存して、提出後の検証フェーズで受け入れられるようにしようと、何度も試みましたが、うまくいきません。何かヒントはありますか？

モデル、重み、トークナイザーはすべて、提出ファイルと一緒に提出用 tarball に含まれていますが、検証に失敗し続けています。すでに開始ノートブックで示されている Gemma を使用していますが、他の LLM を試してみたいと思っています。HF スナップショットの読み込み、Git リポジトリのクローン作成、公開コードからの手順のコピーなど、さまざまな方法を試しましたが、うまくいきません。

私が見落としている Kaggle ゲーム環境に関するドキュメントはありますか？

ご協力いただければ幸いです。

よろしくお願いいたします！

---

# 他のユーザーからのコメント

> ## Chris Deotte
> 
> こんにちは。手順を [こちら](https://www.kaggle.com/competitions/llm-20-questions/discussion/513759) で説明しています。
> 
> 
> 
> > ## Matthew S Farmer トピック作成者
> > 
> > Chris、ありがとうございます。
> > 
> > 
> > 
---
> ## Gnidnatsuot
> 
> モデルの読み込みに関するコードの一部を見せていただけますか？
> 
> 
> 
--- 
