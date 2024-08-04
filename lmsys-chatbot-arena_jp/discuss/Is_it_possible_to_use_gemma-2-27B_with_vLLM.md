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

