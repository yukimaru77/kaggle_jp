# Internet access condition

**Kamil Machalica** *Fri May 17 2024 21:07:02 GMT+0900 (日本標準時)* (1 votes)

Hi Kagglers!

If there is internet access restrictions can we even use pre-trained models to download them?

Thanks

Kamil



---

 # Comments from other users

> ## Valentin Werner
> 
> There are several things you can do, and what is often done:
> 
> 1) You can download the models, save them as kaggle dataset, load them from kaggle dataset instead (same goes for pip installs you might want to do)
> 
> 2) You can train models in one notebook with internet access, save the model checkpoint at the end and then create a separate notebook without internet access. Then you can simply add the training notebook as input for the inference notebook!
> 
> Hope this helps, welcome to kaggle and good luck!
> 
> 
> 
> > ## Kamil MachalicaTopic Author
> > 
> > Thank you, it explains a lot!
> > 
> > 
> > 


---

> ## Muhammad Tariq Pervez
> 
> [@machalx](https://www.kaggle.com/machalx), In Kaggle competitions, "disabling internet" means that the code you submit to Kaggle for scoring is executed in an environment that does not have access to the internet. Ensure your submission does not include any code that requires internet access, such as downloading data from external URLs or accessing online APIs.
> 
> Otherwise no issue. 
> 
> 
> 


---

