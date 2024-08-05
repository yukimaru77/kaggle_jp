# [考察] 165k データセットとモデルのパフォーマンスについて

**justin1357** *2024年8月1日 木曜日 20:21:38 JST* (39票)

過去2日間、3ヶ月前にディスカッションエリアで提案された165kデータセットをトレーニングパイプラインに統合しようと試みました。しかし、この試みはリーダーボードで失敗に終わりました。そこで、このデータセットの情報について慎重に検討しました。

重複排除: 165kデータセットと55kのKaggleデータセットに対して、プロンプトと応答レベルで重複排除を行いました。有意な重複は見つかりませんでした。これは、パフォーマンスの低下が重複データによる過剰適合が原因ではないことを示しています。

データソース分析: 技術的な問題を排除した後、データのソースを調べました。多くの人がこのデータセットがUltraFeedbackから来ていることを知っています。しかし、ほとんどの人が知らないのは、プロンプトは人間が生成したものではなく、UltraChat、ShareGPT、Evol-Instruct、TruthfulQA、FalseQA、FLANなどのさまざまな評価データセットから取得されていることです。これがパフォーマンス低下の一番の理由だと考えています。Chatbot Arenaから収集された人間のプロンプトの分布は、専門的な評価データセットのプロンプトとは大きく異なり、モデルを誤った方向に導いています。

モデルパフォーマンスの説明: これは、さまざまな評価データセットで非常に優れたパフォーマンスを発揮したにもかかわらず、このコンペティションではうまくいかなかったLLama-3.1の理由も説明しています。LLama-3.1はDPO（Direct Preference Optimization）を使用しており、本質的に専門的な評価プロンプトに「過剰適合」しています。しかし、これらはChatBot Arenaによって収集されたプロンプトの分布とは異なり、応答を評価するための基準が異なります。

成功したモデル分析: これは、Gemma-2やLLama-3などのモデルがこのコンペティションで良好な成績を収めた理由も説明しています。これらは、トレーニング後の段階で共通の特徴を共有しています。RLHF（人間のフィードバックからの強化学習）を使用しています。この方法は、DPOなどの自動学習方法と比較してコストがかかりますが、実際の人間のプロンプトの分布に合致しており、モデルは実際の人間のプロンプトをよりよく理解することができます。

テスト結果: UltraFeedbackデータセットでDPOまたはSimPOで微調整されたGemma-2モデルをいくつかテストしましたが、パフォーマンスは不十分でした。これは、DPOのような方法の問題を間接的に反映しています。

これらの考察が皆様のお役に立てれば幸いです。この回答が役に立ったと感じたら、ぜひ投票をお願いします。
---
 # 他のユーザーからのコメント
> ## xiaotingting
> 
> はい、このコンペティションにおけるデータの処理は、後期のスコア向上のための重要なポイントになる可能性を感じます。
> 
> 
> 
---
