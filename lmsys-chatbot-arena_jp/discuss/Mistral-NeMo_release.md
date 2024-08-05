# Mistral-NeMo のリリース

**Ashwani** *2024年7月19日 金曜日 01:09:26 GMT+0900 (日本標準時)* (22票)

Mistral-NeMo 12B がリリースされました。

- Gemma2 9B および Llama3 8B を凌駕します。
- 128K のコンテキストウィンドウ。
- 100 以上の言語に対応する多言語モデル: ヨーロッパ語、アジア語、インド語に優れています。
- FP8 での量子化対応トレーニング。
- Apache 2.0 ライセンス。

ブログ: [https://mistral.ai/news/mistral-nemo/](https://mistral.ai/news/mistral-nemo/)

HF ウェイト (ベース): [https://huggingface.co/mistralai/Mistral-Nemo-Base-2407](https://huggingface.co/mistralai/Mistral-Nemo-Base-2407)

HF ウェイト (インストラクト): [https://huggingface.co/mistralai/Mistral-Nemo-Instruct-2407](https://huggingface.co/mistralai/Mistral-Nemo-Instruct-2407)

---

# 他のユーザーからのコメント

> ## James Day
> 
> FYI、Mistral-NeMo のファインチューニングは現在、transformers ライブラリで壊れているようです（[https://huggingface.co/mistralai/Mistral-Nemo-Instruct-2407/discussions/6](https://huggingface.co/mistralai/Mistral-Nemo-Instruct-2407/discussions/6) を参照）。修正はすぐにリリースされる予定です ([https://github.com/huggingface/transformers/pull/32065](https://github.com/huggingface/transformers/pull/32065))。
> 
> いつものように、新しいモデルを使用する前に、少なくとも数日間はバグが発見されて修正されるのを待ちたいと思います 😉。
> 
> 
> 
---
> ## Lorry Zou
> 
> 昨日、インストラクトモデルをファインチューニングしたのですが、Gemma2 9b に匹敵するレベルには達していません…奇妙です。
> 
> 
> 
> > ## Valentin Werner
> > 
> > James が言及したバグかもしれません。これらのバグは、常に明確なものではなく、例外を発生させることもあります。モデルがトレーニングされていない、または異なるアテンションメカニズムが使用されている可能性もあります（それが実際に存在するのか、例外が発生するのかはわかりませんが、要点は理解できると思います）。
> > 
> > 
> > 
> > ## Eisuke Mizutani
> > 
> > ソースから最新の transformers をインストールして、エラーなしでトレーニングを実行できました。
> > 
> > しかし、Lorry Zou が言及したように、結果はあまり良くありませんでした（私の場合、llama3 よりも悪かったです）。
> > 
> > 
> > 
---
> ## EISLab_hwlee
> 
> コードの実装が非常に難しいです…
> 
> 
> 
---
> ## Valentin Werner
> 
> コンペティションの残り 5 週間で、リリースシーズンが本格化しています 🚀
> 
> 
> 
> > ## Psi
> > 
> > 幸い、あと 3 週間しかありません :)
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > GenAI の盛り上がりは面白いですね。NLP コンペティションでのブレークスルーは、モデリング技術ではなく、H2O、Google、Mistral（& NVIDIA）などの企業がたまたま高品質なモデルをリリースしたという偶然の産物かもしれません。それほど昔には、Mistral-7B をトレーニングして最高のパフォーマンスを出していましたが、今では 3 番目の選択肢のモデルのように思えます。
> > > 
> > > 
> > > 
---
> ## gentle bird
> 
> 新しいモデルですね。誰が試していますか？
> 
> 
> 
---
