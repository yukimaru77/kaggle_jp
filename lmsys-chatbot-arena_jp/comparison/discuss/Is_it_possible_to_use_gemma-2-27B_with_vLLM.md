# 要約 
このディスカッションは、KaggleのLMSYS - Chatbot Arena Human Preference Predictionsコンペティションにおいて、gemma-2-27BモデルをvLLMで利用できるかどうかについて議論しています。

**要約:**

* ユーザーyechenzhi1は、gemma-2-27BをvLLMで利用しようとしましたが、FlashInferのGPUサポートの制限により、T4 GPUでは実行できないことがわかりました。
* Yixiao Yuanは、gemma-2をHugging Faceで実行できることを提案し、vLLMは生成タスクに適していますが、分類タスクではHugging Faceとパフォーマンスが似ていると述べています。
* yechenzhi1は、量子化されたgemma-2-27Bはvllm/sglangでのみ正しく推論できることを発見しました。
* ShelterWは、gemma-2-27BをvLLMで現在使用できるかどうかを尋ねました。
* Somesh88は、Kaggleのgemma-2の重みに設定ファイルが含まれていないため、Transformersからロードしようとするとインターネットアクセスが必要になる問題を提起しました。
* Kishan Vavdaraは、設定、パッケージ、重みをKaggleデータセットとして作成することで、インターネットアクセスなしで推論ノートブックに追加できる解決策を提案しました。

**結論:**

このディスカッションは、gemma-2-27BをvLLMで利用することの課題と、その問題に対する潜在的な解決策について議論しています。vLLMは、gemma-2-27Bのような大規模言語モデルを効率的に実行するための有望なツールですが、GPUサポートの制限や設定ファイルの欠如など、克服すべき課題があります。


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

# Is it possible to use gemma-2-27B with vLLM?

**yechenzhi1** *Tue Jul 23 2024 00:34:19 GMT+0900 (日本標準時)* (1 votes)

Inspired by [@cdeotte](https://www.kaggle.com/cdeotte)'s great [work](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/521294), I'm trying to use gemma-2-27B with vLLM. First I use GPTQmodel to quantinize it to 4-bit, then use vLLM-0.5.2 to do the infer. But we have to use flashinfer as the backend because of gemma-2's logits capping, then the problem comes, it's said flashinfer only supports GPU with compute [capability >= 8.0](https://github.com/vllm-project/vllm/issues/6173#issuecomment-2214759644), and T4 is 7.5. So is gemma-2-27b impossible for this competition?



---

 # Comments from other users

> ## Yixiao Yuan
> 
> I think we can't run gemma-2 with vLLM, but we can run it by huggingface. vLLM is much better for generation task due to PagedAttention. However, if we only generate one token or use classification head (we don't need KV cache in such cases), the performance should be similar.
> 
> 
> 
> > ## yechenzhi1Topic Author
> > 
> > bad news here, it seems only vllm/sglang can infer [quantized gemma-2-27b](https://github.com/ModelCloud/GPTQModel/issues/140#issuecomment-2242221690) correctly right now. 
> > 
> > 
> > 
> > ## yechenzhi1Topic Author
> > 
> > But thanks! I'll try it anyway!
> > 
> > 
> > 
> > > ## beanpotato
> > > 
> > > Could you share if you can run gema-2-27b with vLLM?🥰
> > > 
> > > 
> > > 
> > > ## yechenzhi1Topic Author
> > > 
> > > No, T4 GPU doesn't support FlashInfer. I stopped trying gemma-2-27B after a few days.
> > > 
> > > 
> > > 


---

> ## ShelterW
> 
> Is it possible to use gemma-2-27B with vLLM now?
> 
> 
> 
> > ## Somesh88
> > 
> > I've been trying to use gemma 2 with vllm the weights over kaggle doesn't contain config file. If I try to load it form transformers then I have to keep internet access enabled which is not allowed in submission. have you found any workround for this? 
> > 
> > 
> > 
> > > ## Kishan Vavdara
> > > 
> > > you can create kaggle dataset of configs, packages, weights, etc. and add to your inference notebook, then you can use it without enabling internet. 
> > > 
> > > 
> > > 


---



</div>
<div class="column-right">

# 日本語訳

# vLLMでgemma-2-27Bを使用することは可能ですか？

**yechenzhi1** *2024年7月23日 火曜日 00:34:19 日本標準時* (1票)

[@cdeotte](https://www.kaggle.com/cdeotte) の素晴らしい[仕事](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/521294) に触発されて、gemma-2-27BをvLLMで使用しようと試みています。まず、GPTQmodelを使って4ビットに量子化し、次にvLLM-0.5.2を使って推論を実行します。しかし、gemma-2のロジット上限のため、FlashInferをバックエンドとして使用する必要があります。そして問題が発生します。FlashInferは、[compute capability >= 8.0](https://github.com/vllm-project/vllm/issues/6173#issuecomment-2214759644) のGPUのみをサポートするとされており、T4は7.5です。つまり、gemma-2-27bはこのコンペティションでは不可能なのでしょうか？
---
# 他のユーザーからのコメント
> ## Yixiao Yuan
> 
> gemma-2をvLLMで実行することはできないと思いますが、Hugging Faceで実行できます。vLLMは、PagedAttentionのおかげで生成タスクに適していますが、トークンを1つだけ生成する場合や分類ヘッドを使用する場合（このような場合、KVキャッシュは不要です）、パフォーマンスは似ているはずです。
> 
> 
> 
> > ## yechenzhi1トピック作成者
> > 
> > 悪い知らせですが、現在、[量子化されたgemma-2-27b](https://github.com/ModelCloud/GPTQModel/issues/140#issuecomment-2242221690) を正しく推論できるのはvllm/sglangのみのようです。
> > 
> > 
> > 
> > ## yechenzhi1トピック作成者
> > 
> > しかし、ありがとうございます！ それでも試してみます！
> > 
> > 
> > 
> > > ## beanpotato
> > > 
> > > gema-2-27bをvLLMで実行できたかどうか教えていただけますか？🥰
> > > 
> > > 
> > > 
> > > ## yechenzhi1トピック作成者
> > > 
> > > いいえ、T4 GPUはFlashInferをサポートしていません。数日後、gemma-2-27Bの試みを中止しました。
> > > 
> > > 
> > > 
---
> ## ShelterW
> 
> gemma-2-27BをvLLMで現在使用することは可能ですか？
> 
> 
> 
> > ## Somesh88
> > 
> > gemma 2をvllmで試していますが、Kaggleの重みには設定ファイルが含まれていません。Transformersからロードしようとすると、インターネットアクセスを有効にする必要がありますが、これは提出では許可されていません。これに対する回避策はありますか？
> > 
> > 
> > 
> > > ## Kishan Vavdara
> > > 
> > > 設定、パッケージ、重みなどのKaggleデータセットを作成して、推論ノートブックに追加できます。そうすれば、インターネットを有効にすることなく使用できます。
> > > 
> > > 
> > > 
---



</div>