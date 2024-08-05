# 要約 
このディスカッションは、KaggleのLMSYS - Chatbot Arena Human Preference Predictionsコンペティションで、ユーザーJamshaidSohailがLlama 2モデルのトレーニングで問題に遭遇し、解決策を求めたものです。

JamshaidSohailは、kishanvavdaraが共有したノートブックを使ってLlama 2モデルをトレーニングしようとしていましたが、トレーニングが進まないという問題に直面していました。

Valentin Wernerは、tqdmを内部ループ（エポック内のステップ）に変更して、実際に何か動作しているかどうかを確認することを提案しました。また、最初のサンプルは数分かかることがあるため、ファクトリーリセットして再試行することを推奨しました。

JamshaidSohailは、Valentin Wernerのアドバイスに従い、tqdmをSTEPS_PER_EPOCH行にも追加し、トレーニングが内部に入っていることを確認しました。さらに、トークナイザーとモデルの読み込み領域に自分のアカウントのHF_TOKENを追加したところ、トレーニングが正常に動作するようになりました。

最終的に、JamshaidSohailはValentin Wernerの助けによって問題を解決し、トレーニングが正常に動作するようになりました。


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

# Training not proceeding for Llama 3

**JamshaidSohail** *Sun Jul 14 2024 20:29:44 GMT+0900 (日本標準時)* (0 votes)

Hi. I am trying to train the Llama 2 model from the [notebook](https://www.kaggle.com/code/kishanvavdara/lmsys-llama-3-tpu-train/notebook) shared by [@kishanvavdara](https://www.kaggle.com/kishanvavdara). But my training is not proceeding as shown in the figure. Any help would be appreciated.  



---

 # Comments from other users

> ## Valentin Werner
> 
> If you have the tqdm per epoch, I recommend changing it to the inner loop (steps within the epoch) to see if it actually does something:
> 
> ```
> for epoch in range(CFG.NUM_EPOCHS):
>     ste = time()
>     for step in tqdm(range(STEPS_PER_EPOCH)):
>         # Zero Out Gradients
>         OPTIMIZER.zero_grad()
> 
> ```
> 
> Also, the first samples sometimes take multiple minutes (I once had 300 seconds for the first batch) but then it will speed up afterwards. The notebook shared works well technically, so if you havent changed anything, I would just recommend factory reset and try again.
> 
> 
> 
> > ## JamshaidSohailTopic Author
> > 
> > The only changes I need to do is the addition of HF_TOKEN for my own account in the tokenizer as well as in the model loading area as below. 
> > 
> > ```
> > model_id = "meta-llama/Meta-Llama-3-8B-Instruct"
> > tokenizer = AutoTokenizer.from_pretrained(model_id,use_auth_token=HF_TOKEN)
> > 
> > base_model = LlamaForSequenceClassification.from_pretrained(model_id,
> >                                                             use_auth_token=HF_TOKEN,
> >                                                             torch_dtype=torch.bfloat16,
> >                                                             num_labels=3)    
> > 
> > ```
> > 
> > Now i followed your advice and added the tqdm to the STEPS_PER_EPOCH line as well and watching the training goes inside. 
> > 
> > 
> > 
> > > ## JamshaidSohailTopic Author
> > > 
> > > It is working now. Thank you for your comment and help 😀
> > > 
> > > 
> > > 


---



</div>
<div class="column-right">

# 日本語訳

# Llama 3のトレーニングが進まない

**JamshaidSohail** *2024年7月14日 20:29:44 (日本標準時)* (0票)
こんにちは。私は[@kishanvavdara](https://www.kaggle.com/kishanvavdara)さんが共有した[ノートブック](https://www.kaggle.com/code/kishanvavdara/lmsys-llama-3-tpu-train/notebook)を使ってLlama 2モデルをトレーニングしようとしています。しかし、図のようにトレーニングが進みません。何か助けがあれば幸いです。  
---
# 他のユーザーからのコメント
> ## Valentin Werner
> 
> エポックごとのtqdmがある場合、それを内部ループ（エポック内のステップ）に変更して、実際に何か動作しているかどうかを確認することをお勧めします。
> 
> ```
> for epoch in range(CFG.NUM_EPOCHS):
>     ste = time()
>     for step in tqdm(range(STEPS_PER_EPOCH)):
>         # Zero Out Gradients
>         OPTIMIZER.zero_grad()
> 
> ```
> 
> また、最初のサンプルは数分かかることがあります（一度、最初のバッチに300秒かかりました）。その後は速度が向上します。共有されているノートブックは技術的には問題なく動作するため、何も変更していない場合は、ファクトリーリセットして再試行することをお勧めします。
> 
> 
> 
> > ## JamshaidSohailトピック作成者
> > 
> > 必要な変更は、トークナイザーとモデルの読み込み領域に自分のアカウントのHF_TOKENを追加することだけです。以下のように。
> > 
> > ```
> > model_id = "meta-llama/Meta-Llama-3-8B-Instruct"
> > tokenizer = AutoTokenizer.from_pretrained(model_id,use_auth_token=HF_TOKEN)
> > 
> > base_model = LlamaForSequenceClassification.from_pretrained(model_id,
> >                                                             use_auth_token=HF_TOKEN,
> >                                                             torch_dtype=torch.bfloat16,
> >                                                             num_labels=3)    
> > 
> > ```
> > 
> > さて、あなたのアドバイスに従って、tqdmをSTEPS_PER_EPOCH行にも追加し、トレーニングが内部に入っているのを確認しました。
> > 
> > 
> > 
> > > ## JamshaidSohailトピック作成者
> > > 
> > > 今は動作しています。コメントと助けをありがとう 😀
> > > 
> > > 
> > > 
---



</div>