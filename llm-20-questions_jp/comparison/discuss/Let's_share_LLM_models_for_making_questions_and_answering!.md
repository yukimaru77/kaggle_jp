# 要約 
このディスカッションでは、参加者たちが「20の質問」ゲームのために使用しているLLM（大規模言語モデル）について意見を交換しています。主なモデルとしては、Googleの「gemma-7b-it」やMetaの「Meta-Llama-3-8B-Instruct」が挙げられ、量子化についても8ビットと4ビットが言及されています。参加者の一人は、基本の5つのモデルとしてLlama3、Mistral、Gemma2、Phi3、Qwen2を提案し、SmaugとBagelという人気のアップグレードモデルについても言及しています。

いくつかのユーザーは異なるモデルをテストしており、「llama3-8b-it」が最も良い結果を出しているとの意見がありました。また、モデル選択においては、実用性や戦略に基づく選定が行われているようです。ある参加者はGemma 2の位置情報に対する優れた戦略に期待を寄せており、今後のベンチマークを待っている様子です。ディスカッションを通じて、LLMの活用に関する具体的な経験や洞察が共有されています。

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

# Let's share LLM models for making questions and answering!

**c-number** *Mon Jul 08 2024 10:46:38 GMT+0900 (日本標準時)* (4 votes)

What models do you use?

I use google/gemma-7b-it and meta-llama/Meta-Llama-3-8B-Instruct, both 8-bit quantized.



---

 # Comments from other users

> ## Chris Deotte
> 
> The basic 5 models are Llama3, Mistral, Gemma2, Phi3, Qwen2. And two popular upgrades are Smaug and Bagel. All have versions around 7B parameter size which work well in this competition.
> 
> 
> 


---

> ## Iqbal Singh
> 
> Phi3 Mini. No fine tuning!
> 
> 
> 


---

> ## TuMinhDang
> 
> i use gemma-9b-it fineturning
> 
> 
> 


---

> ## Kasahara
> 
> I experimented with llama3-8b-it, gemma2-9b-it, gemma-7b-it, and mistral-7b. In my experiments, llama3-8b-it performed the best.
> 
> 
> 
> > ## c-numberTopic Author
> > 
> > Same impression here.
> > 
> > 
> > 


---

> ## OminousDude
> 
> I also use llama meta-llama/Meta-Llama-3-8B-Instruct as it has a very high IF-Eval score. But I chose 4-bit quantization as it works faster and lets me make my prompts and strategy more lengthy without having to worry about my agent timing out. Also, if you do not intend to keep it a secret how do you use both models is it chosen based on the category of the keyword or what?
> 
> 
> 
> > ## c-numberTopic Author
> > 
> > I only submit one of the two models for now, but am testing both of them.
> > 
> > 
> > 
> > > ## OminousDude
> > > 
> > > Oh ok! Nice Gemma 2 is pretty promising and has a very good strategy for locations. Might use it later when the actually benchmarks and a working AWQ version come out
> > > 
> > > 
> > > 


---

> ## Matthew S Farmer
> 
> Phi3 mini here. 
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# 質問を作成し、回答するためのLLMモデルを共有しましょう！
**c-number** *2024年7月8日 10:46:38 (日本標準時)* (4票)
どのモデルを使用していますか？
私はgoogle/gemma-7b-itとmeta-llama/Meta-Llama-3-8B-Instructの両方を8ビット量子化で使用しています。
---
 # 他のユーザーからのコメント
> ## Chris Deotte
> 
> 基本の5つのモデルは、Llama3、Mistral、Gemma2、Phi3、Qwen2です。そして、人気のある2つのアップグレードモデルはSmaugとBagelです。これらはすべて、このコンペティションでうまく機能する7Bパラメータサイズのバージョンを揃えています。
> 
> ---
> 
> ## Iqbal Singh
> 
> Phi3 Miniを使用しています。ファインチューニングは行っていません！
> 
> ---
> 
> ## TuMinhDang
> 
> 私はgemma-9b-itをファインチューニングして使っています。
> 
> ---
> ## Kasahara
> 
> llama3-8b-it、gemma2-9b-it、gemma-7b-it、mistral-7bを試しましたが、実験の結果、llama3-8b-itが最も良い結果を出しました。
> 
> > ## c-number (トピック作成者)
> > 
> > 私も同じ印象です。
> > 
> > ---
> 
> ## OminousDude
> 
> 私もllama meta-llama/Meta-Llama-3-8B-Instructを使用しています。非常に高いIF-Evalスコアを持っていますからね。しかし、4ビットの量子化を選んだのは、処理が速くなり、エージェントのタイムアウトを心配せずにプロンプトや戦略を長くできるからです。また、どちらのモデルをどのように使い分けているのか秘密にしないのであれば、キーワードのカテゴリーに基づいて選んでいるのですか？
> 
> > ## c-number (トピック作成者)
> > 
> > 今のところ、2つのモデルのうち一つだけを提出していますが、両方をテストしています。
> > 
> > > ## OminousDude
> > > 
> > > なるほど！Gemma 2はかなり期待が持てそうで、位置情報に対する非常に優れた戦略を持っています。実際のベンチマークと動作するAWQバージョンが出てきたら使うかもしれませんね。
> > > 
> > > ---
> 
> ## Matthew S Farmer
> 
> 私はPhi3 miniを使っています。
> 
> ---


</div>