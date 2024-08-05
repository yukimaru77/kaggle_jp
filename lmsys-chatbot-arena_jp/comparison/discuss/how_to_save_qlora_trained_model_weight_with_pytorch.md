# 要約 
このディスカッションは、KaggleコンペティションでQLoRAを使って訓練されたモデルの重みをPyTorchで保存する方法に関するものです。

**問題:**

* ユーザーは、transformers.Trainerを使ってQLoRAでモデルを訓練することができず、独自のPyTorch訓練スクリプトで訓練し、`torch.save`で重みを直接保存しました。
* しかし、訓練した重みを使って推論を実行したところ、ノートブックを実行するたびに予測結果が異なることがわかりました。

**解決策:**

* Valentin Wernerは、`peft_model.save_pretrained()`を使ってアダプターのみを保存することを提案しました。これにより、モデル全体を保存する必要がなくなり、保存されるデータ量が大幅に削減されます。
* ユーザーは、`torch.save`の代わりに`peft_model.save_pretrained()`を使用することを確認しました。
* Valentin Wernerは、訓練とテストの一貫性を確保するために、シードを設定することと、トークナイザーを保存するか、訓練中にトークナイザーに行った決定論的な変更を複製することを提案しました。

**結論:**

* QLoRAで訓練されたモデルの重みを保存する際には、`peft_model.save_pretrained()`を使用することが推奨されます。
* 訓練とテストの一貫性を確保するために、シードを設定し、トークナイザーを適切に処理することが重要です。

**追加情報:**

* ユーザーは、カスタムモジュールを追加したため、モデルを再訓練し、重みを2つの部分に分けて保存しました。
* Ilya Turaevは、デコーダーの分類ヘッドは、いくつかのベンチマークやその他のデータで事前訓練されているという誤解を解消しました。


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

# how to save qlora_trained model weight with pytorch

**YEI0907** *Sat Jul 13 2024 14:23:51 GMT+0900 (日本標準時)* (0 votes)

