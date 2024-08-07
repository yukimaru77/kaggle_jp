# 要約 
このディスカッションは、Chatbot Arena と呼ばれる、人間の好みを基にした大規模言語モデル (LLM) の評価のための新しいプラットフォームについて議論しています。このプラットフォームは、ユーザーが 2 つの LLM と対話して、どちらの応答を好むかを投票できるようにすることで機能します。

ディスカッションでは、Chatbot Arena のデータセットと、そのデータセットを使用して LLM のパフォーマンスを評価する方法について説明しています。特に、Bradley-Terry モデルを使用して LLM の Elo レーティングを計算する方法について説明しています。

ディスカッションの主なポイントは次のとおりです。

* **Chatbot Arena は、LLM のパフォーマンスを評価するための新しいプラットフォームです。** このプラットフォームは、人間の好みを基にしたライブ評価を提供します。
* **Chatbot Arena のデータセットは、LLM のパフォーマンスを評価するために使用できます。** データセットには、ユーザーと 2 つの LLM 間の複数回の会話と、ユーザーがどちらのモデルを好むかを示す投票が含まれています。
* **Bradley-Terry モデルを使用して、LLM の Elo レーティングを計算できます。** Elo レーティングは、プレイヤーの相対的なスキルレベルを計算する方法です。
* **Chatbot Arena のプロンプトは、モデルを識別するのに役立ちます。** これは、モデルがさまざまな分野で異なる強みを示す可能性があるためです。

ディスカッションでは、Chatbot Arena のデータセットと Elo レーティングの計算方法について、いくつかの追加情報も提供されています。たとえば、データセットには 50 以上のモデルが含まれており、会話は 100 以上の言語をカバーしています。また、Elo レーティングを計算するためのさまざまな方法も説明されています。

全体として、このディスカッションは、Chatbot Arena と、人間の好みを基にした LLM の評価について、有益な洞察を提供しています。


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

# ChatBot Arena Prompts Can Distinguish Models. The Bradley-Terry model. Elo Ratings on Kaggle.

**Marília Prata** *Fri May 03 2024 14:27:26 GMT+0900 (日本標準時)* (42 votes)

# ChatBot Arena

Super cool Notebook Chatbot Arena MLE Elo Rating

