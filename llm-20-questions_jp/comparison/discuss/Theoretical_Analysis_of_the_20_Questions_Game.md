# 要約 
ディスカッションでは、20の質問ゲームにおける戦略と理論的な勝率についての分析が行われており、ISAKA Tsuyoshiさんが主に発表しています。投稿の要点は以下の通りです。

1. **ゲームの背景**:
   - 20の質問ゲームは、はい/いいえの質問を通じて特定のキーワードを当てることを目的とするゲームです。

2. **勝率の計算**:
   - 理論的な勝率を計算するための仮定として、各ラウンドで候補のキーワード数が一定の係数（reduction_factor）で減少することが挙げられています。具体的な公式や計算方法も紹介され、各ラウンドの候補数と勝率の計算が行われています。

3. **Pythonコードの提供**:
   - 勝率を計算し、異なる削減係数に基づいて結果をプロットするためのPythonコードが共有されており、実際のシミュレーションも可能です。また、各ラウンドにおける勝率の累積確率をグラフで示す手法が詳細に説明されています。

4. **結論**:
   - この分析により、キーワード特定の確率がラウンドに応じてどのように変化するかを理解することができ、効果的な質問戦略を構築するための指標としての重要性が強調されています。

最後に、著者は質問やフィードバックを歓迎し、読者がこの分析を活用できることを願っています。

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

# Theoretical Analysis of the 20 Questions Game

**ISAKA Tsuyoshi** *Sun Jul 14 2024 10:32:45 GMT+0900 (日本標準時)* (8 votes)

Hello everyone!

I wanted to share an interesting discussion on the strategy and theoretical winning probability in the 20 Questions game. In this post, I will explain how to calculate the winning probability for each round and present the results plotted for different reduction factors.

### Background

The 20 Questions game involves identifying a keyword through Yes/No questions. To calculate the theoretical winning probability, we assume the following conditions:

The number of candidates decreases by a certain factor after each question.
The game consists of 20 rounds, and the keyword can be guessed in each round.

### Formulas and Calculation Method

Let N be the initial number of keywords, and reduction_factor be the ratio by which the number of candidates decreases in each round.

The number of candidates Nk in round k is given by:

```
Nk = N * (reduction_factor ^ k)

```

The winning probability Pk in round k is calculated as:

```
Pk = (1 - sum(Pi for i in range(1, k))) * (1 / Nk)

```

The cumulative winning probability Ck is:

```
Ck = sum(Pi for i in range(1, k+1))

```

### Calculation and Plotting with Python Code

The following Python code calculates the cumulative winning probability for each round in the 20 Questions game and plots the results for different reduction factors.

```
import matplotlib.pyplot as plt

def calculate_win_probabilities(N: int, rounds: int, reduction_factor: float) -> list[float]:
    cumulative_probabilities = []
    previous_prob = 0

    for k in range(1, rounds + 1):
        Nk = N * (reduction_factor ** k)
        current_prob = (1 - previous_prob) * (1 / Nk)
        previous_prob += current_prob
        if previous_prob > 1:
            previous_prob = 1  # Ensure the winning probability does not exceed 1
        cumulative_probabilities.append(previous_prob)

    return cumulative_probabilities

def plot_cumulative_probabilities(probabilities_dict: dict[float, list[float]]):
    plt.figure(figsize=(12, 8))

    for reduction_factor, probabilities in probabilities_dict.items():
        rounds = range(1, len(probabilities) + 1)
        plt.plot(rounds, probabilities, marker='o', linestyle='-', label=f'Reduction Factor = {reduction_factor}')

    plt.xlabel('Round')
    plt.ylabel('Cumulative Probability of Winning')
    plt.title('Cumulative Probability of Winning per Round for Different Reduction Factors')
    plt.grid(True)
    plt.xticks(range(1, 21))
    plt.yticks([i/10 for i in range(11)])
    plt.ylim(0, 1)
    plt.legend()
    plt.show()

def main():
    N = 1024
    rounds = 20
    reduction_factors = [0.5, 0.6, 0.7, 0.8, 0.9, 1.0]  # Reduction factors ranging from 0.5 to 1.0
    probabilities_dict = {}

    for reduction_factor in reduction_factors:
        probabilities = calculate_win_probabilities(N, rounds, reduction_factor)
        probabilities_dict[reduction_factor] = probabilities
        for i, prob in enumerate(probabilities, 1):
            print(f"Reduction Factor {reduction_factor}, Round {i}: Cumulative probability of winning = {prob:.10f}")

    plot_cumulative_probabilities(probabilities_dict)

if __name__ == "__main__":
    main()

```

The graph is shown below:

The source code is provided below. Feel free to modify the parameters and explore different scenarios!

