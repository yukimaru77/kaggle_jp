# キャリブレーションは重要？

**yechenzhi1** *2024年7月2日 火曜日 19:06:56 JST* (3 votes)
皆さん、こんにちは。

[以前のディスカッション](https://www.kaggle.com/code/valentinwerner/log-loss-what-are-good-scores/notebook)でVALENTIN WERNERが述べたように、適切なキャリブレーションは対数損失スコアを大幅に向上させる可能性があります。温度調整やハードな例に対するバイナリ分類器のトレーニングなど、さまざまなキャリブレーション手法を試してみましたが、満足のいく結果を得ることができませんでした。この問題についてしばらく考えてきました。もしかしたら、アンサンブル手法や新しいモデルの探索など、他の戦略に焦点を移すべきでしょうか？事前に感謝します！

---
# 他のユーザーからのコメント
> ## James Day
> 
> 後処理ステップとして予測をよりよくキャリブレーションしようとしても、成功したことはありません。プラットスケーリング、アイソトニック回帰、モデルスタッキングはすべて、良いよりも悪い影響を与えているようです。
> 
> 少し前にChatGPTは、追加の交差検証指標として「期待キャリブレーション誤差」を計算し、「信頼性ダイアグラム」を生成することで、予測のキャリブレーションがどの程度優れているかを調査することを提案しました。そのためのコードと、私の最高のアンサンブル（0.899 LB）のサンプル結果を以下に示します。自信値は、トップの推測が正しい確率と非常に相関しているように見えるため、後処理ロジックでできることはほとんどありません。私のモデルは、少し自信過剰になる傾向があるのかもしれませんが、推論時にそれを修正しようとした私の最善の試みは、生の予測を使用した場合と0.001（CV）以内のスコアでした。基になるモデルが弱ければ、後処理はより有益になるかもしれません。
> 
> ```
> def compute_ece(predictions, labels, num_bins=25):
>     bin_boundaries = np.linspace(0, 1, num_bins + 1)
>     ece = 0.0
>     total_samples = len(labels)
> 
>     confidences = []
>     accuracies = []
> 
>     for bin_lower, bin_upper in zip(bin_boundaries[:-1], bin_boundaries[1:]):
>         bin_indices = np.where((predictions >= bin_lower) & (predictions < bin_upper))[0]
>         if len(bin_indices) == 0:
>             continue
> 
>         bin_confidence = predictions[bin_indices].max(axis=1).mean()
>         bin_accuracy = (labels[bin_indices] == predictions[bin_indices].argmax(axis=1)).mean()
> 
>         bin_size = len(bin_indices)
>         ece += (bin_size / total_samples) * np.abs(bin_confidence - bin_accuracy)
> 
>         confidences.append(bin_confidence)
>         accuracies.append(bin_accuracy)
> 
>     return ece, confidences, accuracies
> 
> ece, confidences, accuracies = compute_ece(all_predictions, np.array(labels))
> print(f'Expected Calibration Error (ECE): {ece:.4f}')
> 
> from matplotlib import pyplot as plt
> 
> plt.plot([0, 1], [0, 1], linestyle='--')
> plt.scatter(confidences, accuracies, marker='o')
> plt.xlabel('Confidence')
> plt.ylabel('Accuracy')
> plt.title('Reliability Diagram')
> plt.show()
> 
> ```
> 
> 
> 
> > ## Yu Chengzhi
> > 
> > 共有していただきありがとうございます！さまざまな手法をどのようにアンサンブルすればよいですか？単にさまざまなモデルからの確率の平均値ですか？
> > 
> > 
> > 
> > > ## yechenzhi1トピック作成者
> > > 
> > > 各モデルの確率の重みを調整できます。たとえば、preds = 0.8 * model_a_preds + 0.2 * model_b_preds です。
> > > 
> > > 
> > > 
> > ## yechenzhi1トピック作成者
> > 
> > ご回答ありがとうございます！トレーニングプロセスに焦点を当てるか、新しいアイデアを試してみることにします。
> > 
> > 
> > 
---
> ## Valentin Werner
> 
> モデルはすでに損失を最小化しているので、私の経験では、予測の後処理は良い結果をもたらしません。ただし、トランスフォーマーをトレーニングする場合、ラベルスムージングなどのパラメータは、より良いキャリブレーションを実現するのに役立ちます（モデルは基本的に、アルファが0.1など、1.0ではなく0.9を予測するように求められます）。ただし、一般的にデータは混乱しており、これは私のモデルが基本的に0.85を超える予測をほとんどしないという課題の1つです。なぜなら、それほど自信を持つことは非常に難しいからです。
> 
> ディスカッションとリンクされたノートブックを書いたとき、モデルは大きく過剰適合し、一部のクラスを強く支持すると想定していましたが、実際にはそうではありませんでした。
> 
> キャリブレーションは確かに重要ですが、おそらく後処理ではなく、トレーニング中に実行する必要があります。
> 
> 
> 
---


