# 要約 
このディスカッションでは、ユーザーのMelindaがM1 Macbook上で動作するllama-cpp-pythonを用いた応募コードのバージョンを作成しているが、Kaggleでの有効な提出物の作成に苦戦していることが述べられています。彼女は、他の参加者に成功した経験やヒントを求めています。

Melindaは、Kaggleの最新のdockerイメージでllama-cpp-pythonをインストールしようと失敗したことを報告し、自身の試行錯誤の結果を共有して、依然としてエラーが発生している状況を説明しています。彼女は古いバージョンのllama-cpp-pythonを使用したが、互換性に関するエラーに直面し、依然として有効な応募を達成できていない状態です。

他のユーザーからは、具体的なインストールコマンドやデバッグのアドバイスが寄せられましたが、それらもMelindaには効果がなく、最終的に彼女は特定のデータセットを追加し、依存関係のエラーを無視することで、llama-cpp-pythonを使用したエージェントのバリデーションラウンドを通過したことを報告しました。このように、複数の試行やコミュニティからの協力を通じて、最終的に前進を見出した事例が記されています。

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

# [SOLVED] Has anyone created a valid submission with llama-cpp-python?

**Melinda** *Sun Jun 09 2024 06:50:48 GMT+0900 (日本標準時)* (0 votes)

Hello, new friends. I have a version of the competition code using llama-cpp-python running beautifully on my M1 Macbook, but now I have spent quite a while trying to get a version of it working in a valid submission on Kaggle and have not figured out how. I'm wondering if anyone else has gotten this to work, and if anyone has tips to get my llama submission to be successful.

Here is a notebook showing what happens when trying to pip install on the latest environment - [https://www.kaggle.com/code/melindaweathers/error-installing-llama-cpp-python](https://www.kaggle.com/code/melindaweathers/error-installing-llama-cpp-python) . I am considering submitting this as an issue on the kaggle docker github, but I'm not actually sure if it is an issue with kaggle or llama-cpp-python, so I haven't done that.

I am trying to use the gguf file from this [notebook](https://www.kaggle.com/code/raki21/llama-3-gguf-with-llama-cpp/notebook), and I am actually able to install llama-cpp-python on kaggle with the old environment and wheels used in the notebook, but given that it doesn't work for me on the latest docker image, and the agents are probably run on the latest docker image, this approach seems unlikely to work as a submission. (In fact I tried it and it did not work)

I was able to get an old version of llama-cpp-python (0.2.25) to run in kaggle on the latest docker image, but another issue I am having (as mentioned [here](https://www.kaggle.com/competitions/llm-20-questions/discussion/505650#2859210)) is that trying to pip install llama-cpp-python to a target folder with the -t option throws a large number of errors about compatibility. I've tried ignoring these errors and submitting anyways, but so far no dice. (I think it's not properly using the GPU when I ignore the errors)

Any suggestions?



---

 # Comments from other users

> ## MelindaTopic Author
> 
> If anyone here is looking for more specifics about how this was solved, I added an example towards the bottom of this notebook - [https://www.kaggle.com/code/melindaweathers/installing-running-llama-cpp-python?scriptVersionId=184413038](https://www.kaggle.com/code/melindaweathers/installing-running-llama-cpp-python?scriptVersionId=184413038)
> 
> 
> 


---

> ## omqriko
> 
> Use this
> 
> !CMAKE_ARGS="-DLLAMA_CUBLAS=on" pip install llama-cpp-python -U --force-reinstall --extra-index-url https://abetlen.github.io/llama-cpp-python/whl/cu121
> 
> 
> 
> > ## MelindaTopic Author
> > 
> > Thanks for the suggestion! Unfortunately I'm seeing the same error with that as well -
> > 
> > ```
> > Target "ggml" links to:
> >         CUDA::cuda_driver
> >         but the target was not found. 
> > 
> > ```
> > 
> > [Here](https://www.kaggle.com/code/melindaweathers/error-installing-llama-cpp-python?scriptVersionId=183134477) is a new version of a notebook showing that full error message.
> > 
> > 
> > 
> > > ## omqriko
> > > 
> > > Okay finally got there with some debugging, here it is:
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
> > > Thank you for another suggestion! That didn't work for me for some reason either, but I did find something that seems to have worked.
> > > 
> > > I added this [input](https://www.kaggle.com/datasets/mikeee8/llama-cpp-python-py310-cuda-4-kaggle/data) and copied the folders to my /kaggle/working/submission/lib and then also did pip install -t /kaggle/working/submission/lib "diskcache>=5.6.1" "jinja2>=2.11.3" "numpy>=1.20.0" "typing-extensions>=4.5.0" and ignored the conflicts it listed after ERROR: pip's dependency resolver does not currently take into account all the packages that are installed. This behaviour is the source of the following dependency conflicts.
> > > 
> > > Previously I didn't realize that when you install into a target directory, pip always ignores the packages installed in the system, so I guess those errors are safe to ignore in this case.
> > > 
> > > Anyways the agent passed the validation round at least now using llama-cpp-python!
> > > 
> > > 
> > > 


---



</div>
<div class="column-right">

# 日本語訳

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


</div>