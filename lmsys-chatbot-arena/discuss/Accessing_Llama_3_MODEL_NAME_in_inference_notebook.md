# Accessing Llama 3 MODEL_NAME in inference notebook

**JamshaidSohail** *Mon Jul 15 2024 00:07:29 GMT+0900 (日本標準時)* (1 votes)

Hi. I have successfully run the amazing [TPU Llama 3 training notebook](https://www.kaggle.com/code/kishanvavdara/lmsys-llama-3-tpu-train) by [@kishanvavdara](https://www.kaggle.com/kishanvavdara) and now I am trying to run the inference notebook. I have already been given access to the Llama 3 usage both on hugging face and meta official page and I have the corresponding hugging face token as well and weights file as well. When I try to run the [inference notebook](https://www.kaggle.com/code/kishanvavdara/inference-llama-3-8b), i get the below error 

OSError: Incorrect path_or_model_id: '/kaggle/input/llama-3/transformers/8b-chat-hf/1'. Please provide either the path to a local folder or the repo_id of a model on the Hub.

Internet access is off in the inference notebook. So I cannot use MODEL_NAME="meta-llama/Meta-Llama-3-8B-Instruct" like I did in training notebook which downloads the model from scratch from hugging face hub. Any sort of help would be highly appreciated. [@valentinwerner](https://www.kaggle.com/valentinwerner) 



---

 # Comments from other users

> ## Valentin Werner
> 
> First, you also need to request Llama Access on Kaggle, you can do so by following the model link. Then, make sure you have the llama model added as model in the notebook, then the path will be exactly right.
> 
> 
> 
> > ## JamshaidSohailTopic Author
> > 
> > So I already got access to the Llama model via using the official Meta page and now I submitted the form via the Kaggle. I hope it gets approved quickly and I can move fast :D. Thank you so much once again.
> > 
> > 
> > 
> > > ## JamshaidSohailTopic Author
> > > 
> > > Thank you [@valentinwerner](https://www.kaggle.com/valentinwerner). I have been granted access and I am able to do the inference :D
> > > 
> > > 
> > > 
> > > ## Valentin Werner
> > > 
> > > Amazing, that you got it within the hour on a saturday! Some people reported waiting times of 24+ hours. Best of luck with your training - toi toi toi 😉
> > > 
> > > 
> > > 


---

