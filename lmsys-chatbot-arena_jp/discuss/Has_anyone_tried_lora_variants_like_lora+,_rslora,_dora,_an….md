# LoRAのバリエーション（LoRA+、RSLoRA、DoRAなど）を試した人はいますか？最新のLoRA-GA、LoRA-Proは効果がありますか？
**ShelterW** *2024年7月30日 火曜日 04:27:50 GMT+0900 (日本標準時)* (10 votes)

これらのバリエーションは、フルファインチューニングに近いと聞いています。このコンペティションで試した人はいますか？私はDoRAを試しましたが、従来のLoRAと変わらない結果でした。

### 参考文献:
[1] LoRA: Hu, E. J., Shen, Y., Wallis, P., Allen-Zhu, Z., Li, Y., Wang, S., … & Chen, W. (2021). Lora: Low-rank adaptation of large language models. arXiv preprint arXiv:2106.09685.
[2] LoRA+: Hayou, S., Ghosh, N., & Yu, B. (2024). LoRA+: Efficient Low Rank Adaptation of Large Models. arXiv preprint arXiv:2402.12354.
[3] VeRA: Kopiczko, D. J., Blankevoort, T., & Asano, Y. M. (2023). Vera: Vector-based random matrix adaptation. arXiv preprint arXiv:2310.11454.
[4] LoRA-FA: Zhang, L., Zhang, L., Shi, S., Chu, X., & Li, B. (2023). Lora-fa: Memory-efficient low-rank adaptation for large language models fine-tuning. arXiv preprint arXiv:2308.03303.
[5] LoRA-drop: Zhou, H., Lu, X., Xu, W., Zhu, C., & Zhao, T. (2024). LoRA-drop: Efficient LoRA Parameter Pruning based on Output Evaluation. arXiv preprint arXiv:2402.07721.
[6] AdaLoRA: Zhang, Q., Chen, M., Bukharin, A., He, P., Cheng, Y., Chen, W., & Zhao, T. (2023). Adaptive budget allocation for parameter-efficient fine-tuning. arXiv preprint arXiv:2303.10512.
[7] DoRA: Liu, S. Y., Wang, C. Y., Yin, H., Molchanov, P., Wang, Y. C. F., Cheng, K. T., & Chen, M. H. (2024). DoRA: Weight-Decomposed Low-Rank Adaptation. arXiv preprint arXiv:2402.09353.
[8] Delta-LoRA: Zi, B., Qi, X., Wang, L., Wang, J., Wong, K. F., & Zhang, L. (2023). Delta-lora: Fine-tuning high-rank parameters with the delta of low-rank matrices. arXiv preprint arXiv:2309.02411.
[9] LoRA-GA: Wang, S., Yu, L., & Li, J. (2024). LoRA-GA: Low-Rank Adaptation with Gradient Approximation. arXiv preprint arXiv:2407.05000.
[10] LoRA-Pro: Wang, Z., & Liang, J. (2024). LoRA-Pro: Are Low-Rank Adapters Properly Optimized?. arXiv preprint arXiv:2407.18242.
---
# 他のユーザーからのコメント
> ## James Day
> 
> いくつか試してみましたが、効果はわずかでした。
> 
> - LoRA+ - トレーニングの初期段階では収束が速いように見えましたが、数万件のサンプルを処理した後、差はなくなりました（同じように良いモデルに収束しました）。小さなデータセットには役立つかもしれませんが、このコンペティションではあまり役に立たないようです。
> 
> - DoRA - すべての線形層をチューニングする前に、初期の実験ではLoRAと比べてわずかに精度が向上しましたが、トレーニング時間が2倍になりました。他の変更（すべての線形層のチューニングなど、パフォーマンスに影響を与える可能性のある変更）を加えた後、DoRAを使用することによる遅延はさらに大きくなり、20倍になりました。コンペティションの締め切りまでに、DoRAで1つのモデルを適切にトレーニングできるほどのハードウェア能力がなく、利得も小さいと考えられるため、DoRAの使用を諦めました。
> 
> - AdaLoRA - 従来のLoRAよりも収束が遅いように見えました（サンプル効率が悪い）。最終モデルは従来のLoRAベースラインよりも悪化しました。追加のハイパーパラメータチューニングでうまく機能させることは可能かもしれませんが、これについてさらに実験するのはGPU時間の無駄だと感じました。
> 
> 
> 
> > ## CPMP
> > 
> > DORAを試しましたが、同様の経験をしました。2倍の遅延で明確な利得はありませんでした。
> > 
> > 
> > 
---
> ## Ashwani
> 
> RSLORAとDORAを試しました。
> 
> RSLORAはパフォーマンスの向上をもたらしました。
> 
> DORAは時間がかかりすぎたため（8〜9倍）、使用しませんでした。
> 
> 
> 
> > ## justin1357
> > 
> > 私の経験では、rs-loraは役に立ちませんでした。
> > 
> > 
> > 
---
> ## justin1357
> 
> LoRA-GAは理論的には最高です。ファインチューニングの勾配をシミュレートします。しかし、大規模なデータセットの場合、すべての方法はほぼ同じです。
> 
> 
> 
---