[https://www.kaggle.com/code/isakatsuyoshi/theoretical-analysis-of-the-20-questions-game](https://www.kaggle.com/code/isakatsuyoshi/theoretical-analysis-of-the-20-questions-game)

### Conclusion

This analysis provides a clear understanding of how the probability of identifying the keyword changes with each round of questions. Notably, the variation in winning probability based on different reduction factors serves as a crucial indicator for building effective questioning strategies.

I hope you find this discussion helpful. Please feel free to share any questions or feedback in the comments!

This concludes my theoretical analysis of winning probability and strategy in the 20 Questions game. Thank you for reading!





</div>
<div class="column-right">

# 日本語訳

# 20の質問ゲームの理論的分析
**ISAKA Tsuyoshi** *2024年7月14日（日）10:32:45 GMT+0900（日本標準時）* (8票)
皆さん、こんにちは！
今回は、20の質問ゲームにおける戦略と理論的勝率についての興味深い議論を共有したいと思います。この投稿では、各ラウンドの勝率の計算方法を説明し、異なる削減係数に基づいてプロットした結果を示します。

### 背景
20の質問ゲームは、はい/いいえの質問を通じてキーワードを特定することを目的としています。理論的な勝率を計算するために、以下の条件を仮定します：
質問の後、候補の数が一定の係数で減少します。
ゲームは20ラウンドから構成され、各ラウンドでキーワードを推測できます。

### 公式と計算方法
Nを初期のキーワード数、reduction_factorを各ラウンドで候補数が減少する比率とします。
ラウンドkにおける候補数Nkは次のように表されます：
```
Nk = N * (reduction_factor ^ k)
```
ラウンドkにおける勝率Pkは以下のように計算されます：
```
Pk = (1 - sum(Pi for i in range(1, k))) * (1 / Nk)
```
累積勝率Ckは次の通りです：
```
Ck = sum(Pi for i in range(1, k+1))
```

### 計算とプロットのためのPythonコード
以下のPythonコードは、20の質問ゲームの各ラウンドにおける累積勝率を計算し、異なる削減係数に基づいた結果をプロットします。
```python
import matplotlib.pyplot as plt
def calculate_win_probabilities(N: int, rounds: int, reduction_factor: float) -> list[float]:
    cumulative_probabilities = []
    previous_prob = 0
    for k in range(1, rounds + 1):
        Nk = N * (reduction_factor ** k)
        current_prob = (1 - previous_prob) * (1 / Nk)
        previous_prob += current_prob
        if previous_prob > 1:
            previous_prob = 1  # 勝率が1を超えないようにする
        cumulative_probabilities.append(previous_prob)
    return cumulative_probabilities

def plot_cumulative_probabilities(probabilities_dict: dict[float, list[float]]):
    plt.figure(figsize=(12, 8))
    for reduction_factor, probabilities in probabilities_dict.items():
        rounds = range(1, len(probabilities) + 1)
        plt.plot(rounds, probabilities, marker='o', linestyle='-', label=f'削減係数 = {reduction_factor}')
    plt.xlabel('ラウンド')
    plt.ylabel('勝率の累積確率')
    plt.title('異なる削減係数におけるラウンド毎の勝率の累積確率')
    plt.grid(True)
    plt.xticks(range(1, 21))
    plt.yticks([i/10 for i in range(11)])
    plt.ylim(0, 1)
    plt.legend()
    plt.show()

def main():
    N = 1024
    rounds = 20
    reduction_factors = [0.5, 0.6, 0.7, 0.8, 0.9, 1.0]  # 0.5から1.0までの削減係数
    probabilities_dict = {}
    for reduction_factor in reduction_factors:
        probabilities = calculate_win_probabilities(N, rounds, reduction_factor)
        probabilities_dict[reduction_factor] = probabilities
        for i, prob in enumerate(probabilities, 1):
            print(f"削減係数 {reduction_factor}, ラウンド {i}: 勝率の累積確率 = {prob:.10f}")
    plot_cumulative_probabilities(probabilities_dict)

if __name__ == "__main__":
    main()
```
以下にグラフが示されています：
ソースコードは以下に提供されていますので、パラメータを変更してさまざまなシナリオを探索してください！  
[https://www.kaggle.com/code/isakatsuyoshi/theoretical-analysis-of-the-20-questions-game](https://www.kaggle.com/code/isakatsuyoshi/theoretical-analysis-of-the-20-questions-game)

### 結論
この分析は、キーワード特定の確率が質問のラウンドに応じてどのように変化するかについての明確な理解を提供します。特に、さまざまな削減係数に基づく勝率の変動は、効果的な質問戦略を構築するための重要な指標として機能します。

この議論が役に立つことを願っています。質問やフィードバックがあれば、コメントでお気軽にお知らせください！
これで、20の質問ゲームにおける勝率と戦略の理論的分析は終了です。お読みいただきありがとうございます！


</div>