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


