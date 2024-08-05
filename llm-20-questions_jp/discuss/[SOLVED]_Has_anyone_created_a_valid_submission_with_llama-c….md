# [解決済み] llama-cpp-pythonを使用した有効な提出物を作成した方はいらっしゃいますか？
**Melinda** *2024年6月9日 06:50:48（日本標準時）* (0票)
こんにちは、新しい友達！私はM1 Macbookで美しく動作するllama-cpp-pythonを使ったコンペティション用のコードのバージョンを持っていますが、現在、有効な提出物としてKaggleで動作するバージョンを作成するのにかなりの時間を費やしていますが、まだうまくいきません。他にこれを機能させた方はいらっしゃるでしょうか？ llamaの提出を成功させるためのヒントがあれば教えてほしいです。
こちらのノートブックで最新の環境でpip installを試みた時の結果を示しています - [https://www.kaggle.com/code/melindaweathers/error-installing-llama-cpp-python](https://www.kaggle.com/code/melindaweathers/error-installing-llama-cpp-python)。この件をkaggle dockerのgithubに問題として提出を考えていますが、Kaggle側の問題なのかllama-cpp-python側の問題なのか確信が持てないので、まだ行っていません。
私はこの[ノートブック](https://www.kaggle.com/code/raki21/llama-3-gguf-with-llama-cpp/notebook)からggufファイルを使用しようとしており、Kaggleの古い環境とノートブックで使用されたwheelsではllama-cpp-pythonをインストールできたのですが、最新のdockerイメージではうまくいかず、エージェントはおそらく最新のdockerイメージで動作するため、このアプローチが提出物として機能する可能性は低いように思えます。実際に試したところ、うまくいきませんでした。
私は古いバージョンのllama-cpp-python（0.2.25）を最新のdockerイメージのKaggleで動作させることができたのですが、別の問題として（[こちら](https://www.kaggle.com/competitions/llm-20-questions/discussion/505650#2859210)に記載の通り）、ターゲットフォルダに-pip install llama-cpp-pythonを使用してインストールしようとすると、多くの互換性に関するエラーが出ます。これらのエラーを無視してそのまま提出してみましたが、今のところうまくいっていません（エラーを無視するとGPUを正しく使用できていないのかもしれません）。何か提案はありますか？

---
 # 他のユーザーからのコメント
> ## Melinda トピック作成者
> 
> この問題がどのように解決されたかの詳細を以下のノートブックに追加したので、興味のある方はご覧ください - [https://www.kaggle.com/code/melindaweathers/installing-running-llama-cpp-python?scriptVersionId=184413038](https://www.kaggle.com/code/melindaweathers/installing-running-llama-cpp-python?scriptVersionId=184413038)

> 
---
> ## omqriko
> 
> こちらを試してください
> 
> !CMAKE_ARGS="-DLLAMA_CUBLAS=on" pip install llama-cpp-python -U --force-reinstall --extra-index-url https://abetlen.github.io/llama-cpp-python/whl/cu121
> 
> > ## Melinda トピック作成者
> > 
> > 提案ありがとうございます！残念ながら、私も同じエラーが表示されています -
> > 
> > ```
> > ターゲット "ggml" は以下にリンクしています:
> >         CUDA::cuda_driver
> >         しかし、そのターゲットは見つかりませんでした。 
> > > ```
> > 
> > [こちら](https://www.kaggle.com/code/melindaweathers/error-installing-llama-cpp-python?scriptVersionId=183134477)にフルエラーメッセージを示す新しいバージョンのノートブックがあります。
> > 
> > 
> > > ## omqriko
> > > 
> > > いくつかのデバッグを通じてようやく到達しました、こちらです：
> > > 
> > > ```
> > > !CMAKE_ARGS="-DLLAMA_CUBLAS=on" pip install llama-cpp-python==0.2.77 -U --force-reinstall --no-cache-dir --extra-index-url https://abetlen.github.io/llama-cpp-python/whl/cu121
> > > ```
> > > 
> > > 
> > > 
> > > ## Melinda トピック作成者
> > > 
> > > また別の提案をありがとうございます！それも私にはうまくいかなかったのですが、どうやらうまくいった方法が見つかりました。
> > > 
> > > この[データセット](https://www.kaggle.com/datasets/mikeee8/llama-cpp-python-py310-cuda-4-kaggle/data)を追加し、フォルダを/kaggle/working/submission/libにコピーしてから、pip install -t /kaggle/working/submission/lib "diskcache>=5.6.1" "jinja2>=2.11.3" "numpy>=1.20.0" "typing-extensions>=4.5.0"を行い、出てきたエラーを無視しました。この時、「pipの依存関係解決ツールは現在、すべてのインストールパッケージを考慮していません」と表示される場合があるのですが、この動作は、ターゲットディレクトリにインストールする際はpipが常にシステムにインストールされたパッケージを無視するため、今回は無視して問題ありません。
> > > 
> > > とにかく、少なくともllama-cpp-pythonを使用してエージェントのバリデーションラウンドは通過しました！
