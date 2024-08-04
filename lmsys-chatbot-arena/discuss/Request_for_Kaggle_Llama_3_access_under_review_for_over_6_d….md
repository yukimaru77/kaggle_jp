# Request for Kaggle Llama 3 access under review for over 6 days [Solved]

**Allie K.** *Mon Jul 08 2024 20:18:16 GMT+0900 (日本標準時)* (5 votes)

On Friday early morning MDT I submitted request for Llama 3 and Llama 2 access first via Meta website (of course with the same email address as I have on Kaggle) and I was granted the access in a minute.

Immediately I successfully submitted request to access Llama 3 model via Kaggle. 

Now, after more than 6 days, the request is still "pending a review from the authors".

As it can be seen from the discussion under the model, I am not alone in this desperate situation.

[@addisonhoward](https://www.kaggle.com/addisonhoward) is the access to the model on Kaggle somehow restricted? 

In this case all the competition wouldn't be fair at all. It isn't fair even now, because I couldn't make submission with Llama 3 for 3 days due to problems on Kaggle side.  

Edited:

And suddenly, after "only" 6 days a magic happened and the access is granted.

The magic seems to be triggered by another discussion thread.



---

 # Comments from other users

> ## CPMP
> 
> Reading this only now. It is wrong that your post did not have effect until mine. 
> 
> 
> 


---

> ## RB
> 
> I downloaded Transformer weights for Gemma (since they are not [yet available on Kaggle](https://www.kaggle.com/models/google/gemma-2/discussion/516164)) You can do the same for Llama as well 
> 
> Following code will save weights in /kaggle/working directory of your kernel. You do need read access token from Huggingface and your request must be approved there.
> 
> Typically I found process is much faster when the models are released, so apply even if you are not planning to use it. 
> 
> ```
> import os
> os.environ["HF_HUB_ENABLE_HF_TRANSFER"] = "1"
> 
> from kaggle_secrets import UserSecretsClient
> user_secrets = UserSecretsClient()
> secret_value_0 = user_secrets.get_secret("HF_TOKEN")
> 
> from huggingface_hub import  snapshot_download, login
> login(token=secret_value_0, add_to_git_credential=False)
> 
> ## Download model from HuggingfaceHub
> ## https://huggingface.co/google/gemma-2-9b-it/tree/main
> 
> snapshot_download(repo_id="google/gemma-2-9b-it", 
>                   revision="main", 
>                   repo_type="model",
>                   allow_patterns="*",
>                   local_dir = "/kaggle/working/", 
>                   ignore_patterns="consolidated.safetensors")
> 
> ```
> 
> 
> 
> > ## BladeRunner
> > 
> > This approach seems to only support models with weight files under 20GB, because of the capacity cap of /kaggle/working/, I wonder how it should be handled for models 13b and above?😀
> > 
> > 
> > 
> > > ## RB
> > > 
> > > You can download in /tmp directory - I think there's 50+ GB space available there. 
> > > 
> > > From /tmp you can upload to a Kaggle Dataset with [Kaggle API  ](https://github.com/Kaggle/kaggle-api/blob/main/docs/README.md#datasets)
> > > 
> > > 
> > > 


---

> ## sayoulala
> 
> [https://www.kaggle.com/datasets/junglebeastds/llama3instruct](https://www.kaggle.com/datasets/junglebeastds/llama3instruct) .Someone upload the model here
> 
> 
> 


---

> ## Allie K.Topic Author
> 
> Big thanks to everybody who suggested me (and hopefully not only to me) a solution how to solve the unpleasant situation. I could start submitting.
> 
> Anyway I hope that Kaggle team will restore the broken Llama 3 access pipeline in a reasonable time, not only after the competition ends. 
> 
> 
> 


---

> ## Pamin
> 
> Same, 3 days ago.
> 
> 
> 


---

> ## hn
> 
> Same here actually. 
> 
> 
> 


---

> ## Valentin Werner
> 
> This is wild, it has been approved for me within 10 minutes on a weekend
> 
> 
> 


---

> ## Xinyuan Qiao
> 
> Just do it again, I got same situation before.
> 
> 
> 


---

> ## Arindam Roy
> 
> Same here 
> 
> 
> 


---

> ## samson
> 
> You can get an access via [meta's webpage](https://llama.meta.com/) or directly on [huggingface](https://huggingface.co/meta-llama/Meta-Llama-3-8B), then download the weights and upload all the stuff as a private dataset on Kaggle. Its much faster! Basically minutes (I have submitted a request for model access via Kaggle 4 days ago and still waiting)
> 
> 
> 


---

