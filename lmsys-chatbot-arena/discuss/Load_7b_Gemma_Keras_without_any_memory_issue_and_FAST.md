# Load 7b Gemma Keras without any memory issue and FAST.

**Marília Prata** *Sun May 12 2024 07:28:29 GMT+0900 (日本標準時)* (27 votes)

# A tip  to avoid memory issues while running your 1.1 -7b_instruct_en Gemma/Keras Model:

[Gemma 1.1 7B Int8 Load](https://www.kaggle.com/code/awsaf49/gemma-1-1-7b-int8-load) By Awsaf.

On the last topic (2 days ago ), I asked "How to work with Gemma Keras 1.1- 7b instruct-en WITHOUT your Kaggle Notebook being restarted cause you've allocated more memory than is avaiable. Then we should opt to Google Cloud or dismiss our work.

Some answers that I got to that previous topic:  I read/learned  that reducing batches and max_length could help me to load the model and face the memory issue.  Not always, it's a 7b (7 billion parameters model).

But, what if we don't have max_lenght and batches written on our Kaggle Notebook script? Sometimes it happens. Therefore, it's great to have a Plan B:

Fortunately, I found Awsaf's code and published my 1st Gemma 1.1-7b-instruct-en.  

So, take a look and check Awsaf's amazing, cristal clear code:

[Gemma 1.1 7B Int8 Load](https://www.kaggle.com/code/awsaf49/gemma-1-1-7b-int8-load) By Awsaf.

For the record, there aren't many 7b Gemma Keras  Kaggle Notebooks. Though we can find plenty of 2b Models.



---

 # Comments from other users

> ## Adnan Alaref
> 
> Good news for find solution, thanks for sharing  [@mpwolke](https://www.kaggle.com/mpwolke) 
> 
> 
> 
> > ## Marília PrataTopic Author
> > 
> > Indeed Alaref,
> > 
> > I was so happy that I was able to work with Gemma/Keras 1.1-7b_instruct-en without any memory issue that I felt that I should share this topic because very few showed appreciation to Awsaf's code (till yesterday he had only 6 votes for such a remarkable and useful code and  his 2 datasets.  
> > 
> > Maybe, kagglers didn't realize the importance of that code.
> > 
> > For the record, the Notebook ran in only GPU 15 minutes!  Isn't that great?
> > 
> > Besides, I was able to deliver the last Model that the hosts had pinned on this competition.
> > 
> > Not many users are working with 1.1_7b_instruct. In fact, I didn't read any other, except Awsaf's code.
> > 
> > It was almost my "Moby Dick" of models.
> > 
> > Thank you Alaref.
> > 
> > 
> > 


---

