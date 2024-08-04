# Can I use model which is not in kaggle ? 

**AlphaTT30** *Sat Jun 29 2024 08:42:50 GMT+0900 (日本標準時)* (1 votes)

In this competition, internet access is not allowed. So I can't use hugging face pre-trained transformer models like this one. The submission gets an error, I think for this one. This needs to be downloaded 

```
# Load model directly
from transformers import AutoTokenizer, AutoModelForMaskedLM

tokenizer = AutoTokenizer.from_pretrained("google-bert/bert-base-uncased")
model = AutoModelForMaskedLM.from_pretrained("google-bert/bert-base-uncased")

```

So what to do? 

Are all the hugging face models in kaggle? 

should I use a model that exists on Kaggle? 

or is there another way to use this one? 



---

 # Comments from other users

> ## tanaka
> 
> You can download these kind of Bert related things and llms before internet ristriction.
> 
> Major topic of these competition is
> 
> Training llm or nlp related model using some techniques and gpus (it is updated to you)
> 
> And then use these models as inference models without internet.
> 
> 
> 


---

> ## Yichuan Gao
> 
> If the model license permits, you can just download the model from huggingface and upload it to kaggle as a model, then add it to your notebook
> 
> 
> 
> > ## AlphaTT30Topic Author
> > 
> > Can I train a model outside kaggle and then upload here and use that model for this competition?  
> > 
> > 
> > 
> > > ## Ravi Ramakrishnan
> > > 
> > > Yes of course, this is a preferred way to handle these competitions [@alphatt30](https://www.kaggle.com/alphatt30) 
> > > 
> > > 
> > > 
> > ## Ivel afred
> > 
> > Does this mean that your model needs to be made public on Kaggle? Or is it okay to just make it public on Hugging Face.
> > 
> > 
> > 
> > > ## Yichuan Gao
> > > 
> > > You don't need to upload your model to huggingface, just upload it here on kaggle is ok. Also you can make it private (by default) and use it in your notebooks
> > > 
> > > 
> > > 
> > > ## Ivel afred
> > > 
> > > Code Requirements in LMSYS states: 'Freely&publicly available external data is allowed, including pre trained models.' Does this not require your models to be public? I'm a little confused
> > > 
> > > 
> > > 


---