[Chatbot Arena: MLE Elo Rating (Bradley-Terry model) Calculation (Apr 22, 2024)](#https://colab.research.google.com/drive/1KdwokPjirkTmpO_P1WByFNFiqxWQquwH#scrollTo=B_PYA7oVyaHO)

"Maximum Likelihood Estimation for Elo Ratings (aka Bradley-Terry model). In the context of LLM evaluation, models can be assumed to be static. In this case, the authors could directly fit the ratings by maximum likelihood estimation method (aka Bradley-Terry model), which produce significantly stable ratings. Here they provided an implementation with logistic regression."

[https://colab.research.google.com/drive/1KdwokPjirkTmpO_P1WByFNFiqxWQquwH#scrollTo=PbTdhkLQp113](https://colab.research.google.com/drive/1KdwokPjirkTmpO_P1WByFNFiqxWQquwH#scrollTo=PbTdhkLQp113)

# Chatbot Arena: An Open Platform for Evaluating LLMs by Human Preference

Authors: Wei-Lin Chiang, Lianmin Zheng, Ying Sheng, Anastasios N. Angelopoulos, Tianle Li, Dacheng Li, Banghua Zhu, HaoZhang, Michael I. Jordan, Joseph E. Gonzalez, Ion Stoica.

"To assess the performance of LLMs, the research community has introduced a variety of benchmarks. These benchmarks can be categorized based on two factors: the source of questions (either static or live) and the evaluation metric (either ground truth or human preference). According to these fac tors, benchmarks can be classified into four categories. While a range of benchmarks is beneficial, the most prevalent current method for evaluating LLMs remains a static, ground-truth-based evaluation, partly because such evaluations are inexpensive and reproducible."

"However, these static, ground-truth-based benchmarks exhibit several limitations. Firstly, the questions within these benchmarks are not open-ended, hindering the ability to capture the flexible and interactive use found in real-world settings. Secondly, the test sets in these benchmarks are static, meaning they can become contaminated over time, which undermines the reliability of the evaluation results. Furthermore,for many complex tasks, establishing a definitive ground truth is not only challenging but sometimes unattainable."

" Consequently, current benchmarks fail to adequately address the needs of state-of-the-art LLMs, particularly in evaluating user preferences. Thus, there is an urgent necessity for an open, live evaluation platform based on human preference that can more accurately mirror real-world usage."

"Creating such a benchmark platform entails significant challenges. It requires the collection of live, fresh, and diverse user questions to accurately represent real-world scenarios."

CONTRIBUTIONS MADE by the AUTHORS:

"They built the first large-scale crowd-sourced live LLM evaluation platform with over 1M users visit."

"They conducted an in-depth analysis of the collected data, including prompt diversity, quality, vote quality, and insights on human feedback."

"They will publicly release a human preference dataset with over 100K pairwise votes collected from Chatbot Arena."

"They designed an efficient sampling algorithm that actively chooses which model pairs to show, such that our sample efficiency improves, sometimes to a large degree."

# Risks of Static Benchmarks.

"Static benchmarks have certain issues, including contamination, saturation, overfitting, and a lack of human alignment. DynaBench identifies these challenges and recommends the use of a live benchmark that incorporates a human-in-the-loop approach for classical NLP benchmarks. Their system adopts a similar spirit."

DATA STATISTICS 

"The authors began collecting data in April 2023. As of Jan 2024, they have received around 240K votes from over 90K users. Their data involves more than 50 models, including both proprietary models like GPT-4, Claude, and Gemini, as well as open models such as LLaMA and Mistral. These conversations cover more than 100 languages, with 77% being in English, 5% in Chinese, and the remaining languages, such as Russian, German, Spanish, French, and Japanese, each representing less than 2% of the total. Each data point includes multi-turn conversations between the user and two LLMs, and a vote to indicate which model the user prefers."

# Can Arena Prompts Distinguish Models?

"The authors studied how effective are these topic clusters in distinguishing models strengths. Their result shows models may exhibit varying strengths in different areas, but also highlights some of the topic clusters in Chatbot Arena are effective in differentiate models."

[https://arxiv.org/pdf/2403.04132](https://arxiv.org/pdf/2403.04132)

# Elo Ratings

Remember that it is "Elo", not "ELO" since it was named after Arpad Elo. The USCF implemented Arpad Elo's suggestions in 1960, and the system quickly gained recognition as being both fairer and more accurate than the Harkness rating system.

[Elo rating system](https://en.wikipedia.org/wiki/Elo_rating_system)

"The Elo rating system is a method for calculating the relative skill levels of players, which has been widely adopted in chess and other competitive games. The difference in the ratings between two players serves as a predictor of the outcome of a match. The Elo rating system works well for our case because we have multiple models and we run pairwise battles between them. In this section, we present different methods for calculating Elo ratings."

Compute Ratings

"The authors first use the online linear update algorithm to compute Elo ratings. They chose a small K-factor of 4 to make the Elo ratings more stable and less biased towards recent games."

[https://colab.research.google.com/drive/1KdwokPjirkTmpO_P1WByFNFiqxWQquwH#scrollTo=B_PYA7oVyaHO](https://colab.research.google.com/drive/1KdwokPjirkTmpO_P1WByFNFiqxWQquwH#scrollTo=B_PYA7oVyaHO)

# Elo Ratings on Kaggle

KAGGLE TOPICS:

[Intro to Rating Systems](https://www.kaggle.com/competitions/chess/discussion/92) By Jeff Sonas - 14 y ago

[Elo Ratings Shiny App for Euro Soccer Teams](https://www.kaggle.com/datasets/hugomathien/soccer/discussion/31154) By Kevin Pan - 8 y ago

[Elo RATING ALGORITHM](https://www.kaggle.com/discussions/getting-started/216048) By Kaushik Deb

KAGGLE NOTEBOOKS:

[Elo Ratings in Python](https://www.kaggle.com/code/kplauritzen/elo-ratings-in-python) By Kasper P. Lauritzen

[Simple Simulation & Elo Rating Approach](https://www.kaggle.com/code/kenjee/simple-simulation-elo-rating-approach) By Ken Jee

[Custom Football Elo Rating](https://www.kaggle.com/code/thomasstokes/custom-football-elo-rating) By Thomas Stokes

There are many more on Kaggle. I've just picked a few to exemplify. Therefore, search by Code or Discussion if you intend to read more material.





</div>
<div class="column-right">

# 日本語訳

# ChatBot Arena のプロンプトはモデルを識別できる。Bradley-Terry モデル。Kaggle での Elo レーティング。

**Marília Prata** *2024年5月3日 金曜日 14:27:26 GMT+0900 (日本標準時)* (42 票)

# ChatBot Arena
とてもクールなノートブック Chatbot Arena MLE Elo レーティング
[Chatbot Arena: MLE Elo レーティング (Bradley-Terry モデル) 計算 (2024年4月22日)](#https://colab.research.google.com/drive/1KdwokPjirkTmpO_P1WByFNFiqxWQquwH#scrollTo=B_PYA7oVyaHO)
"Elo レーティングの最尤推定 (Bradley-Terry モデルとも呼ばれます)。LLM 評価の文脈では、モデルは静的であると仮定できます。この場合、著者は最尤推定法 (Bradley-Terry モデルとも呼ばれます) によってレーティングを直接適合させることができ、これは非常に安定したレーティングを生み出します。ここでは、ロジスティック回帰を使用した実装を提供しています。"
[https://colab.research.google.com/drive/1KdwokPjirkTmpO_P1WByFNFiqxWQquwH#scrollTo=PbTdhkLQp113](https://colab.research.google.com/drive/1KdwokPjirkTmpO_P1WByFNFiqxWQquwH#scrollTo=PbTdhkLQp113)

# Chatbot Arena: 人間の好みによる LLM 評価のためのオープンなプラットフォーム
著者: Wei-Lin Chiang、Lianmin Zheng、Ying Sheng、Anastasios N. Angelopoulos、Tianle Li、Dacheng Li、Banghua Zhu、HaoZhang、Michael I. Jordan、Joseph E. Gonzalez、Ion Stoica。
"LLM のパフォーマンスを評価するために、研究コミュニティはさまざまなベンチマークを導入してきました。これらのベンチマークは、質問のソース (静的またはライブ) と評価指標 (真値または人間の好み) の 2 つの要素に基づいて分類できます。これらの要素に基づいて、ベンチマークは 4 つのカテゴリに分類できます。さまざまなベンチマークは有益ですが、LLM を評価するための現在の最も一般的な方法は、静的な真値ベースの評価であり、これは部分的には、このような評価が安価で再現性があるためです。"
"しかし、これらの静的な真値ベースのベンチマークには、いくつかの制限があります。第一に、これらのベンチマーク内の質問はオープンエンドではなく、現実世界の状況で見られる柔軟でインタラクティブな使用を捉える能力を阻害します。第二に、これらのベンチマークのテストセットは静的であり、つまり時間の経過とともに汚染される可能性があり、評価結果の信頼性を損ないます。さらに、多くの複雑なタスクでは、決定的な真値を確立することは、困難であるだけでなく、場合によっては不可能です。"
"その結果、現在のベンチマークは、特にユーザーの好みを評価する際に、最先端の LLM のニーズを十分に満たしていません。したがって、現実世界の使用状況をより正確に反映できる、人間の好みを基にしたオープンなライブ評価プラットフォームの緊急の必要性があります。"
"このようなベンチマークプラットフォームを作成するには、現実世界のシナリオを正確に表現するために、ライブで新鮮で多様なユーザーの質問を収集する必要があります。"
著者が行った貢献:
"彼らは、100 万人以上のユーザーが訪れた、大規模なクラウドソーシングされたライブ LLM 評価プラットフォームを初めて構築しました。"
"彼らは、プロンプトの多様性、品質、投票の品質、人間のフィードバックに関する洞察など、収集されたデータの詳細な分析を行いました。"
"彼らは、Chatbot Arena から収集された 10 万件以上のペアワイズ投票を含む、人間の好みに関するデータセットを公開します。"
"彼らは、どのモデルペアを表示するかを積極的に選択する効率的なサンプリングアルゴリズムを設計しました。これにより、サンプル効率が向上し、場合によっては大幅に改善されます。"

# 静的ベンチマークのリスク。
"静的ベンチマークには、汚染、飽和、過剰適合、人間の整合性の欠如など、特定の問題があります。DynaBench はこれらの課題を特定し、古典的な NLP ベンチマークのために人間のループアプローチを組み込んだライブベンチマークの使用を推奨しています。彼らのシステムは、同様の精神を採用しています。"

データ統計
"著者は 2023 年 4 月にデータの収集を開始しました。2024 年 1 月現在、彼らは 9 万人以上のユーザーから約 24 万票を受け取っています。彼らのデータには、GPT-4、Claude、Gemini などの独自のモデルと、LLaMA や Mistral などのオープンモデルを含む 50 以上のモデルが含まれています。これらの会話は 100 以上の言語をカバーしており、77% が英語、5% が中国語、残りの言語 (ロシア語、ドイツ語、スペイン語、フランス語、日本語など) はそれぞれ 2% 未満です。各データポイントは、ユーザーと 2 つの LLM 間の複数回の会話と、ユーザーがどちらのモデルを好むかを示す投票を含みます。"

# Arena のプロンプトはモデルを識別できるか?
"著者は、これらのトピッククラスターがモデルの強みを識別する上でどの程度効果的かを調査しました。彼らの結果は、モデルはさまざまな分野で異なる強みを示す可能性がありますが、Chatbot Arena の一部のトピッククラスターはモデルを区別する上で効果的であることも示しています。"
[https://arxiv.org/pdf/2403.04132](https://arxiv.org/pdf/2403.04132)

# Elo レーティング
これは「Elo」であり、「ELO」ではありません。これは、アーパッド・エロにちなんで名付けられたからです。USCF は 1960 年にアーパッド・エロの提案を実装し、このシステムはすぐに、ハーケネス評価システムよりも公正で正確であると認められました。
[Elo レーティングシステム](https://en.wikipedia.org/wiki/Elo_rating_system)
"Elo レーティングシステムは、チェスやその他の競技ゲームで広く採用されている、プレイヤーの相対的なスキルレベルを計算する方法です。2 人のプレイヤー間のレーティングの差は、試合の結果の予測因子として機能します。Elo レーティングシステムは、複数のモデルがあり、それらの間でペアワイズのバトルを実行するため、私たちのケースに適しています。このセクションでは、Elo レーティングを計算するためのさまざまな方法を紹介します。"

レーティングの計算
"著者は最初に、オンライン線形更新アルゴリズムを使用して Elo レーティングを計算します。彼らは、Elo レーティングをより安定させ、最近のゲームに偏らないように、4 の小さな K ファクターを選択しました。"
[https://colab.research.google.com/drive/1KdwokPjirkTmpO_P1WByFNFiqxWQquwH#scrollTo=B_PYA7oVyaHO](https://colab.research.google.com/drive/1KdwokPjirkTmpO_P1WByFNFiqxWQquwH#scrollTo=B_PYA7oVyaHO)

# Kaggle での Elo レーティング
KAGGLE トピック:
[レーティングシステム入門](https://www.kaggle.com/competitions/chess/discussion/92) Jeff Sonas 著 - 14 年前
[ヨーロッパサッカーチームの Elo レーティング Shiny アプリ](https://www.kaggle.com/datasets/hugomathien/soccer/discussion/31154) Kevin Pan 著 - 8 年前
[Elo レーティングアルゴリズム](https://www.kaggle.com/discussions/getting-started/216048) Kaushik Deb 著
KAGGLE ノートブック:
[Python での Elo レーティング](https://www.kaggle.com/code/kplauritzen/elo-ratings-in-python) Kasper P. Lauritzen 著
[単純なシミュレーションと Elo レーティングアプローチ](https://www.kaggle.com/code/kenjee/simple-simulation-elo-rating-approach) Ken Jee 著
[カスタムフットボール Elo レーティング](https://www.kaggle.com/code/thomasstokes/custom-football-elo-rating) Thomas Stokes 著
Kaggle には他にもたくさんあります。私は単に例としていくつかを選びました。したがって、さらに多くの資料を読みたい場合は、コードまたはディスカッションで検索してください。



</div>