# 20問ゲームの理論的分析
**ISAKA Tsuyoshi** *Sun Jul 14 2024 10:32:45 GMT+0900 (日本標準時)* (8 votes)
皆さん、こんにちは！

20問ゲームの戦略と理論的な勝利確率について、興味深い議論を共有したいと思います。この投稿では、各ラウンドの勝利確率を計算する方法を説明し、さまざまな縮小率に対してプロットした結果を紹介します。

### 背景
20問ゲームは、イエス/ノーの質問を通じてキーワードを特定するゲームです。理論的な勝利確率を計算するために、次の条件を仮定します。

* 各質問の後、候補の数が一定の比率で減少します。
* ゲームは20ラウンドで構成され、各ラウンドでキーワードを推測できます。

### 式と計算方法
N を初期のキーワード数、reduction_factor を各ラウンドで候補の数が減少する比率とします。

ラウンド k における候補の数 Nk は次のように表されます。

```
Nk = N * (reduction_factor ^ k)
```

ラウンド k における勝利確率 Pk は次のように計算されます。

```
Pk = (1 - sum(Pi for i in range(1, k))) * (1 / Nk)
```

累積勝利確率 Ck は次のように表されます。

```
Ck = sum(Pi for i in range(1, k+1))
```

### Python コードによる計算とプロット
次の Python コードは、20問ゲームの各ラウンドの累積勝利確率を計算し、さまざまな縮小率に対して結果をプロットします。

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

グラフは以下のとおりです。

ソースコードは以下に示されています。パラメータを変更して、さまざまなシナリオを探索してみてください！

[https://www.kaggle.com/code/isakatsuyoshi/theoretical-analysis-of-the-20-questions-game](https://www.kaggle.com/code/isakatsuyoshi/theoretical-analysis-of-the-20-questions-game)

### まとめ
この分析は、各ラウンドの質問によってキーワードを特定する確率がどのように変化するかを明確に理解するのに役立ちます。特に、さまざまな縮小率に基づく勝利確率の変化は、効果的な質問戦略を構築するための重要な指標となります。

この議論が役に立てば幸いです。コメントで質問やフィードバックを共有してください！

これで、20問ゲームにおける勝利確率と戦略の理論的分析は終了です。お読みいただきありがとうございました！

