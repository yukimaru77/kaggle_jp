# 要約 
ディスカッションでは、Etienne Kaiserがコンペティションに向けたアイデアを共有しています。以下が要約です。

### 理論的手法
- **決定木**を用いて、「はい/いいえ」質問を基に可能な答えを絞り込む。
- **マルコフ決定過程 (MDP)** により、累積報酬を最大化する意思決定のプロセスを形成。
- **LLM**は詳細に進みすぎる可能性があるため、初期質問を大まかなカテゴリー（例: 車両、果物、動物）に絞り込む方針。
- 複数の手法を組み合わせ、強力な一般化エージェントを構築する。

### 統合戦略
- **語彙リスト**を作成し、可能性のある単語をリストアップ。
- **質問データベース**を構築し、事前に定義した質問を準備。
- **ポリシー最適化**に強化学習アルゴリズムを利用し、質問ポリシーを報酬に基づいて最適化。
- 探索と活用のバランスを取り、状況に応じて調整する。

### 追加の考え
- 具体的な質問は不確実性を減少させるが、初期段階での詳細な質問は無関係な情報を掴むリスクがあるため注意が必要。

他の利用者からも、初期のアイデアに対する支持と感謝のコメントが寄せられています。参加者たちはこのテーマに興味を持ち、ディスカッションを続けています。

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

# Starting ideas: LLM, MDP, Decision-Trees & Optimizations

**Etienne Kaiser (郑翊天）** *Thu May 16 2024 22:05:22 GMT+0900 (日本標準時)* (15 votes)

Currently I'm more in this domain than ever, unfortunately I have no time to touch this gem, that's why I spread my ideas where I might would start:

## Theoretical Methods

- Decision Tree - as it is binary and helps in systematically narrowing down the possible answers based on yes/no questions.

- Markov Decision Process (MDP) - Provides the framework for making the sequence of decisions to maximize cumulative (even it's not the classical immediate) reward. 

- LLM - Using directly LLM from the first questions on (from max 20) could also have disadvantages. It might be to detailed, as LLM tend to go in depth first. My first thought was trying to create a decision trees that categorize roughly (like "Vehicle", "Fruits", "Animal" etc..) to narrow down first, in the first 3 questions for instance.

- Combine them! - I think that a combination over a row of experiments will make up a strong generalized agent for the long run.

## Integration Strategy

- Vocabulary List - List of possible words (historical data) that can be guessed.

- Questions Database - Predefined list of yes/no questions.

- Policy Optimization - Use a reinforcement learning algorithm (e.g. Q-learning) to optimize the question-asking policy based on the rewards. Experiment with greedy (off-policy) or on-policy.

- Exploration - Make use of gamma and alpha over time. Dynamically adjust the exploration-exploitation trade-off based on the confidence in its current policy and the remaining time in the game. (as it is limited). Keep in mind that agents must strike a balance between exploring new possibilities (exploration) and exploiting existing knowledge (exploitation). Early in the game, exploration tends to be more beneficial to gather information about the possibilities. Later, exploitation becomes more important to narrow down the remaining options.

## Extra thought

- Depth vs. Width - Going into depth with specific questions can be effective if it leads to significant reductions in uncertainty. However, being to specific too early may also risk wasting questions on irrelevant details or outliers (Should make sense).

I'm open to any feedback to discuss further thoughts, even it increases the chance to get dragged into this competition even more - the curse of time. ;) 

Have fun everyone!



---

 # Comments from other users

> ## Aditya Anil
> 
> Thanks for this, seems like a very nice place to start :) 
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# アイデアのスタート: LLM、MDP、決定木と最適化
**Etienne Kaiser (郑翊天）** *2024年5月16日 22:05:22 JST* (15票)
現在、私はこの分野にこれまで以上に取り組んでいますが、残念ながらこの素晴らしいテーマにじっくり時間をかけることができません。そのため、始めるべきアイデアをここに共有します。

## 理論的手法
- 決定木 - 二項の構造を持ち、「はい/いいえ」質問に基づいて可能な答えを体系的に絞り込むのに役立ちます。
- マルコフ決定過程 (MDP) - 累積報酬を最大化するための意思決定の連鎖を作成するためのフレームワークを提供します（従来の即時報酬ではなくても）。
- LLM - 最初の質問から（最大20）直接LLMを使用することにはデメリットがあるかもしれません。LLMは、詳細に進む傾向があるため、あまりにも詳細になり過ぎる可能性があります。私の初めの考えは、「車両」、「果物」、「動物」などの大まかなカテゴリに分ける決定木を作成し、最初の3つの質問でまず絞り込むことです。
- 組み合わせ - 一連の実験を通じて、長期的に強力な一般化エージェントを構築すると考えています。

## 統合戦略
- 語彙リスト - 推測できる可能性のある単語のリスト（履歴データ）。
- 質問データベース - 猜疑的な「はい/いいえ」の質問の事前定義リスト。
- ポリシー最適化 - 報酬に基づいて質問するポリシーを最適化するために強化学習アルゴリズム（例: Q学習）を利用します。貪欲（オフポリシー）またはオンポリシーで実験します。
- 探索 - 時間が限られているため、時間に伴ってガンマとアルファを動的に調整し、探索と活用のトレードオフを調整します。エージェントは新しい可能性を探る探索と、既存の知識を活用する活用のバランスを取る必要があります。ゲーム初期には、可能性について情報を集めるために探索が有益であり、後半には残っている選択肢を絞るために活用が重要になります。

## 追加の考え
- 深さと幅 - 特定の質問に深く入ることは、不確実性を著しく減少させる場合に効果的ですが、早すぎる段階であまりにも具体的になり過ぎると、無関係な詳細や外れ値に対して質問を浪費するリスクもあります（理解できますよね）。

追加の意見やフィードバックを大歓迎です。これにより、このコンペティションに更に引き込まれる可能性が高まるかもしれませんが、それもまた時間の呪いですね。参加者の皆さん、楽しんでください！

---
# 他のユーザーからのコメント
> ## Aditya Anil
> 
> ありがとう、非常に良い出発点のようですね :) 
> 
> ---


</div>