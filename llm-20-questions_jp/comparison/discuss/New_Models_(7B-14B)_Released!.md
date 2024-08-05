# 要約 
このKaggleコンペのディスカッションでは、新たにリリースされた言語モデル（7Bから14Bのパラメータを持つモデル）についての意見交換が行われています。主なリリースされたモデルには、Gemma2、Mistral-Nemo、Llama-3.1、Qwen2、Phi-3シリーズなどが含まれています。

参加者は各モデルの性能を評価し、実際に試した結果を共有しています。例えば、Gemma2は優れたモデルである一方、微調整が不十分であるとの意見があります。Mistral系モデルは指示に従う能力が低いと言われ、Llama-3はエラーを起こす可能性がありますが、将来的には期待されているようです。Qwen2は良好な回答を提供する一方、詳細な指示には劣るとの評価です。Phiシリーズはミニモデルが優れた性能を見せているものの、語彙に限りがあるとされ、ミディアムモデルは十分な性能を発揮しきれないことが指摘されています。

全体的に、ディスカッションでは新モデルの試用を促しつつ、各モデルの特性について詳細に意見が交わされています。また、今後の調整や微調整がパフォーマンスに大きく影響するという見解も示されています。各参加者がどのモデルが「20の質問」ゲームに適しているかについての考えを述べ、さらなる試行と情報の共有を希望しています。

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

# New Models (7B-14B) Released!

**Chris Deotte** *Mon Jul 29 2024 06:07:11 GMT+0900 (日本標準時)* (17 votes)

There have been many new models released in the past 1-2 months. Have people tried these new models? How is their performance?

