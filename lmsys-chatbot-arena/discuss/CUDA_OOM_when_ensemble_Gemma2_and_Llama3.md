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

