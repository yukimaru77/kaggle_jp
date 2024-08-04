# submissions get timeout?

**yechenzhi1** *Sun May 19 2024 11:28:12 GMT+0900 (日本標準時)* (6 votes)

Hi, I'm new to kaggle. I've submitted several times, all all my submissions failed due to timeout, but when I run it in my local Kaggle environment with T4*2 the inference time is as follows:

And I got a warning like this:

2024-05-19 01:36:52.192095: E external/local_xla/xla/stream_executor/cuda/cuda_dnn.cc:9261] Unable to register cuDNN factory: Attempting to register factory for plugin cuDNN when one has already been registered

  2024-05-19 01:36:52.192192: E external/local_xla/xla/stream_executor/cuda/cuda_fft.cc:607] Unable to register cuFFT factory: Attempting to register factory for plugin cuFFT when one has already been registered

  2024-05-19 01:36:52.309490: E external/local_xla/xla/stream_executor/cuda/cuda_blas.cc:1515] Unable to register cuBLAS factory: Attempting to register factory for plugin cuBLAS when one has already been registered

But I'm sure GPU is used during the inference.

Any help would be appreciated. 



---

 # Comments from other users

> ## yechenzhi1Topic Author
> 
> thanks everyone helped! Setting batch size=1 solved my problem😃
> 
> 
> 


---

> ## yechenzhi1Topic Author
> 
> Another question is that, when we score in the public leaderboard, is the test dataset about 25000 * 0.3 rows? And when tested in the private leaderboard, it's about 25000 * 0.7 rows?
> 
> 
> 
> > ## Kishan Vavdara
> > 
> > Yes, that's correct! 
> > 
> > 
> > 
> > ## Rich Olson
> > 
> > I'll add that assuming this is like most contests - you're notebook is always run for the entire private / public test set.  It's just the scores for the private data portion of the scores is revealed at the end of the contest.
> > 
> > 
> > 


---

> ## lijiang3859
> 
> Hey, [@yechenzhi1](https://www.kaggle.com/yechenzhi1). Thanks for your sharing! I also got this warning:
> 
> ```
>   warnings.warn(
> 2024-07-06 05:05:32.818151: E external/local_xla/xla/stream_executor/cuda/cuda_dnn.cc:9261] Unable to register cuDNN factory: Attempting to register factory for plugin cuDNN when one has already been registered
> 2024-07-06 05:05:32.818272: E external/local_xla/xla/stream_executor/cuda/cuda_fft.cc:607] Unable to register cuFFT factory: Attempting to register factory for plugin cuFFT when one has already been registered
> 2024-07-06 05:05:32.956771: E external/local_xla/xla/stream_executor/cuda/cuda_blas.cc:1515] Unable to register cuBLAS factory: Attempting to register factory for plugin cuBLAS when one has already been registered
> 
> ```
> 
> However, my program does not raise bugs. Is there any influence on it?  By setting batch_size=1, the warning is gone?
> 
> 
> 
> > ## yechenzhi1Topic Author
> > 
> > We can ignore this warning.
> > 
> > 
> > 


---

> ## lijiang3859
> 
> I think I also have the same issue with model=llama3-8B. Here is my script:
> 
> ```
> results = []
> df = pd.read_csv(args.test_file, dtype={'prompt': str, "response_a":str, "response_b":str})
> df.fillna("''", inplace=True)
> df.replace('null', "'null'", inplace=True)
> 
> eval_dataset = Dataset.from_pandas(df)
> length =  len(eval_dataset)
> for i in tqdm(range(length)): # batch_size = 1
>     data = eval_dataset[i]
>     idx = data["id"]
>     resp_a = template.format(data['prompt'], data['response_a'])
>     resp_b = template.format(data['prompt'], data['response_b'])
>     resp_tokens = tokenizer(
>         [resp_a, resp_b],
>         max_length=args.max_total_length,
>         padding=True,
>         truncation=True,
>         return_tensors="pt",
>     )
>     # concated responses to save inference time -> batch_size =2
>     output = model(resp_tokens)
> 
> ```
> 
> Here is some other settings to speed up the inference process:
> 
> use bf116=True for model initialization.
> use autocast() and
> 
> Is there any other process to speed up the inference? I have tested it with 25000 samples, it is very risky to excel the total training budget with 9hrs.
> 
> 
> 
> > ## yechenzhi1Topic Author
> > 
> > [https://www.kaggle.com/code/emiz6413/llama-3-8b-38-faster-inference](https://www.kaggle.com/code/emiz6413/llama-3-8b-38-faster-inference)  you can check this notebook to see if it can help.
> > 
> > 
> > 


---

> ## Valentin Werner
> 
> One Remark, the test data has 25000 samples, so this will 10x your runtime. Technically that is still less than 540 minutes, but it is a lot slower
> 
> 
> 
> > ## yechenzhi1Topic Author
> > 
> > yes, so the prediction time should be 40x10 minutes, that's about 7 hours,  so it shouldn't be timeout.
> > 
> > 
> > 


---

> ## Rich Olson
> 
> how many rows are you testing prediction with?
> 
> (when you score - it scores against 25,000)
> 
> 
> 
> > ## yechenzhi1Topic Author
> > 
> > I tested 2500 rows, it was about 40 minutes.
> > 
> > 
> > 
> > > ## Rich Olson
> > > 
> > > well - I can't think of anything obvious.  just assuming you aren't doing anything that takes a bunch of time before inference? (training / pre-processing / generating embeddings)?
> > > 
> > > if you run out of ideas - I would try to test the workflow as close as possible to submission.
> > > 
> > > I would load 25k rows from "train" into your "test" dataframe (and drop columns / etc to make it look like test).
> > > 
> > > Then - I would save a version of your notebook.  That will run it like it was getting submitted.
> > > 
> > > You should then be able to look at the logs (even if it times out before finishing).
> > > 
> > > Might want to try adding some logging / debug statements before doing.
> > > 
> > > 
> > > 


---