because of some problems,I can`t use qlora to train my model  with transformers.Trainer,so,I trained my qlora model with my own pytorch training script and save my weights with torch.save directly,but when i use my weights to inference,i found that when i run my notebook ,my predictions is different in each turns .so,i think my model saving method might be wrong,so, how can i save my trained weights after qlora training with pytorch training script? can i use torch.save directly? or is there any other problems during my inference?Thanks very much for answering my question



---

 # Comments from other users

> ## Valentin Werner
> 
> If you load the model with the peft library, you simply also use model.save_pretrained. This will only save the adapter and not the full model. So we are talking < 100 MB instead of multiple GB.
> 
> Code snippet as example:
> 
> ```
> if test_loss < best_val and epoch != 0:
>     model.save_pretrained(
>         f"my_newest_model_{epoch+1}_{step}"
>     )
> 
> ```
> 
> You will later load it by first loading the model itself (e.g., LlamaForSequenceClassification), getting the PEFT model and then loading the QLoRA weights
> 
> ```
> # Get peft
> model_0 = get_peft_model(base_model_0, peft_config).to(device_0) 
> # Load weights
> model_0.load_state_dict(torch.load(CFG.LORA_PATH), strict=False)
> model_0.eval()
> 
> ```
> 
> 
> 
> > ## YEI0907Topic Author
> > 
> > thanks!,I use torch.save directly to save my model,code just like this
> > 
> > ```
> > if score < best_score:
> >             best_score = score
> >             if int(os.environ["RANK"]) == 0:
> >                 torch.save({
> >                     'epoch': epoch,
> >                     'model_state_dict': dict([(k, v) for k, v in model.module.named_parameters() if v.requires_grad]),
> >                     'optimizer_state_dict': optimizer.state_dict(),
> >                     'scheduler_state_dict': scheduler.state_dict()
> >                 }, model_path)
> > 
> > ```
> > 
> > and my model loading method is same as yours,
> > 
> > so you mean I should use peft_model.save_pretrained() insteat of torch.save?
> > 
> > addtionaly,i test my weights in kaggle by using train_data and my loss is 1.8xxxx,but in my traing, the eval_sets loss is 0.9XX and train_sets loss is also 0.9xx
> > 
> > by the way,i learned a lot from your notebooks, thank you for sharing your notebook!
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > Happy to be of help :)
> > > 
> > > I highly recommend saving adapters separately and loading them separately. I do not see any value in saving full models as long as you are not adding any layers to the model. If you create a custom model with additional layers, you will need to save these weights to, in that case it might make sense to save full models.
> > > 
> > > However, if you load Llama3 like this:
> > > 
> > > ```
> > > base_model = LlamaForSequenceClassification.from_pretrained(model_id, token=HF_TOKEN, num_labels=CFG.NUM_LABELS, torch_dtype=CFG.TORCH_DTYPE, trust_remote_code=True)   
> > > 
> > > ```
> > > 
> > > The sequence classification head is always initialized in the same way, just random values. Things that can help achieve the same result is setting the seed, so the weights are randomly initialized exactly as they were initialized during training.
> > > 
> > > ```
> > > def set_seeds(seed):
> > >     """Set seeds for reproducibility """
> > >     os.environ['PYTHONHASHSEED'] = str(seed)
> > >     random.seed(seed)
> > >     np.random.seed(seed)
> > >     torch.manual_seed(seed)
> > >     if torch.cuda.is_available():
> > >         torch.cuda.manual_seed(seed)
> > >         torch.cuda.manual_seed_all(seed)
> > >     # Set seed for all TPU cores
> > >     xm.set_rng_state(seed, device=xm.xla_device())  
> > > 
> > > ```
> > > 
> > > Doing this helped me to achieve a better LB <-> CV relationship.
> > > 
> > > Further, you may want to save the tokenizer or replicate and deterministic changes you did to it during training (e.g., if you changed pad_token_id or such). Make sure you are exactly tokenizing the same way (also input formats etc.) as you did during training. This can easily switch a lot for your score too.
> > > 
> > > 
> > > 
> > > ## YEI0907Topic Author
> > > 
> > > thanks,this provide a new idea for me to ensure consistency between train and test ;for my model , i had added some my custom modules,and i will re-train the model and save the weight with two part,one for llama3 with peft.save_pretrained(),one for my custom module with torch.save directly.T_T，the previous weight resulted in my LB score reaching 3.x
> > > 
> > > 
> > > 
> > > ## Ilya Turaev
> > > 
> > > All my life I've been thinking that classification heads for decoders were pretrained on some benchmarks or other data. Glad that I've busted this myth and misunderstanding now…
> > > 
> > > 
> > > 


---



</div>
<div class="column-right">

# 日本語訳

# QLoRAで訓練したモデルの重みをPyTorchで保存する方法

**YEI0907** *2024年7月13日土曜日 14:23:51 JST* (0票)

transformers.Trainerを使ってQLoRAでモデルを訓練することができない問題が発生したため、独自のPyTorch訓練スクリプトでQLoRAモデルを訓練し、`torch.save`で重みを直接保存しました。しかし、訓練した重みを使って推論を実行したところ、ノートブックを実行するたびに予測結果が異なることがわかりました。そのため、モデルの保存方法が間違っているのではないかと考えています。

PyTorch訓練スクリプトでQLoRA訓練後の重みを保存するにはどうすればよいでしょうか？`torch.save`を直接使用できますか？それとも、推論中に他に問題があるのでしょうか？ご回答よろしくお願いいたします。

---

# 他のユーザーからのコメント

> ## Valentin Werner
> 
> PEFTライブラリでモデルを読み込む場合は、`model.save_pretrained`も使用します。これにより、アダプターのみが保存され、モデル全体は保存されません。そのため、保存されるデータは、数GBではなく、100MB未満になります。
> 
> コードスニペットの例：
> 
> ```python
> if test_loss < best_val and epoch != 0:
>     model.save_pretrained(
>         f"my_newest_model_{epoch+1}_{step}"
>     )
> 
> ```
> 
> 後で、まずモデル自体（例：LlamaForSequenceClassification）を読み込み、PEFTモデルを取得してからQLoRAの重みを読み込むことで、モデルを読み込むことができます。
> 
> ```python
> # PEFTを取得
> model_0 = get_peft_model(base_model_0, peft_config).to(device_0) 
> # 重みを読み込み
> model_0.load_state_dict(torch.load(CFG.LORA_PATH), strict=False)
> model_0.eval()
> 
> ```
> 
> 
> 
> > ## YEI0907トピック作成者
> > 
> > ありがとうございます！`torch.save`を直接使用してモデルを保存しています。コードは以下のとおりです。
> > 
> > ```python
> > if score < best_score:
> >             best_score = score
> >             if int(os.environ["RANK"]) == 0:
> >                 torch.save({
> >                     'epoch': epoch,
> >                     'model_state_dict': dict([(k, v) for k, v in model.module.named_parameters() if v.requires_grad]),
> >                     'optimizer_state_dict': optimizer.state_dict(),
> >                     'scheduler_state_dict': scheduler.state_dict()
> >                 }, model_path)
> > 
> > ```
> > 
> > モデルの読み込み方法は、あなたと同じです。
> > 
> > つまり、`torch.save`の代わりに`peft_model.save_pretrained()`を使用する必要があるということですか？
> > 
> > さらに、Kaggleで訓練データを使って重みをテストしたところ、損失は1.8xxxxでした。しかし、訓練では、評価セットの損失は0.9XX、訓練セットの損失も0.9xxでした。
> > 
> > ちなみに、あなたのノートブックから多くのことを学びました。ノートブックを共有していただきありがとうございます！
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > お役に立てて幸いです :)
> > > 
> > > アダプターを別々に保存して、別々に読み込むことを強くお勧めします。モデルにレイヤーを追加していない限り、モデル全体を保存するメリットはありません。カスタムモデルを作成してレイヤーを追加する場合は、これらの重みも保存する必要があります。その場合、モデル全体を保存する方が理にかなっているかもしれません。
> > > 
> > > ただし、Llama3を以下のように読み込む場合：
> > > 
> > > ```python
> > > base_model = LlamaForSequenceClassification.from_pretrained(model_id, token=HF_TOKEN, num_labels=CFG.NUM_LABELS, torch_dtype=CFG.TORCH_DTYPE, trust_remote_code=True)   
> > > 
> > > ```
> > > 
> > > シーケンス分類ヘッドは常に同じ方法で初期化されます。ランダムな値だけです。同じ結果を得るのに役立つのは、シードを設定することです。これにより、重みが訓練中に初期化されたときとまったく同じようにランダムに初期化されます。
> > > 
> > > ```python
> > > def set_seeds(seed):
> > >     """再現性のためにシードを設定します"""
> > >     os.environ['PYTHONHASHSEED'] = str(seed)
> > >     random.seed(seed)
> > >     np.random.seed(seed)
> > >     torch.manual_seed(seed)
> > >     if torch.cuda.is_available():
> > >         torch.cuda.manual_seed(seed)
> > >         torch.cuda.manual_seed_all(seed)
> > >     # すべてのTPUコアのシードを設定
> > >     xm.set_rng_state(seed, device=xm.xla_device())  
> > > 
> > > ```
> > > 
> > > これにより、LBとCVの関係を改善することができました。
> > > 
> > > さらに、トークナイザーを保存するか、訓練中にトークナイザーに行った決定論的な変更を複製する必要があるかもしれません（例：`pad_token_id`などを変更した場合）。訓練時と同じように、トークナイザーをまったく同じ方法でトークナイズしていることを確認してください（入力形式なども含めて）。これにより、スコアが大きく変わる可能性があります。
> > > 
> > > 
> > > 
> > > ## YEI0907トピック作成者
> > > 
> > > ありがとうございます。これは、訓練とテストの一貫性を確保するための新しいアイデアを提供してくれます。私のモデルでは、カスタムモジュールをいくつか追加しました。モデルを再訓練し、重みを2つの部分に分けて保存します。1つは`peft.save_pretrained()`を使用したLlama3用、もう1つは`torch.save`を直接使用したカスタムモジュール用です。T_T、以前の重みはLBスコアが3.xに達していました。
> > > 
> > > 
> > > 
> > > ## Ilya Turaev
> > > 
> > > これまでずっと、デコーダーの分類ヘッドは、いくつかのベンチマークやその他のデータで事前訓練されていると思っていました。この誤解と誤解を解消できて嬉しいです…
> > > 
> > > 
> > > 
---




</div>