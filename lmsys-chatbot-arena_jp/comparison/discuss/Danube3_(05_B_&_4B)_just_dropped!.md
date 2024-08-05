# 要約 
このディスカッションは、H2O.aiチームがリリースした新しい言語モデル、Danube3について議論しています。Danube3は、0.5Bと4Bの2つのバージョンでリリースされ、チャットモデルも付属しています。

投稿者は、Danube3が、特に4Bバージョンが、他のオープンソースLLMと比較して優れた性能を発揮していることを指摘しています。特に、4Bモデルは、同等のサイズのPhi3-Miniと比較して、どのように性能が異なるのかに興味を持っています。

投稿者は、KaggleのGPUでは、0.5Bモデルはサイズが大きすぎてトレーニングできないため、4Bモデルに焦点を当てることを表明しています。また、H2OチームのオープンソースLLMへの貢献を称賛し、このモデルがコンペティションでどのように役立つのか期待しています。

コメント欄では、他のユーザーがDanube3の性能や、Kaggleでのトレーニングに関する質問をしています。投稿者は、Danube2-1.8Bを0.98xにトレーニングできたことを共有しています。

全体として、このディスカッションは、Danube3のリリースと、この新しいモデルがコンペティションでどのように役立つのかについて、コミュニティの興奮と期待を表しています。


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

# Danube3 (0.5 B & 4B) just dropped!

**Valentin Werner** *Mon Jul 15 2024 15:57:26 GMT+0900 (日本標準時)* (32 votes)

I have used Danube2 for several experiments and even with QLoRA on Kaggle GPU it seems to be a way better alternative to DeBERTa Large. 

Danube3 just came out as 0.5B and 4B and also comes with a Chat model, which might be an upside for this competition. The 4B model outperforms its 1.5B predecessor on all benchmarks by a lot (also a bit of a size difference), while the 0.5B outperforms Qwen2 0.5B on most benchmarks. However, to me it will be particularly interesting, how the 4B model compares to Phi3-Mini, as this is the only other model I know in its weight class. Maybe this is team Danube's secret? 😉

From my experience smaller models, like 0.5B will still not fit on Kaggle GPUs (it should work on a 4090), so I will focus on the 4B model.

I also want to applaud the H2O Team, which is quite active on Kaggle, on this new release! It is always amazing, when talented researchers and Data Scientists contribute towards the Open LLM efforts (also the sheer speed of new releases). Looking forward to see how good this model is!

Links: 

