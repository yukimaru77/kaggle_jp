# 要約 
このディスカッションは、KaggleコンペティションでLLMのファインチューニングを行う際に、トレーニングステップ数が期待通りにならない問題について議論しています。

**問題:**

* ユーザーは、Kaggle GPUで実行したコードではトレーニングステップ数が期待通りに31ステップになるのに対し、リモートサーバーで実行した場合は10ステップしか実行されなかったと報告しています。
* サンプルサイズ、gradient_accumulate_steps、batch_sizeは両方の環境で同じ設定になっています。

**原因:**

* ユーザーは、リモートサーバーに3つのGPUがあり、モデルをロードした際にdevice_map={'': 0}を設定したにもかかわらず、なぜか並列に実行されてしまったことを突き止めました。

**解決策:**

* ユーザーは、コードの先頭にCUDA_VISIBLE_DEVICES = 0を明示的に設定することで、問題を解決しました。これにより、GPUの並列化が回避され、トレーニングステップ数が期待通りになりました。

**その他:**

* Valentin Wernerは、トレーニングデータセットと検証データセットが入れ替わっていないか確認することを提案しました。ユーザーは、トレーニングデータセットの長さが500、検証データセットの長さが100であることを確認しました。

**結論:**

このディスカッションは、GPUの並列化が意図せず発生した場合に、トレーニングステップ数が期待通りにならない問題が発生する可能性があることを示しています。CUDA_VISIBLE_DEVICES変数を明示的に設定することで、このような問題を回避することができます。


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

# Traing steps cannot match the sample size!

**godmysalary** *Fri Jul 05 2024 12:49:34 GMT+0900 (日本標準時)* (1 votes)

Hello everyone! We were using the vscode to run the amazing fine-tune work by [https://www.kaggle.com/code/hotchpotch/train-llm-detect-ai-comp-mistral-7b/notebook](url)

The only difference is that we change the model to Llama3. 

And when I run the code on Kaagle GPU, everything is fine. The sample size is 500, gradient_accumulate_steps is 16, batch_size=1, so we will undergo 31 steps, which is shown by the first picture below. 

However when I just COPY the same code to my vscode which is connected to a remote server, the total steps became 10! The sample size, gradient_accumulate_steps, batch_size stay unchanged but the total steps became 10, which is shown in the second picture and means only about 160 (16*10) samples are processed? Only one GPU is used on the vscode. 

Could anybody give me a hint about what is going on? The packages are updated. 



---

 # Comments from other users

> ## godmysalaryTopic Author
> 
> Hello everybody! We checked this probelm again and finally found the "killer"! Our remote server has 3 GPUs and so as you may suspect, the program is parallelled. The most annoying part is that when we loaded the model, we set device_map={'': 0} but somehow it still ran parallelly. So we explicitly set CUDA_VISIBLE_DEVICES = 0 at the beginning of our code and the problem faded! Hope this help you for your fine-tuning.
> 
> 
> 


---

> ## Valentin Werner
> 
> Did you check the length of your data? Did you accidentally swap train and validation dataset?
> 
> 
> 
> > ## godmysalaryTopic Author
> > 
> > yes! the length of train_dataset is 500 and the length of evaluation_dataset is 100.
> > 
> > 
> > 


---



</div>
<div class="column-right">

# 日本語訳

# トレーニングステップがサンプルサイズと一致しません！

**godmysalary** *2024年7月5日 金曜日 12:49:34 JST* (1票)

皆さん、こんにちは！私たちは、[https://www.kaggle.com/code/hotchpotch/train-llm-detect-ai-comp-mistral-7b/notebook](url) の素晴らしいファインチューニング作業を実行するために、vscodeを使用していました。

唯一の違いは、モデルをLlama3に変更したことです。

そして、Kaggle GPUでコードを実行すると、すべて正常に動作します。サンプルサイズは500、gradient_accumulate_stepsは16、batch_sizeは1なので、31ステップを実行することになります。これは、下の最初の画像に示されています。

しかし、同じコードをリモートサーバーに接続したvscodeにコピーしたところ、合計ステップ数が10になりました！サンプルサイズ、gradient_accumulate_steps、batch_sizeは変更されていませんが、合計ステップ数は10になり、これは2番目の画像に示されており、約160（16*10）のサンプルしか処理されていないことを意味します。vscodeでは、1つのGPUのみが使用されています。

何が起こっているのか、ヒントをいただけませんか？パッケージは更新されています。

---
# 他のユーザーからのコメント

> ## godmysalaryトピック作成者
> 
> 皆さん、こんにちは！この問題を再度確認したところ、ついに「犯人」を見つけました！私たちのリモートサーバーには3つのGPUがあり、予想通りプログラムは並列化されています。最も厄介な点は、モデルをロードしたときに、device_map={'': 0}を設定したにもかかわらず、なぜか並列に実行されてしまったことです。そこで、コードの先頭にCUDA_VISIBLE_DEVICES = 0を明示的に設定したところ、問題は解消されました！ファインチューニングでお役に立てれば幸いです。
> 
> 
> 
---
> ## Valentin Werner
> 
> データの長さを確認しましたか？誤ってトレーニングデータセットと検証データセットを入れ替えていませんか？
> 
> 
> 
> > ## godmysalaryトピック作成者
> > 
> > はい！train_datasetの長さは500、evaluation_datasetの長さは100です。
> > 
> > 
> > 
---



</div>