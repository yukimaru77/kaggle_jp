# Getting error in sumbission.

**AlphaTT30** *Sun Jun 30 2024 21:56:50 GMT+0900 (日本標準時)* (1 votes)

Notebook successfully rans but then getting error like this 

[no idea what's going no or why happening this ] 

What to do now ? 

You're using a BertTokenizerFast tokenizer. Please note that with a fast tokenizer, using the __call__ method is faster than using a method to encode the text followed by a call to the pad method to get a padded encoding.

89.2s    2   /opt/conda/lib/python3.10/site-packages/traitlets/traitlets.py:2930: FutureWarning: --Exporter.preprocessors=["remove_papermill_header.RemovePapermillHeader"] for containers is deprecated in traitlets 5.0. You can pass --Exporter.preprocessors item … multiple times to add items to a list.

89.2s    3     warn(

89.2s    4   [NbConvertApp] WARNING | Config option kernel_spec_manager_class not recognized by NbConvertApp.

89.3s    5   [NbConvertApp] Converting notebook notebook.ipynb to notebook

89.7s    6   [NbConvertApp] Writing 32587 bytes to notebook.ipynb

91.3s    7   /opt/conda/lib/python3.10/site-packages/traitlets/traitlets.py:2930: FutureWarning: --Exporter.preprocessors=["nbconvert.preprocessors.ExtractOutputPreprocessor"] for containers is deprecated in traitlets 5.0. You can pass --Exporter.preprocessors item … multiple times to add items to a list.

91.3s    8     warn(

91.3s    9   [NbConvertApp] WARNING | Config option kernel_spec_manager_class not recognized by NbConvertApp.

91.3s    10  [NbConvertApp] Converting notebook notebook.ipynb to html

92.2s    11  [NbConvertApp] Writing 319012 bytes to results.html



---

 # Comments from other users

> ## Anya
> 
> Same situation. Waiting for resolution🤷‍♂️
> 
> 
> 
> > ## Anya
> > 
> > [https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/511861](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/511861)
> > 
> > There is a similar tag, you can check if it helps.
> > 
> > 
> > 
> > > ## AlphaTT30Topic Author
> > > 
> > > I solved my problem. Do you need a solution? 
> > > 
> > > 
> > > 


---

