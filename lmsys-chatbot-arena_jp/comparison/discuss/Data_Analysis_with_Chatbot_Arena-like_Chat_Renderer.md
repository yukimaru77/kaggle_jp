# 要約 
このディスカッションは、KaggleのLMSYS - Chatbot Arena Human Preference Predictionsコンペティションに参加しているAbaoJiangさんによるものです。彼は、コンペティションのデータ分析を支援するために、チャットボットアリーナ風のUIを持つシンプルな静的チャットレンダラーを作成しました。このレンダラーは、2つのモデルからの応答を並べて比較できるようにすることで、データ分析をより容易にします。

レンダラーは、マークダウンレンダリング、Unicodeレンダリング、勝者の表示などの機能をサポートしています。また、AbaoJiangさんは、公式論文にある勝率と対戦回数のヒートマップも実装しました。これにより、頻繁に出現するモデルペアと、どのモデルがより高い勝率を持っているかを視覚的に確認することができます。

AbaoJiangさんは、このレンダラーがコンペティション参加者にとって役立つことを期待しており、今後も分析と洞察を共有していく予定です。

Hafiz Noumanさんは、AbaoJiangさんのレンダラーを称賛し、自身のデータセットを改善するための提案を求めています。


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

# Data Analysis with Chatbot Arena-like Chat Renderer

**AbaoJiang** *Mon May 27 2024 17:00:34 GMT+0900 (日本標準時)* (8 votes)

Hi everyone,

This is the first time I join an NLP competition. I'm so excited because I need to learn everything from scratch! The very first step is to analyze the data. To facilitate model comparison side by side, instead of scrolling up and down to analyze responses from two models, I write a simple static chat renderer with Chatbot Arena-like UI (co-author by ChatGPT). Following is a screenshot of one chat,

[](https://postimg.cc/Tyyhq5RC)

This renderer supports,

Pair comparison between responses from two models.
Markdown rendering powered by [<md-block>](https://md-block.verou.me/).
- e.g., strong and italic fonts, unordered and ordered lists, etc.

Unicode rendering.
- Characters like emojis can be shown.

[](https://postimg.cc/VdffWZ1K)

Also, winner is displayed at the bottom! I hope this can make raw text analysis more handy.

In addition, I also implement the win rate and battle count heatmaps in [the official paper](https://arxiv.org/pdf/2403.04132). We can use this to find frequent model pairs (i.e., battle counts) and which model has the higher win rate (e.g., gpt-4-1106-preview has only 17.42% lose rate).

[](https://postimg.cc/ThswTMDB)

For detailed implementation, please refer to [LMSYS - Detailed EDA](https://www.kaggle.com/code/abaojiang/lmsys-detailed-eda/notebook).

I'll share more analysis and insights during this interesting learning journey. Hope you like it!



---

 # Comments from other users

> ## Hafiz Nouman
> 
> Amazing Improvement keep it up 
> 
> Review my dataset and give some suggestions on it how I can improve my work
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# チャットボットアリーナ風チャットレンダラーを用いたデータ分析
**AbaoJiang** *2024年5月27日 月曜日 17:00:34 GMT+0900 (日本標準時)* (8票)

皆さん、こんにちは！

NLPコンペティションに初めて参加します。すべてをゼロから学ばなければならないので、とても興奮しています！ 最初のステップはデータ分析です。2つのモデルからの応答を分析するために、上下にスクロールするのではなく、モデルを並べて比較できるように、チャットボットアリーナ風のUIを持つシンプルな静的チャットレンダラーを作成しました（ChatGPTとの共同作成）。以下は、チャットのスクリーンショットです。

[](https://postimg.cc/Tyyhq5RC)

このレンダラーは、以下の機能をサポートしています。

* 2つのモデルからの応答のペア比較
* [<md-block>](https://md-block.verou.me/) を使用したマークダウンレンダリング
    * 例：太字と斜体フォント、箇条書きと番号付きリストなど
* Unicodeレンダリング
    * 絵文字などの文字を表示できます。
[](https://postimg.cc/VdffWZ1K)

また、下部に勝者が表示されます！ これにより、生のテキスト分析がより便利になることを願っています。

さらに、[公式論文](https://arxiv.org/pdf/2403.04132) にある勝率と対戦回数のヒートマップも実装しました。これを使用して、頻繁に出現するモデルペア（つまり、対戦回数）と、どのモデルがより高い勝率を持っているか（例：gpt-4-1106-previewは敗北率がわずか17.42%）を見つけることができます。

[](https://postimg.cc/ThswTMDB)

詳細な実装については、[LMSYS - 詳細なEDA](https://www.kaggle.com/code/abaojiang/lmsys-detailed-eda/notebook) を参照してください。

この興味深い学習の旅の中で、さらに分析と洞察を共有していきます。気に入っていただければ幸いです！

---
# 他のユーザーからのコメント
> ## Hafiz Nouman
> 
> 素晴らしい改善ですね！ 頑張ってください！
> 
> 私のデータセットを見直して、どのように改善できるか、いくつか提案をいただけませんか？
> 
> 
> 
---



</div>