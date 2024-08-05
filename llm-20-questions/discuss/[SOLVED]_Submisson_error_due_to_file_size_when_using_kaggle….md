# [SOLVED] Submisson error due to file size when using kaggle CLI in kaggle notebook

**c-number** *Fri Jun 28 2024 11:28:47 GMT+0900 (日本標準時)* (0 votes)

Hello,

I am working on the competition based on this [notebook](https://www.kaggle.com/code/robikscube/intro-to-rigging-for-llm-20-questions-llama3), but I get the following error when trying to submit from the notebook.

400 - Bad Request - Submission not allowed:  Your file exceeds the maximum size of 20 GB.

Does anyone know how to submit files larger than 20GB? or is the submission file limited to that size for this competition? (I couldn' t find such a statement though.)

Thank you in advance.



---

 # Comments from other users

> ## OminousDude
> 
> The file size is limited however files larger than ~ 8 GB won't have time to run on the Tesla T4s for submission. Try using a smaller model (guessing you used Gemma 2 🫣)
> 
> 
> 
> > ## c-numberTopic Author
> > 
> > Thanks, I was trying to upload several models (Gemma 2 is not one of them :) ) and run all of them for a single question.
> > 
> > Maybe I should upload the quantized weights directly.
> > 
> > 
> > 


---

> ## Sumo
> 
> [@cnumber](https://www.kaggle.com/cnumber) I'm a bit late to the party, but I saw you marked this thread as solved. How did you get around it? I'm running into the same issue
> 
> 
> 
> > ## c-numberTopic Author
> > 
> > Well, it's not actually solved, but I managed to fit 2 models in 20GB by quantizing them.
> > 
> > Hope this helps!
> > 
> > 
> > 
> > > ## Sumo
> > > 
> > > ah that's a shame. Thank you anyway!
> > > 
> > > offtopic, but we're looking for a teammate for this comp (and future competitions!), in case you're interested we'll be very happy to have you in our team :) 
> > > 
> > > 
> > > 
> > > ## OminousDude
> > > 
> > > Off topic but I am asking all of the top places about if they use the public lb keywords for their model. Does your team use them?
> > > 
> > > 
> > > 


---

> ## c-numberTopic Author
> 
> I'm having some trouble trying to submit 2 7B~8B models, so I really hope Kaggle would relax the submission file size restriction.
> 
> 
> 
> > ## OminousDude
> > 
> > I see the problem however is that on the Kaggle GPUs such a model would likely not have enough time (60 sec) to run
> > 
> > 
> > 
> > > ## c-numberTopic Author
> > > 
> > > Thanks for you advice, but currently I have no problems with running a single 7~8B model in the given computation time, and the log tells me that I might have time for another model.
> > > 
> > > 
> > > 


---