- Gemma2-9B-IT [here](https://huggingface.co/google/gemma-2-9b-it)

- (Nvidia) Mistral-Nemo-Instruct-2407 (12B) [here](https://huggingface.co/mistralai/Mistral-Nemo-Instruct-2407)

- (Nvidia) Minitron-8B-base [here](https://huggingface.co/nvidia/Minitron-8B-Base)

- Apple-DCLM-7B [here](https://huggingface.co/apple/DCLM-7B)

- Llama-3.1-8B-Instruct [here](https://huggingface.co/meta-llama/Meta-Llama-3.1-8B-Instruct)

- Qwen2-7B-Instruct [here](https://huggingface.co/Qwen/Qwen2-7B-Instruct)

- Phi-3-Mini-4k-Instruct (4B) [here](https://huggingface.co/microsoft/Phi-3-mini-4k-instruct)

- Phi-3-Medium-4k-Instruct (14B) [here](https://huggingface.co/microsoft/Phi-3-medium-4k-instruct)



---

 # Comments from other users

> ## Matthew S Farmer
> 
> gemma 2 - loves to answer in markdown, gives some generic answers, great at following instructions, seems like a good contended for this comp if it can get its things category vocab a bit higher. 
> 
> mistral variants (nemo int and minitron) - difficult to constraint and follow instructions. 
> 
> llama 3.1 - get ROPE error in kaggle env 
> 
> Qwen2 7b - great at following instructions but fails to get specific on keyword answers
> 
> Phi3 mini - all around good at the three roles, limited vocabulary in the things category
> 
> Phi3 medium - interestingly worse than phi3 mini? I had a very difficult time keeping this model from getting philisophical as questioner and guesser, despite multiple attempts. Implemented as AWQ, perhaps quantization affects it's instruction training? 
> 
> I keep going back to community fine tunings of LLaMa 3… getting the best results there. 
> 
> MaziyarPanahi/Llama-3-8B-Instruct-v0.10
> 
> mlabonne/Daredevil-8B
> 
> openchat/openchat-3.6-8b-20240522
> 
> 
> 
> > ## Chris DeotteTopic Author
> > 
> > Thank you for the comprehensive summary. Great experiments.
> > 
> > 
> > 
> > > ## OminousDude
> > > 
> > > I have tried most of the above models and can give a more accurate description of which models to use and why.
> > > 
> > > Gemma 2: This will give errors unless huggingface is upgraded (I think that the kaggle env. still uses old version where "Gemma2ForCasualLM" is not supported). Furthermore, this is a very good model with the current highest scores in the LLM Leaderboard for its param count. However, as this model just came out it has poor finetuning. What I mean by this is that most models (for example llama 3) have many finetuned variants (Smaug and others) which each help in some ways and are worse in others, to me the perfect model is not Gemma 2 since it does not have these yet. I think that since Gemma 2 is not meant for LLM 20Q some models that are finetuned on similar tasks could outrank it.
> > > 
> > > Mistral + Variants: Like Mathew said above these are difficult to instruct and anyone with a sophisticated prompt is out of luck. I do however think that Nemo can be different that the others because it has the current best tokenizer (out of the smaller models), Tekken, as explained [here](https://mistral.ai/news/mistral-nemo/)
> > > 
> > > Llama 3.1: Very, very promising but has an error when loading if the loading error is fixed we may see only llama 3.1 in the top places at the end. However, only time will tell and if someone can get this model to work this competition could be ruled by Llama 3.1
> > > 
> > > Qwen2: I disagree with Mathew on this one and the statistics favor me too. I do not beleive this model is great at following robust directions from my testing and from the [LLM Leaderboard](https://huggingface.co/spaces/open-llm-leaderboard/open_llm_leaderboard). On the IFEval score (this explains how well it is at following instructions) it scores a 31.49 (its instruct variant scores a 56.79); however, compared to Llama 3 it is outmatched by quite a bit because Llama 3 gets 74.08 (this is the instruct score). Furthermore, Llama 3.1 gets 77.40 which is more than 20 points ahead. However, Qwen is a good answerer and makes good questions (however it is bad at instruction following)
> > > 
> > > Phi 3 mini & medium: Mini performs better but it was trained on much less data so it doesn't know many objects/things. Medium is likely the bot that gave [these](https://www.kaggle.com/competitions/llm-20-questions/discussion/519297) flat earth questions, because like Matt said it sometimes asks questions when it is questioner.
> > > 
> > > I hope this helps you understand the reasons in which Matt made the above statements.
> > > 
> > > PS: The best strategy to use is obviously alphabetical bisection because it has such a high score on the public leaderboard.
> > > 
> > > 
> > > 
> > ## G R Shanker Sai
> > 
> > Hello [@matthewsfarmer](https://www.kaggle.com/matthewsfarmer) ,
> > 
> > Thank you for you insight on this, just wanted to understand, that by "community fine tunings of LLaMa 3", are you referring to the different flavours of llama 3 present in hugging face, or you are fine tuning it with your own data?
> > 
> > 
> > 
> > > ## Matthew S Farmer
> > > 
> > > Yes, on huggingface. I listed a few at the bottom of my comment. I've also fine tuned a model but the HF ones are too good! 
> > > 
> > > 
> > > 
> > ## Matthew S Farmer
> > 
> > RoPE error solved: [https://www.kaggle.com/competitions/llm-20-questions/discussion/523619](https://www.kaggle.com/competitions/llm-20-questions/discussion/523619)
> > 
> > 
> > 


---

> ## Muhammad Ehsan
> 
> (Written by ChatGPT-4o)
> 
> Below a bit more detail on each: 
> 
> - Gemma2-9B-IT: 
> 
> This model has 9 billion parameters and is designed for detailed comprehension and complex tasks. It's useful for applications that require a deep understanding of context and nuance.
> 
> - Mistral-Nemo-Instruct-2407: 
> 
> With 12 billion parameters, this model is optimized for instructional tasks, meaning it's particularly good at following and executing specific instructions given to it.
> 
> - Minitron-8B-base: 
> 
> An 8 billion parameter model that serves as a general-purpose base model. It's versatile and can be used for a wide range of tasks, though it might not have specialized capabilities compared to others.
> 
> - Apple-DCLM-7B: 
> 
> This model, developed by Apple, has 7 billion parameters. It's aimed at various applications and might include unique features or optimizations specific to Apple's ecosystem.
> 
> - Llama-3.1-8B-Instruct: 
> 
> This version of Llama, with 8 billion parameters, is tailored for tasks that involve following instructions or guidelines. It’s built to better understand and act on specific commands.
> 
> - Qwen2-7B-Instruct: 
> 
> Another instruction-focused model with 7 billion parameters. It’s designed to interpret and respond to detailed instructions effectively.
> 
> - Phi-3-Mini-4k-Instruct: 
> 
> This smaller model has 4 billion parameters and is optimized for following instructions, suitable for tasks that don’t require extensive processing power but need good command-following abilities.
> 
> - Phi-3-Medium-4k-Instruct: 
> 
> A medium-sized model with 14 billion parameters, this one is also geared towards instruction-following tasks, offering more processing power and complexity compared to the smaller versions.
> 
> 
> 
> > ## OminousDude
> > 
> > Which model did you use to write this response? Was it llama 3? Looks AI generated to me…
> > 
> > 
> > 
> > ## fufu2022
> > 
> > Thank you! Gemma2-9B-IT and Llama-3.1-8B are the best for me.
> > 
> > 
> > 
> > > ## torino
> > > 
> > > Hi [@fufu2022](https://www.kaggle.com/fufu2022) ,
> > > 
> > > How do you load llama3.1 on the submit environment? f it is not a secret, can you share it?
> > > 
> > > 
> > > 
> > > ## OminousDude
> > > 
> > > I don't think he does not sure if anyone has succeeded with it yet. I think he just thinks it will work well.
> > > 
> > > 
> > > 
> > > ## Matthew S Farmer
> > > 
> > > I developed a [solution today. ](https://www.kaggle.com/competitions/llm-20-questions/discussion/523619)
> > > 
> > > 
> > > 


---

> ## francesco fiamingo
> 
> wow! thanks , few of them i explored (mistral,llama,qwen) but some other even not heard (!) tks a lot! ps which is the best for our game? in your opinion?
> 
> 
> 


---

> ## Aadit Shukla
> 
> I haven't had the chance to try these new models yet, but I'm really curious about their performance. From what I've heard, they seem to offer some impressive capabilities. Has anyone here had any experience with them? I'd love to hear your thoughts! 
> 
>  thank you for update [@cdeotte](https://www.kaggle.com/cdeotte) .
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# 新しいモデル (7B-14B) のリリース！
**Chris Deotte** *2024年7月29日 06:07:11 JST* (17票)
ここ1-2ヶ月で多くの新しいモデルがリリースされました。皆さんはこれらの新しいモデルを試しましたか？パフォーマンスはいかがですか？
- Gemma2-9B-IT [こちら](https://huggingface.co/google/gemma-2-9b-it)
- (Nvidia) Mistral-Nemo-Instruct-2407 (12B) [こちら](https://huggingface.co/mistralai/Mistral-Nemo-Instruct-2407)
- (Nvidia) Minitron-8B-base [こちら](https://huggingface.co/nvidia/Minitron-8B-Base)
- Apple-DCLM-7B [こちら](https://huggingface.co/apple/DCLM-7B)
- Llama-3.1-8B-Instruct [こちら](https://huggingface.co/meta-llama/Meta-Llama-3.1-8B-Instruct)
- Qwen2-7B-Instruct [こちら](https://huggingface.co/Qwen/Qwen2-7B-Instruct)
- Phi-3-Mini-4k-Instruct (4B) [こちら](https://huggingface.co/microsoft/Phi-3-mini-4k-instruct)
- Phi-3-Medium-4k-Instruct (14B) [こちら](https://huggingface.co/microsoft/Phi-3-medium-4k-instruct)
---
 # 他のユーザーからのコメント
> ## Matthew S Farmer
> 
> gemma 2 - マークダウン形式で答えるのが好きで、少し一般的な回答をするが、指示に従うのが得意のよう。カテゴリ語彙が少し向上すれば、このコンペでの優秀な候補になると思います。
> 
> mistralのバリエーション（nemo intとminitron） - 指示に従うのが難しいです。
> 
> llama 3.1 - kaggle環境でROPEエラーが発生します。
> 
> Qwen2 7b - 指示に従うのが得意で、キーワードに対する具体的な回答には失敗します。
> 
> Phi3 mini - 3つの役割において全体的に良いが、「もの」カテゴリの語彙が限られています。
> 
> Phi3 medium - 不思議なことにPhi3 miniよりも性能が劣る？質問者や推測者として、哲学的になってしまうのを防ぐのが非常に難しかったです。同様の論理的探求を持つAWQとして実装され、量子化が指示トレーニングに影響しているのかもしれません。
> 
> 私はコミュニティの微調整されたLLaMa 3に戻っています…そこで最良の結果が得られています。
> 
> MaziyarPanahi/Llama-3-8B-Instruct-v0.10
> 
> mlabonne/Daredevil-8B
> 
> openchat/openchat-3.6-8b-20240522
> 
> > ## Chris Deotte トピック作成者
> > 
> > 包括的な概要をありがとうございます。素晴らしい実験ですね。
> > 
> > > ## OminousDude
> > > 
> > > 私は上記のほとんどのモデルを試しており、使用するモデルとその理由についてより正確な説明ができます。
> > > 
> > > Gemma 2: このモデルは、huggingfaceがアップグレードされない限りエラーを出します（Kaggle環境は、"Gemma2ForCasualLM"がサポートされていない古いバージョンを使用していると思います）。さらに、このモデルは現在のパラメータ数でLLMリーダーボードで最高のスコアを持っている非常に良いモデルです。しかし、このモデルは最近リリースされたばかりで、微調整が不十分です。私が言いたいのは、ほとんどのモデル（例えばLlama 3）は、多くの微調整済みバリエーション（Smaugなど）を持っており、それぞれが異なる点で役立ち、他の点では劣ることです。私にとって完璧なモデルはGemma 2ではありません。なぜなら、まだそれらのバリエーションが存在しないからです。そのため、Gemma 2はLLM 20Q向けではなく、特定のタスクで微調整された他のモデルに順位を上げられる可能性があります。
> > > 
> > > Mistral + バリエーション: Matthewが言ったように、指示に従うのが難しく、洗練されたプロンプトを持つ人は運がないでしょう。しかし、Nemoは他のモデルとは異なり、現在の小型モデルの中で最も良いトークナイザーであるTekkenを持つため、異なると思います。[こちらに説明があります](https://mistral.ai/news/mistral-nemo/)
> > > 
> > > Llama 3.1: 非常に有望ですが、ロード時にエラーが発生します。ロードエラーが解決されれば、このコンペのトップにLlama 3.1だけになるかもしれません。しかし、時間が経てばわかることであり、誰かがこのモデルを機能させられれば、このコンペはLlama 3.1に支配されるかもしれません。
> > > > 
> > > Qwen2: Matthewとは異なる意見ですし、統計も私に味方しています。このモデルは私のテストによって、高度な指示に従うのが得意ではないと考えています。[LLMリーダーボード](https://huggingface.co/spaces/open-llm-leaderboard/open_llm_leaderboard)でも結果がそれを示しています。IFEvalスコア（指示に従う能力を示す）は31.49（指示済みバリエーションが56.79のスコア）ですが、Llama 3に比べるとかなり劣ります。Llama 3は74.08を得ます（三指示スコア）。さらに、Llama 3.1は77.40を得ており、20ポイント以上もリードしています。しかし、Qwenは良い回答者で良い質問をする（ただし指示に従う能力は劣ります）。
> > > > 
> > > Phi 3 mini & medium: Miniが優れた性能を示しますが、はるかに少ないデータで訓練されているため、あまり多くのオブジェクトを知りません。Mediumは、[これらの](https://www.kaggle.com/competitions/llm-20-questions/discussion/519297)平面地球に関する質問を出したボットかもしれません。Matthewが言ったように、時々質問する側で質問を出すことがあります。
> > > > 
> > > Mattの上記の発言を理解するのに役立つことを願っています。
> > > > 
> > > PS: 明らかに最良の戦略はアルファベットの二分探索です。なぜなら、公開リーダーボードで非常に高いスコアを持っているからです。
> > > 
> > > 
> > ## G R Shanker Sai
> > > 
> > こんにちは [@matthewsfarmer](https://www.kaggle.com/matthewsfarmer)、
> > > 
> > Matthewさんの意見に感謝しますが、"LLaMa 3のコミュニティ微調整"とは、Hugging Faceにある異なるフレーバーのことを指していますか？それとも自分のデータで微調整しているのですか？
> > > 
> > > 
> > > 
> > ## Matthew S Farmer
> > > > 
> > > はい、Hugging Faceのことです。私はコメントの下部にいくつかリストアップしました。また、モデルを微調整したこともありますが、HFのものがあまりにも優れています！
> > > 
> > > 
> > ## Matthew S Farmer
> > > 
> > RoPEエラー解決済み: [こちら](https://www.kaggle.com/competitions/llm-20-questions/discussion/523619)
> > >
---
> ## Muhammad Ehsan
> 
> (ChatGPT-4oによる執筆)
> 
> 各モデルについてもう少し詳しく述べます：
> 
> - Gemma2-9B-IT: 
> 
> このモデルは9億のパラメータを持ち、詳細な理解や複雑なタスクに最適化されています。コンテキストやニュアンスの深い理解を必要とするアプリケーションに役立ちます。
> 
> - Mistral-Nemo-Instruct-2407: 
> 
> 12億のパラメータを持つこのモデルは、指示に特化しており、与えられた具体的な指示に従い、実行するのが得意です。
> 
> - Minitron-8B-base: 
> 
> 8億のパラメータを持つ一般的なベースモデルです。多用途でさまざまなタスクに使用できますが、他のモデルと比べると特化した能力は持たないかもしれません。
> 
> - Apple-DCLM-7B: 
> 
> Appleが開発したこのモデルは、7億のパラメータを持っています。さまざまなアプリケーションを対象としており、Appleのエコシステムに特有の機能や最適化が含まれている可能性があります。
> 
> - Llama-3.1-8B-Instruct: 
> 
> 8億のパラメータを持つこのLlamaバージョンは、指示やガイドラインに従うタスクに合わせて調整されています。特定のコマンドを理解し、行動する能力を向上させています。
> 
> - Qwen2-7B-Instruct: 
> 
> 指示に焦点を当てた別のモデルで、7億のパラメータを持っています。詳細な指示を効果的に解釈し、応答することを目指しています。
> 
> - Phi-3-Mini-4k-Instruct: 
> 
> 4億のパラメータを持つこの小型モデルは、指示に従うことに特化しており、広範な処理能力は必要ありませんが、良好な命令追従能力を求めるタスクに適しています。
> 
> - Phi-3-Medium-4k-Instruct: 
> 
> 14億のパラメータを持つ中型モデルで、指示追従タスクにも対応しており、小型モデルと比べて処理能力や複雑さを提供します。
> 
> > ## OminousDude
> > 
> > この返信を書くためにどのモデルを使用しましたか？Llama 3でしょうか？AI生成のように見えます…
> > 
> > 
> > > ## fufu2022
> > > 
> > > ありがとうございます！Gemma2-9B-ITとLlama-3.1-8Bが私にとっては最高です。
> > > 
> > > 
> > > > ## torino
> > > > 
> > > > こんにちは[@fufu2022](https://www.kaggle.com/fufu2022)、
> > > > 
> > > > 提出環境でどのようにLlama3.1をロードしますか？秘密でないなら、共有していただけますか？
> > > > 
> > > > 
> > > > > ## OminousDude
> > > > > 
> > > > > 彼はそれを行っていないと思いますが、誰かがそれを成功させたかどうかはわかりません。彼は単に良い結果が出ると思っているだけでしょう。
> > > > 
> > > > > ## Matthew S Farmer
> > > > > 
> > > > > 今日、私は[解決策を開発しました。](https://www.kaggle.com/competitions/llm-20-questions/discussion/523619)
> > > > > 
> > > > 
---
> ## francesco fiamingo
> 
> すごい！いくつかは試しました（mistral, llama, qwen）が、他のものは聞いたことがなかったです！ありがとうございます！ところで、どれが私たちのゲームに最適だと思いますか？
> 
> ---
> ## Aadit Shukla
> 
> これらの新しいモデルを試す機会はまだありませんが、そのパフォーマンスにとても興味があります。聞いたところによると、印象的な能力を持っているようです。ここで体験したことがある方はいらっしゃいますか？あなたの意見をお聞きしたいです！ 
> 
>  更新ありがとうございます [@cdeotte](https://www.kaggle.com/cdeotte) 。


</div>