# 要約 
このディスカッションは、Kaggle の LMSYS - Chatbot Arena Human Preference Predictions コンペティションに参加しているユーザーが、Gemma2 と Llama3 のアンサンブルモデルを使用中に CUDA OOM エラーが発生した問題について議論しています。

Lorry Zou は、Gemma2 モデルの推論後に Llama3 モデルを読み込むと CUDA OOM エラーが発生し、Gemma モデルを GPU から削除してもメモリが解放されないという問題を報告しました。

他のユーザーからのコメントでは、以下の解決策が提案されています。

* **ノートブック全体を Python スクリプトに変換する:** これにより、メモリがクリアされることが確認されました。
* **モデルと中間テンソルへのすべての参照をクリアする:** `gc.collect()` を使用して、モデルとテンソルへの参照をクリアします。
* **GPU を使用している他のプロセスがないことを確認する:** バックグラウンドプロセスがメモリを消費している可能性があります。
* **勾配チェックポイントを使用する:** これにより、メモリを節約できます。
* **バッチサイズと max_length を実験する:** これらのパラメータを調整することで、メモリ使用量を削減できます。
* **モデル並列化を試す:** これにより、複数の GPU にモデルを分散させることができます。

Lorry Zou は、推論中に実際に使用されているのはモデルの 1 つだけである可能性があり、GPU 0 のメモリのみが解放される理由を説明しました。

ShelterW は、Gemma2 と Llama3 のアンサンブルを使用していた際に、さらに悪化したことを報告しました。

最終的に、Lorry Zou は、メモリに残っているものがあり、削除し忘れている可能性があることを認めました。Valentin Werner は、`gc.collect()` を使用することで、両方の GPU のメモリ使用量が 300 MB 未満になったことを報告しました。

このディスカッションは、CUDA OOM エラーのトラブルシューティングに関する有益な情報を提供しています。特に、モデルとテンソルへの参照を正しくクリアすること、GPU を使用している他のプロセスがないことを確認すること、バッチサイズと max_length を調整することなどが重要です。


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

# CUDA OOM when ensemble Gemma2 and Llama3

**Lorry Zou** *Tue Jul 16 2024 00:39:47 GMT+0900 (日本標準時)* (6 votes)

Hi everyone, I'm trying to ensemble gemma2 and llama3. My strategy is load data -> load gemma2 model -> gemma2 inference -> load llama3 model -> llama3 inference -> ensemble. I use T4*2 and my code is mainly based on [@kishanvavdara](https://www.kaggle.com/kishanvavdara) 's inference notebook.

My issue is: When I try to load llama3 model after gemma2 inference, I encounter CUDA OOM. I try to clear memory by removing gemmas from the two GPUs (I load one gemma model on each GPU) using gemma_model.cpu(); del gemma_model; torch.cuda.empty_cache(), but it doesn't help. Only GPU 0 is freed and GPU 1 is still using 8.9GB memory. 

Is there any way to release all the memory from both GPUs? Or perhaps reduce of size of the models?



---

 # Comments from other users

> ## no fit just luck
> 
> I would like to share a simple method. You can use '%%writefile' to create a '.py' file and then run this file by "!python file_name.py" to generate your submission. Specifically, you can create two py files for gemma and llama. In each of the file, you can save the model output as a csv file. At last, you can load them and do your ensemble. 
> 
> The key point is that by using  "!python file_name.py", the memory will be clean. Hope this can solve your problem.
> 
> 
> 
> > ## Lorry ZouTopic Author
> > 
> > Yeah I just converted the whole notebook to python script and it works well with releasing memory. I didn't know we can even directly submit a python script LOL.
> > 
> > 
> > 


---

