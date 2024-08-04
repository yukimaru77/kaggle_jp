# how can I load a pretrained model with internet off

**Dirk N** *Tue May 14 2024 23:56:23 GMT+0900 (日本標準時)* (2 votes)

It seems I cannot use pip install, what is the best way to load a pretrained model with internet off?



---

 # Comments from other users

> ## RobsonDSP
> 
> I tried download a model from huggingface but until now is not working. I cloned the model to my local machine and uploaded it to my private space here on Kaggle as dataset. I uploaded all files, config.json, tf_model.h5, vocab.json and others. I tried to load them using the code bellow:
> 
> from transformers import AutoModelForSequenceClassification
> 
> from transformers import TFAutoModelForSequenceClassification
> 
> from transformers import AutoTokenizer, AutoConfig
> 
> import numpy as np
> 
> from scipy.special import softmax
> 
> MODEL = f"/kaggle/input/pretrained-model-from-huggingface/"
> 
> tokenizer = AutoTokenizer.from_pretrained(MODEL)
> 
> config = AutoConfig.from_pretrained(MODEL)
> 
> model = AutoModelForSequenceClassification.from_pretrained(MODEL)
> 
> Now I'm getting the following error message:
> 
> OSError: You seem to have cloned a repository without having git-lfs installed. Please install git-lfs and run git lfs install followed by git lfs pull in the folder you cloned.
> 
> When I run the commands in my machine it starts to download a huge file. I stopped at 1GB and the progress bar at 0%. I intended to upload this file to my account on Kaggle too but I stopped because I'm probably doing something wrong. 
> 
> I really don't know what to do now because I cannot enabled the internet access.
> 
> 
> 


---

> ## Muhammad Tariq Pervez
> 
> [@dirknbr](https://www.kaggle.com/dirknbr), Kaggle competition rules don't impose restrictions to download a model and use it. In Kaggle competitions, "disabling internet" means that the code you submit to Kaggle for scoring is executed in an environment that does not have access to the internet. Ensure your submission does not include any code that requires internet access, such as downloading data from external URLs or accessing online APIs.
> 
> 
> 


---

> ## Kishan Vavdara
> 
> Keep train and inference separate notebooks, download/load/train model in train notebook and import it in inference notebook. 
> 
> 
> 


---

> ## djchen
> 
> You can download the pertrained model on huggingface and upload it to Kaggle as a model, then you can load such pertrained model in your notebook.
> 
> 
> 


---

> ## Simon Veitner
> 
> You can clone the huggingface repository and upload it as a dataset. There are many examples how to load it from there.
> 
> Also you should check, if somebody else did it already :)
> 
> 
> 


---

