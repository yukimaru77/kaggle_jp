# 要約 
## ディスカッション要約

このディスカッションは、KaggleコンペティションでLlama3-8bモデルをファインチューニングしたユーザーが、オフライン環境でモデルの重みをロードできない問題に直面したことから始まりました。

ユーザーは、Hugging Faceから取得したベースモデルとKaggleのデータセットからロードしたベースモデルの両方で、モデルの重みをロードしようとしましたが、どちらも失敗しました。

ユーザーは、Hugging FaceとKaggleのデータセットのモデルが互換性がないために、ロードが失敗しているのではないかと推測しました。

しかし、ユーザーは後に、トレーニングフローの変数名に矛盾があり、バックワードに必要な正しいラベルが取得できないことが原因であることを発見しました。

他のユーザーからのコメントでは、ファインチューニングにかかった時間や、Colabでのファインチューニングに関する質問が寄せられました。

**要約:**

* ユーザーは、KaggleでファインチューニングしたLlama3-8bモデルをオフライン環境でロードできない問題に直面しました。
* 問題の原因は、トレーニングフローの変数名に矛盾があったことでした。
* ユーザーは問題を解決し、ファインチューニングを続けることができました。
* 他のユーザーは、ファインチューニングにかかった時間や、Colabでのファインチューニングに関する質問をしました。 


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

# offline use of fine-tuned Llama3

**nahyat** *Thu Jun 20 2024 16:00:07 GMT+0900 (日本標準時)* (1 votes)

Inspired by Kishan Vavdara's wonderful notebook, I fine-tuned the Llama3-8b model in colab. I got the basemodel from huggingface's Llama3-8b model instead of the kaggle dataset.（MODEL_NAME = 'meta-llama/Meta-Llama-3-8B'）

When I tried to use the fine-tuned model in kaggle, I was faced with a situation where I could not load the weights of the model I created because huggingface could not be authenticated in the offline environment.

After loading the basemodel from the kaggle dataset, I also failed to load the weights of my model.

Is it because the models in huggingface and kaggle dataset are not compatible, which is why the loading fails?

Note: Llama3 license applications for the kaggle dataset are also allowed.

Thank you for watching



---

 # Comments from other users

> ## Kishan Vavdara
> 
> I'm glad you found my notebook helpful. Can you share the error you're facing ? and did you use LoRA for fine-tuning?
> 
> 
> 
> > ## nahyatTopic Author
> > 
> > Thank you for watching!
> > 
> > I wasn't getting any errors, but I was worried that the processing was too fast (compared to your model) when loading the weights of the fine-tuned model into the basemodel. ↓
> > 
> > model_0.load_state_dict(torch.load(WEIGHTS_PATH), strict=False)
> > 
> > I noticed that the results of inference were surprisingly low, so I guessed that there was some kind of problem when loading the model parameters.
> > 
> > However, when I reviewed the code in a local environment, I confirmed that there was a discrepancy in the variable names in the training flow, which caused the correct labels required for backward to fail to be obtained. (I don't know why trainer.train() worked without an error.)
> > 
> > I'm sorry for taking the time to watch it…
> > 
> > 
> > 
> > > ## Kishan Vavdara
> > > 
> > > No worries, It's great to hear that you found the discrepancy and resolved the issue. Happy finetuning) 
> > > 
> > > 
> > > 


---

> ## Lorry Zou
> 
> How long did it take to fine-tune on Colab? I'm also trying to fine-tune on Colab but it'll take over 20 hours using A100, which is much longer than the max session length of Colab (12 hours). How did you make it shorter than 12 hours? Thank you so much.
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# Llama3のファインチューニングモデルをオフラインで使う方法

**nahyat** *2024年6月20日 16:00:07 (日本標準時)* (1票)

Kishan Vavdaraさんの素晴らしいノートブックにインスパイアされて、ColabでLlama3-8bモデルをファインチューニングしました。ベースモデルはKaggleのデータセットではなく、Hugging FaceのLlama3-8bモデル（MODEL_NAME = 'meta-llama/Meta-Llama-3-8B'）から取得しました。

Kaggleでファインチューニングしたモデルを使おうとしたところ、オフライン環境ではHugging Faceの認証ができないため、作成したモデルの重みをロードできませんでした。

Kaggleのデータセットからベースモデルをロードした後も、モデルの重みをロードできませんでした。

これは、Hugging FaceとKaggleのデータセットのモデルが互換性がないために、ロードが失敗しているのでしょうか？

注：Kaggleのデータセットでは、Llama3ライセンスの申請も許可されています。

ご視聴ありがとうございました。

---
# 他のユーザーからのコメント

> ## Kishan Vavdara
> 
> ノートブックが役に立って嬉しいです。発生しているエラーを教えていただけますか？また、ファインチューニングにLoRAを使用しましたか？
> 
> 
> 
> > ## nahyatトピック作成者
> > 
> > ご視聴いただきありがとうございます！
> > 
> > エラーは出ていませんでしたが、ファインチューニングしたモデルの重みをベースモデルにロードする際、処理が速すぎる（あなたのモデルと比べて）のではないかと心配していました。 ↓
> > 
> > model_0.load_state_dict(torch.load(WEIGHTS_PATH), strict=False)
> > 
> > 推論の結果が驚くほど低かったので、モデルのパラメータをロードする際に何か問題があったのではないかと推測しました。
> > 
> > しかし、ローカル環境でコードを見直したところ、トレーニングフローの変数名に矛盾があり、バックワードに必要な正しいラベルが取得できないことがわかりました。（なぜtrainer.train()がエラーなしで動作したのかはわかりません。）
> > 
> > 時間を取らせてしまい申し訳ありません…
> > 
> > 
> > 
> > > ## Kishan Vavdara
> > > 
> > > 問題を見つけて解決できてよかったです。ファインチューニング頑張ってください！
> > > 
> > > 
> > > 
---
> ## Lorry Zou
> 
> Colabでのファインチューニングにかかった時間はどのくらいですか？私もColabでファインチューニングしようとしていますが、A100を使用しても20時間以上かかります。これはColabの最大セッション時間（12時間）よりもはるかに長いです。どのようにして12時間よりも短くできたのですか？どうもありがとうございます。
> 
> 
> 
---




</div>