> ## Priyanshu Joshi
> 
> Make sure you are correctly clearing all references to the model and intermediate tensors.
> 
> ```
> import gc
> 
> gemma_model.cpu()
> del gemma_model
> torch.cuda.empty_cache()
> gc.collect()
> 
> ```
> 
> Ensure your inference environment has no other processes using the GPUs. Sometimes background processes can consume significant memory. Use gradient checkpointing to trade computational cost for memory usage. This saves memory by recomputing some parts of the model during the backward pass. Experiment with batch size and max_length as Veletin mentioned in his comment. You can try [model parallelism](https://huggingface.co/docs/transformers/v4.15.0/parallelism).
> 
> 
> 


---

> ## Lorry ZouTopic Author
> 
> I'm wondering why only GPU 0's memory can be released after inference. Maybe only one of the model is actually used during inference? The code:
> 
> `@torch.no_grad()
> 
> [@torch.cuda.amp.autocast](https://www.kaggle.com/torch.cuda.amp.autocast)()
> 
> def gemma_inference(df, model, device, batch_size=cfg.batch_size, max_length=cfg.max_length):
> 
>     a_win, b_win, tie = [], [], []
> 
> ```
> for start_idx in range(0, len(df), batch_size):
>     end_idx = min(start_idx + batch_size, len(df))
>     tmp = df.iloc[start_idx:end_idx]
>     input_ids = tmp["input_ids"].to_list()
>     attention_mask = tmp["attention_mask"].to_list()
>     inputs = pad_without_fast_tokenizer_warning(
>         gemma_tokenizer,
>         {"input_ids": input_ids, "attention_mask": attention_mask},
>         padding=True,
>         max_length=max_length,
>         pad_to_multiple_of=None,
>         return_tensors="pt",
>     )
>     outputs = model(**inputs.to(device))
>     proba = outputs.logits.softmax(-1).cpu()
> 
>     a_win.extend(proba[:, 0].tolist())
>     b_win.extend(proba[:, 1].tolist())
>     tie.extend(proba[:, 2].tolist())
> 
>     df["winner_model_a"] = a_win
>     df["winner_model_b"] = b_win
>     df["winner_tie"] = tie
>     return df` and
> 
> ```
> 
> with ThreadPoolExecutor(max_workers=2) as executor:
>     gemma_results = executor.map(gemma_inference, (gemma_sub_1, gemma_sub_2), (gemma_model_0, gemma_model_1), (device_0, device_1))
> 
> I also tried batch_size=4 and 2, there's no difference.
> 
> 
> 
> > ## Valentin Werner
> > 
> > are you actually using gc.collect() - i had it before where it wouldnt be released until gc.collect() was done. exatly like ShelterW described in their comment.
> > 
> > 
> > 
> > > ## Lorry ZouTopic Author
> > > 
> > > Yes I'm suing gc.collect(), but it doesn't work: 
> > > 
> > > gemma_model_0.to('cpu')
> > > del gemma_model_0
> > > gc.collect()
> > > gemma_model_1.to('cpu')
> > > del gemma_model_1
> > > gc.collect()
> > > with torch.no_grad():
> > >     torch.cuda.set_device('cuda:0')
> > >     torch.cuda.empty_cache()
> > >     torch.cuda.set_device('cuda:1')
> > >     torch.cuda.empty_cache()
> > > 
> > > 
> > > 


---

> ## ShelterW
> 
> When I used the Gemma2 and Llama3 ensemble, it was even worse.
> 
> ```
> import torch
> import gc
> del proba, model_0, model_1, test, data, aug_data
> gc.collect()
> torch.cuda.empty_cache()
> 
> ```
> 
> 
> 
> > ## Lorry ZouTopic Author
> > 
> > I believe there's something remaining in the memory and we forgot to delete it…😆
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > This gets both GPUs down to below 300 MB. Else turn down max_length and / or batch size
> > > 
> > > 
> > > 
> > ## Allen Wang
> > 
> > Yes, I have the same problem as you. Is there any way to solve it
> > 
> > 
> > 


---



</div>
<div class="column-right">

# 日本語訳

# CUDA OOM が発生する問題: Gemma2 と Llama3 のアンサンブル

**Lorry Zou** *2024年7月16日 火曜日 00:39:47 GMT+0900 (日本標準時)* (6票)

皆さん、こんにちは。Gemma2 と Llama3 をアンサンブルしようとしています。私の戦略は、データの読み込み -> Gemma2 モデルの読み込み -> Gemma2 推論 -> Llama3 モデルの読み込み -> Llama3 推論 -> アンサンブルです。T4*2 を使用しており、コードは主に [@kishanvavdara](https://www.kaggle.com/kishanvavdara) さんの推論ノートブックに基づいています。

問題点は、Gemma2 の推論後に Llama3 モデルを読み込もうとすると、CUDA OOM が発生することです。Gemma モデルを 2 つの GPU から削除してメモリをクリアしようとしました (各 GPU に 1 つの Gemma モデルを読み込んでいます) が、`gemma_model.cpu(); del gemma_model; torch.cuda.empty_cache()` を使用しても効果がありません。GPU 0 のみが解放され、GPU 1 は依然として 8.9GB のメモリを使用しています。

両方の GPU からすべてのメモリを解放する方法、またはモデルのサイズを縮小する方法はあるでしょうか？

---
# 他のユーザーからのコメント

> ## 単なる運ではなく、適切な方法
> 
> 簡単な方法を紹介します。`%%writefile` を使用して `.py` ファイルを作成し、`!python file_name.py` でこのファイルを実行して提出結果を生成できます。具体的には、Gemma と Llama 用に 2 つの py ファイルを作成できます。各ファイルで、モデルの出力を csv ファイルとして保存できます。最後に、それらをロードしてアンサンブルを実行できます。
> 
> 重要な点は、`!python file_name.py` を使用することで、メモリがクリアされることです。これが問題の解決に役立つことを願っています。
> 
> 
> 
> > ## Lorry Zouトピック作成者
> > 
> > はい、ノートブック全体を Python スクリプトに変換したところ、メモリ解放がうまくいきました。Python スクリプトを直接提出できることを知りませんでした。LOL。
> > 
> > 
> > 
---
> ## Priyanshu Joshi
> 
> モデルと中間テンソルへのすべての参照を正しくクリアしていることを確認してください。
> 
> ```
> import gc
> 
> gemma_model.cpu()
> del gemma_model
> torch.cuda.empty_cache()
> gc.collect()
> 
> ```
> 
> 推論環境で GPU を使用している他のプロセスがないことを確認してください。バックグラウンドプロセスが大量のメモリを消費することがあります。勾配チェックポイントを使用して、計算コストをメモリ使用量と交換してください。これにより、バックワードパス中にモデルの一部を再計算することでメモリを節約できます。Veletin がコメントで述べたように、バッチサイズと max_length を実験してください。[モデル並列化](https://huggingface.co/docs/transformers/v4.15.0/parallelism) を試すことができます。
> 
> 
> 
---
> ## Lorry Zouトピック作成者
> 
> 推論後に GPU 0 のメモリのみが解放されるのはなぜでしょうか。もしかしたら、推論中に実際に使用されているのはモデルの 1 つだけかもしれません。コード:
> 
> `@torch.no_grad()
> 
> [@torch.cuda.amp.autocast](https://www.kaggle.com/torch.cuda.amp.autocast)()
> 
> def gemma_inference(df, model, device, batch_size=cfg.batch_size, max_length=cfg.max_length):
> 
>     a_win, b_win, tie = [], [], []
> 
> ```
> for start_idx in range(0, len(df), batch_size):
>     end_idx = min(start_idx + batch_size, len(df))
>     tmp = df.iloc[start_idx:end_idx]
>     input_ids = tmp["input_ids"].to_list()
>     attention_mask = tmp["attention_mask"].to_list()
>     inputs = pad_without_fast_tokenizer_warning(
>         gemma_tokenizer,
>         {"input_ids": input_ids, "attention_mask": attention_mask},
>         padding=True,
>         max_length=max_length,
>         pad_to_multiple_of=None,
>         return_tensors="pt",
>     )
>     outputs = model(**inputs.to(device))
>     proba = outputs.logits.softmax(-1).cpu()
> 
>     a_win.extend(proba[:, 0].tolist())
>     b_win.extend(proba[:, 1].tolist())
>     tie.extend(proba[:, 2].tolist())
> 
>     df["winner_model_a"] = a_win
>     df["winner_model_b"] = b_win
>     df["winner_tie"] = tie
>     return df` and
> 
> ```
> 
> with ThreadPoolExecutor(max_workers=2) as executor:
>     gemma_results = executor.map(gemma_inference, (gemma_sub_1, gemma_sub_2), (gemma_model_0, gemma_model_1), (device_0, device_1))
> 
> また、`batch_size=4` と `2` も試しましたが、違いはありません。
> 
> 
> 
> > ## Valentin Werner
> > 
> > 実際に `gc.collect()` を使用していますか？ShelterW がコメントで説明したように、`gc.collect()` が実行されるまで解放されないことがありました。
> > 
> > 
> > 
> > > ## Lorry Zouトピック作成者
> > > 
> > > はい、`gc.collect()` を使用していますが、機能しません。
> > > 
> > > gemma_model_0.to('cpu')
> > > del gemma_model_0
> > > gc.collect()
> > > gemma_model_1.to('cpu')
> > > del gemma_model_1
> > > gc.collect()
> > > with torch.no_grad():
> > >     torch.cuda.set_device('cuda:0')
> > >     torch.cuda.empty_cache()
> > >     torch.cuda.set_device('cuda:1')
> > >     torch.cuda.empty_cache()
> > > 
> > > 
> > > 
---
> ## ShelterW
> 
> Gemma2 と Llama3 のアンサンブルを使用していたとき、さらに悪化しました。
> 
> ```
> import torch
> import gc
> del proba, model_0, model_1, test, data, aug_data
> gc.collect()
> torch.cuda.empty_cache()
> 
> ```
> 
> 
> 
> > ## Lorry Zouトピック作成者
> > 
> > メモリに残っているものがあり、削除し忘れていると思います…😆
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > これにより、両方の GPU が 300 MB 未満になります。それ以外の場合は、`max_length` と/または `batch_size` を小さくしてください。
> > > 
> > > 
> > > 
> > ## Allen Wang
> > 
> > あなたと同じ問題が発生しています。解決策はありますか？
> > 
> > 
> > 
---




</div>