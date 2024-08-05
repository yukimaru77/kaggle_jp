# 要約 
### 要約

マシュー・S・ファーマーは、コンペに最適なモデル選定について考察し、特に演繹的推論と指示に従う能力が重要であると述べています。彼は、作成された問題を解決するためにモデルが推論と長期的な文脈解析を行う必要があるデータセット「MUSR」と、フォーマット指示への遵守をテストする「IFEval」を優先しています。具体的なモデル名としてPhi 3、Qwen 2、Openchat 3.5、Yi、Hermes 2とそれらの性能を挙げ、一部のモデルはMUSRのスコアが低いと指摘しています。

アジム・ソナワラは、ファーマーの見解に反論し、推論だけでなく事実の知識も重要であると主張しています。また、トークンカウントの多いモデル（例：Llama3）がうまく機能する可能性を示唆しています。ファーマーは、対話を重ね、多言語モデルがこのコンペに適している可能性についても言及しています。

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

# Model Selection

**Matthew S Farmer** *Sat Jun 29 2024 00:51:01 GMT+0900 (日本標準時)* (6 votes)

Outside of fine-tuning a model on a specific 20 Q dataset, I've been thinking about how to select the best model for the competition. This has led to me check out the [HF Open LLM Leaderboard](https://huggingface.co/spaces/open-llm-leaderboard/open_llm_leaderboard) and dig into the different benchmarks. 

The key to performance should be deductive reasoning and the model's ability to follow explicit instructions (to help with parsing). That leads me to prioritize two benchmarks:

MUSR and IFEval

MuSR (Multistep Soft Reasoning) (https://arxiv.org/abs/2310.16049) – MuSR is a new dataset consisting of algorithmically generated complex problems, each around 1,000 words in length. The problems include murder mysteries, object placement questions, and team allocation optimizations. Solving these problems requires models to integrate reasoning with long-range context parsing. Few models achieve better than random performance on this dataset.

IFEval (https://arxiv.org/abs/2311.07911) – IFEval is a dataset designed to test a model’s ability to follow explicit instructions, such as “include keyword x” or “use format y.” The focus is on the model’s adherence to formatting instructions rather than the content generated, allowing for the use of strict and rigorous metrics.

- Phi 3, Qwen 2, Openchat 3.5, Yi, Hermes 2… all at the top of the board when considering the benchmarks above. 

- In contrast: Gemma 2 7b it (the starter notebook model) has a MUSR of 12.53 whereas Intel's Neural Chat has a MUSR or 23.02…

Just some things to think about. Happy kaggleing!



---

 # Comments from other users

> ## Azim Sonawalla
> 
> 
> The key to performance should be deductive reasoning and the model's ability to follow explicit instructions (to help with parsing).
> 
> I'm not sure about this assumption.  The bots need reasoning to the extent that they can find a keyword that satisfies up to 20 simultaneous conditions as the questioner/guesser, but actual knowledge of facts in order to come up with late game questions to narrow down the last few candidates.
> 
> I've been toying with the idea that a model trained on a higher token count (e.g. llama3) might do well for this reason, but haven't gotten around to creating an experiment along those lines.
> 
> 
> 
> > ## Matthew S FarmerTopic Author
> > 
> > Interesting objection! Thanks for challenging my assumptions. Following your idea, a multilingual model may be best for this competition since it requires a larger vocabulary training than English only models? 
> > 
> > 
> > 


---



</div>
<div class="column-right">

# 日本語訳

# モデル選択
**マシュー・S・ファーマー** *2024年6月29日 00:51:01 (日本標準時)* (6票)
特定の20 Qデータセットに対してモデルをファインチューニングすることを除けば、このコンペティションに最適なモデルを選定する方法について考えています。そのため、[HF Open LLM Leaderboard](https://huggingface.co/spaces/open-llm-leaderboard/open_llm_leaderboard)をチェックし、さまざまなベンチマークに目を通してきました。  
パフォーマンスの鍵は、演繹的推論と明示的な指示に従うモデルの能力にあると思います（解析を助けるために）。これにより、以下の2つのベンチマークを優先することにしました：  
- MUSRおよびIFEval
  - MuSR (Multistep Soft Reasoning) (https://arxiv.org/abs/2310.16049) – MuSRは、アルゴリズムで生成された複雑な問題から成る新しいデータセットで、各問題は約1,000ワードの長さです。問題には、殺人ミステリー、オブジェクト配置の質問、およびチーム割り当ての最適化が含まれます。これらの問題を解決するには、モデルが推論と長期的な文脈解析を統合する必要があります。このデータセットでは、ほとんどのモデルがランダムなパフォーマンスを上回ることはありません。
  - IFEval (https://arxiv.org/abs/2311.07911) – IFEvalは、明示的な指示に従うモデルの能力をテストするために設計されたデータセットで、「キーワードxを含める」や「フォーマットyを使用する」といった指示が含まれます。焦点は、生成されたコンテンツよりもフォーマット指示へのモデルの遵守にあり、厳格な指標の使用が可能です。
- Phi 3、Qwen 2、Openchat 3.5、Yi、Hermes 2... これらは上記のベンチマークに基づいてボードのトップに位置しています。  
- 対照的に、Gemma 2 7b（スターターノートブックモデル）はMUSRが12.53であるのに対し、IntelのNeural ChatはMUSRが23.02です…。  
いくつかのことを考慮してみてください。楽しいKaggleライフを！

---

# 他のユーザーからのコメント
> ## アジム・ソナワラ
>
> パフォーマンスの鍵は演繹的推論と、解析を助けるための明示的な指示に従うモデルの能力にあると思います。
>
> この仮定には疑問があります。ボットは、質問者/推測者として同時に20の条件を満たすキーワードを見つけるために推論が必要ですが、実際には遅い段階で最後の数候補を絞り込むために事実の知識も必要です。
>
> より高いトークンカウントで訓練されたモデル（例：Llama3）が、この理由でうまく機能するのではないかと考えていますが、その方向での実験はまだ行っていません。
>
> > ## マシュー・S・ファーマー トピック作成者
> > 
> > 興味深い反論ですね！私の仮定に挑んでくれてありがとう。あなたの考えに従うと、多言語モデルがこのコンペティションには最適かもしれませんね。英語モデルよりもはるかに大きな語彙の訓練が必要だからでしょうか？ 
> > 
> > 


</div>