# How can I use the latest version of the transformers library in the production environment?

**TomFuj** *Fri Jul 19 2024 01:04:06 GMT+0900 (日本標準時)* (2 votes)

Dear Kaggle Staff

The latest transformers library (ver 4.42.4) installed via pip in the Kaggle environment is being downgraded to ver 4.41.2 in the production environment and is not being reflected properly.

Could you please advise on the best way to use the latest transformers library in the production environment ?



---

 # Comments from other users

> ## Mitsutani
> 
> I'm having the same issue. Following to see if anyone has suggestions
> 
> 
> 


---

> ## JacobStein
> 
> Our team is experiencing the same issue. The old version of the transformers library is taking precedence over the newer one we installed during the build.
> 
> 
> 


---

> ## Chris Deotte
> 
> You can view my starter notebook to learn how to pip install packages to be used during submission [here](https://www.kaggle.com/code/cdeotte/starter-code-for-llama-8b-llm-lb-0-750)
> 
> 
> 
> > ## Mitsutani
> > 
> > I've tried using this setup but I'm running Gemma 2. I followed the same steps as in the notebook (changing sys.path etc), but when importing transformers in the production environment I get the older version too so it can't load Gemma 2. I think your main doesn't need transformers 4.42.4 so it runs fine, but correct me if I'm wrong.
> > 
> > 
> > 


---