Model card: [https://huggingface.co/h2oai/h2o-danube3-4b-chat](https://huggingface.co/h2oai/h2o-danube3-4b-chat)

Technical Report: [https://arxiv.org/abs/2407.09276](https://arxiv.org/abs/2407.09276)

Benchmarks:

Some benchmarks I aggrated from the [old open LLM leaderboard](https://huggingface.co/spaces/open-llm-leaderboard-old/open_llm_leaderboard). Danube3 is not included in the leaderboard yet, but reports these values on their model card. I think it is very interesting to see how close Danube3 comes to Gemma-7B and Mistral-7B.

| Category | Benchmark | Danube3-4b-Chat | Danube2-1.8B-Chat | Phi-3-Mini-4K-Ins | Gemma-7B | Mistral-7B Ins 0.2 |
| --- | --- | --- | --- | --- | --- | --- |
| Popular aggregated | MMLU  (5-shot) | 54.74 | 37.77 | 69.08 | 64.56 | 60.78 |
| Language Understanding | HellaSwag (5-shot) | 80.36 | 73.54 | 80.60 | 82.20 | 84.88 |
| Reasoning | ARC Challenge (5-shot) | 58.96 | 43.43 | 62.97 | 61.09 | 63.14 |
|  | TruthfulQA (0-shot) | 47.79 | 39.96 | 59.88 | 44.79 | 68.26 |
|  | WinoGrande (5-shot) | 76.48 | 69.77 | 71.6 | 79.01 | 77.19 |
| Math | GSM8K CoT   (5-shot) | 50.18 | 26.16 | 85.7 | 50.87 | 40.03 |
| Average |  | 61.42 | 48.44 | 69.91 | 63.75 | 63.14 |

Models were chosen based on the models microsoft phi3-mini is reporting against on their model card.



---

 # Comments from other users

> ## chaneyMA
> 
> nice work!!!!
> 
> 
> 


---

> ## madarshbb
> 
> Just for curiosity,
> 
> From my experience smaller models, like 0.5B will still not fit on Kaggle GPUs (it should work on a 4090), so I will focus on the 4B model.
> 
> What do you mean by this? Shouldn't 0.5B model be easier to fit than 4B?
> 
> 
> 
> > ## Valentin WernerTopic Author
> > 
> > I mean 0.5 is just big enough so you can't train it on Kaggle without quantization. This is basically similar size as DeBERTa Large
> > 
> > 
> > 


---

> ## Abhay Ayare
> 
> Fantastic guide! Thank you for sharing these valuable resources and insights on becoming a data scientist. Your passion for data science is inspiring. Looking forward to exploring your book "Kaggle for Beginners."
> 
> 
> 
> > ## Valentin WernerTopic Author
> > 
> > There are plenty of kaggle books, but I certainly have not written one of them 😉
> > 
> > 
> > 


---

> ## sayoulala
> 
> Thanks for you share, May I ask that the scores of this competition by the model ?
> 
> 
> 
> > ## Valentin WernerTopic Author
> > 
> > I have no trained it yet. Some experiments (did not try super hard) got danube2-1.8B to .98x for me
> > 
> > 
> > 


---

> ## The-Hai Nguyen
> 
> You are always shedding light on my learning progress all the way back from the PII-detection competition. Really appreciate and thanks for your sharing, it helps me and the others learn a lot throughout the journey 🙏.
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# Danube3 (0.5B & 4B) がリリースされました！
**Valentin Werner** *2024年7月15日 月曜日 15:57:26 GMT+0900 (日本標準時)* (32 votes)

私はいくつかの実験で Danube2 を使用してきましたが、Kaggle の GPU で QLoRA を使用しても、DeBERTa Large よりもはるかに優れた代替手段であるように思えます。
Danube3 は 0.5B と 4B でリリースされ、チャットモデルも付属しており、このコンペティションでは有利になるかもしれません。4B モデルは、すべてのベンチマークで 1.5B の先行モデルを大幅に上回っており（サイズも少し異なります）、0.5B はほとんどのベンチマークで Qwen2 0.5B を上回っています。しかし、私にとって特に興味深いのは、4B モデルが Phi3-Mini とどのように比較されるかということです。これは、私が知っている同等のサイズの唯一のモデルです。これが Danube チームの秘密かもしれませんね？😉
私の経験では、0.5B のような小さなモデルは、Kaggle の GPU には依然として収まりません（4090 では動作するはずです）。そのため、私は 4B モデルに焦点を当てるつもりです。
また、Kaggle で非常に活発な H2O チームにも、この新しいリリースについて称賛したいと思います！才能ある研究者やデータサイエンティストがオープンな LLM の取り組みに貢献することは、常に素晴らしいことです（新しいリリースのスピードも驚異的です）。このモデルがどれほど優れているかを見るのが楽しみです！

リンク:
モデルカード: [https://huggingface.co/h2oai/h2o-danube3-4b-chat](https://huggingface.co/h2oai/h2o-danube3-4b-chat)
技術レポート: [https://arxiv.org/abs/2407.09276](https://arxiv.org/abs/2407.09276)
ベンチマーク:
[古いオープン LLM リーダーボード](https://huggingface.co/spaces/open-llm-leaderboard-old/open_llm_leaderboard)から集計したいくつかのベンチマークです。Danube3 はまだリーダーボードに含まれていませんが、モデルカードにこれらの値を報告しています。Danube3 が Gemma-7B と Mistral-7B にどれほど近いかを見るのは非常に興味深いと思います。

| カテゴリ | ベンチマーク | Danube3-4b-Chat | Danube2-1.8B-Chat | Phi-3-Mini-4K-Ins | Gemma-7B | Mistral-7B Ins 0.2 |
|---|---|---|---|---|---|---|
| 人気の集計 | MMLU (5-shot) | 54.74 | 37.77 | 69.08 | 64.56 | 60.78 |
| 言語理解 | HellaSwag (5-shot) | 80.36 | 73.54 | 80.60 | 82.20 | 84.88 |
| 推論 | ARC Challenge (5-shot) | 58.96 | 43.43 | 62.97 | 61.09 | 63.14 |
|  | TruthfulQA (0-shot) | 47.79 | 39.96 | 59.88 | 44.79 | 68.26 |
|  | WinoGrande (5-shot) | 76.48 | 69.77 | 71.6 | 79.01 | 77.19 |
| 数学 | GSM8K CoT (5-shot) | 50.18 | 26.16 | 85.7 | 50.87 | 40.03 |
| 平均 |  | 61.42 | 48.44 | 69.91 | 63.75 | 63.14 |

モデルは、microsoft phi3-mini がモデルカードで報告しているモデルに基づいて選択されました。

---
# 他のユーザーからのコメント
> ## chaneyMA
> 
> 素晴らしい仕事です!!!!
> 
> 
> 
---
> ## madarshbb
> 
> 単なる好奇心ですが、
> 
> 私の経験では、0.5B のような小さなモデルは、Kaggle の GPU には依然として収まりません（4090 では動作するはずです）。そのため、私は 4B モデルに焦点を当てるつもりです。
> 
> これはどういう意味ですか？0.5B モデルは 4B よりも収まりやすいはずではありませんか？
> 
> 
> 
> > ## Valentin Wernerトピック作成者
> > 
> > 0.5 は、量子化なしで Kaggle でトレーニングできないほどちょうど良い大きさです。これは、DeBERTa Large とほぼ同じサイズです。
> > 
> > 
> > 
---
> ## Abhay Ayare
> 
> 素晴らしいガイドですね！データサイエンティストになるための貴重なリソースと洞察を共有していただきありがとうございます。データサイエンスに対するあなたの情熱は、刺激的です。「Kaggle for Beginners」という本を調べてみたいと思います。
> 
> 
> 
> > ## Valentin Wernerトピック作成者
> > 
> > Kaggle の本はたくさんありますが、私は確かにそのうちの1冊を書いたわけではありません 😉
> > 
> > 
> > 
---
> ## sayoulala
> 
> 共有していただきありがとうございます。このコンペティションのモデルによるスコアを教えていただけますか？
> 
> 
> 
> > ## Valentin Wernerトピック作成者
> > 
> > まだトレーニングしていません。いくつかの実験（それほど熱心ではありませんでしたが）で、danube2-1.8B を 0.98x にすることができました。
> > 
> > 
> > 
---
> ## The-Hai Nguyen
> 
> あなたは、PII 検出コンペティションからずっと、私の学習の進捗に光を当ててきました。本当に感謝していますし、あなたの共有に感謝しています。それは、私や他の人の旅を通して多くのことを学ぶのに役立ちます 🙏。
> 
> 
> 
---



</div>