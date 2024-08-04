# How to use models from huggingface?

**Parashuram Chavan** *Fri Jun 21 2024 21:42:16 GMT+0900 (日本標準時)* (0 votes)

or can i use huggingface models by API 



---

 # Comments from other users

> ## Chris Deotte
> 
> ## Commit Code
> 
> During commit, download and save the models to folder
> 
> ```
> from transformers import AutoTokenizer, AutoModelForCausalLM
> model = AutoModelForCausalLM.from_pretrained()
> tokenizer = AutoTokenizer.from_pretrained()
> model.save_pretrained("/tmp/submission/weights")
> tokenizer.save_pretrained("/tmp/submission/weights")
> 
> ```
> 
> If you have any pip installs then install into /tmp/submission/lib
> 
> ```
> os.system("pip install -U -t /tmp/submission/lib PACKAGE")
> 
> ```
> 
> Then zip up the entire /tmp/submissions folder to submission.tar.gz. See Kaggle starter code for zip commands.
> 
> ## Submit Code
> 
> Then during submit inside your /tmp/submission/main.py file add the following (and all your pip installs and models will work):
> 
> ```
> import os
> KAGGLE_AGENT_PATH = "/kaggle_simulations/agent/"
> if not os.path.exists(KAGGLE_AGENT_PATH):
>     KAGGLE_AGENT_PATH = "/tmp/submission/"
> 
> import sys
> from transformers import AutoTokenizer, AutoModelForCausalLM
> sys.path.insert(0, f"{KAGGLE_AGENT_PATH}lib")
> model = AutoModelForCausalLM.from_pretrained(
>     f"{KAGGLE_AGENT_PATH}weights/")
> tokenizer = AutoTokenizer.from_pretrained(
>     f"{KAGGLE_AGENT_PATH}weights/")
> 
> ```
> 
> 
> 
> > ## Parashuram ChavanTopic Author
> > 
> > ohh thank you sir 
> > 
> > 
> > 


---

