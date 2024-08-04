# 要約 
このディスカッションは、Kaggleの「LLM 20 Questions」コンペティションで、参加者Melindaがllama-cpp-pythonを使って有効な提出物を生成することに苦労している問題についてです。

Melindaは、M1 Macbookでllama-cpp-pythonを使ってコードを実行することはできるものの、Kaggleで有効な提出物として動作するバージョンを作成することができないと述べています。彼女は、KaggleのDockerイメージでllama-cpp-pythonをインストールする際に問題が発生しており、古いバージョンを実行させることはできたものの、互換性に関するエラーが発生し、GPUを正しく使用できていない可能性があると説明しています。

他のユーザーからのコメントでは、omqrikoがCMAKE_ARGSを使ってllama-cpp-pythonをインストールする方法を提案していますが、Melindaはそれでもエラーが発生したと報告しています。最終的に、Melindaはllama-cpp-pythonのライブラリをKaggleのワーキングディレクトリにコピーし、必要な依存関係をインストールすることで、エージェントが検証ラウンドを通過することに成功しました。

このディスカッションは、Kaggleコンペティションで特定のライブラリを使用する際に発生する可能性のある問題と、それらを解決するためのさまざまなアプローチを示しています。また、コミュニティの助けが問題解決に役立つことを示しています。


---
# [解決済み] llama-cpp-pythonを使って有効な提出物を生成した人はいますか？

**Melinda** *2024年6月9日日曜日 06:50:48 GMT+0900 (日本標準時)* (0票)

こんにちは、皆さん。私はM1 Macbookでllama-cpp-pythonを使ったコンペティションコードのバージョンを動かすことができ、うまく動作しています。しかし、Kaggleで有効な提出物として動作するバージョンを作成しようと、かなりの時間を費やしましたが、まだ方法がわかりません。誰か他にこの方法で成功した人がいるか、そして私のllama提出物を成功させるためのヒントがあれば教えてください。

これが、最新の環境でpip installを試したときに何が起こるかを示すノートブックです - [https://www.kaggle.com/code/melindaweathers/error-installing-llama-cpp-python](https://www.kaggle.com/code/melindaweathers/error-installing-llama-cpp-python)。私はこれをKaggle DockerのGitHubに問題として提出することを検討していますが、実際にはKaggleの問題なのかllama-cpp-pythonの問題なのかよくわからないので、まだやっていません。

私はこの[ノートブック](https://www.kaggle.com/code/raki21/llama-3-gguf-with-llama-cpp/notebook)からggufファイルを使用しようとしています。実際、古い環境とノートブックで使用されているホイールを使ってKaggleにllama-cpp-pythonをインストールすることはできますが、最新のDockerイメージでは動作しないことを考えると、エージェントはおそらく最新のDockerイメージで実行されるため、このアプローチは提出物として機能する可能性は低いと思われます。（実際、試してみましたが、うまくいきませんでした）

最新のDockerイメージでKaggleでllama-cpp-pythonの古いバージョン（0.2.25）を実行させることができましたが、もう1つの問題（[こちら](https://www.kaggle.com/competitions/llm-20-questions/discussion/505650#2859210)で言及されているように）は、-tオプションを使ってターゲットフォルダにllama-cpp-pythonをpip installしようとすると、互換性に関する多数のエラーが発生することです。これらのエラーを無視して提出してみましたが、今のところうまくいっていません。（エラーを無視すると、GPUを正しく使用していないと思います）

何か提案はありますか？
---
# 他のユーザーからのコメント
> ## MelindaTopic Author
> 
> この問題がどのように解決されたのか、より詳しく知りたい方のために、このノートブックの下の方に例を追加しました - [https://www.kaggle.com/code/melindaweathers/installing-running-llama-cpp-python?scriptVersionId=184413038](https://www.kaggle.com/code/melindaweathers/installing-running-llama-cpp-python?scriptVersionId=184413038)
> 
> 
> 
---
> ## omqriko
> 
> これを使ってください
> 
> !CMAKE_ARGS="-DLLAMA_CUBLAS=on" pip install llama-cpp-python -U --force-reinstall --extra-index-url https://abetlen.github.io/llama-cpp-python/whl/cu121
> 
> 
> 
> > ## MelindaTopic Author
> > 
> > 提案ありがとうございます！残念ながら、私も同じエラーが発生しています -
> > 
> > ```
> > Target "ggml" links to:
> >         CUDA::cuda_driver
> >         but the target was not found. 
> > 
> > ```
> > 
> > [こちら](https://www.kaggle.com/code/melindaweathers/error-installing-llama-cpp-python?scriptVersionId=183134477)は、そのエラーメッセージ全体を示すノートブックの新しいバージョンです。
> > 
> > 
> > 
> > > ## omqriko
> > > 
> > > デバッグしてようやく解決しました。これがその方法です。
> > > 
> > > ```
> > > !CMAKE_ARGS="-DLLAMA_CUBLAS=on" pip install llama-cpp-python==0.2.77 -U --force-reinstall --no-cache-dir --extra-index-url https://abetlen.github.io/llama-cpp-python/whl/cu121
> > > 
> > > ```
> > > 
> > > 
> > > 
> > > ## MelindaTopic Author
> > > 
> > > 別の提案ありがとうございます！なぜか私の場合はうまくいきませんでしたが、うまくいったものを見つけました。
> > > 
> > > この[入力](https://www.kaggle.com/datasets/mikeee8/llama-cpp-python-py310-cuda-4-kaggle/data)を追加し、フォルダを/kaggle/working/submission/libにコピーしました。その後、pip install -t /kaggle/working/submission/lib "diskcache>=5.6.1" "jinja2>=2.11.3" "numpy>=1.20.0" "typing-extensions>=4.5.0"を実行し、ERROR: pip's dependency resolver does not currently take into account all the packages that are installed. This behaviour is the source of the following dependency conflicts. の後に表示された競合を無視しました。
> > > 
> > > 以前は、ターゲットディレクトリにインストールする場合、pipは常にシステムにインストールされているパッケージを無視することに気づいていませんでした。そのため、この場合はこれらのエラーを無視しても安全だと思います。
> > > 
> > > とにかく、エージェントは少なくともllama-cpp-pythonを使って検証ラウンドを通過しました！
> > > 
> > > 
> > > 
---


