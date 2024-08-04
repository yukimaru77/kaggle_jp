# Comments 

> ## Samar Elhissi
> 
> Thank you for the example, how to test it locally?
> 
> 
> 
> > ## Valentin Baltazar
> > 
> > Check if you have the hardware for it…these LLM require a lot of computation and a powerful GPU to train and fine tune. I would use the cloud, much easier too.
> > 
> > 
> > 


---

> ## Michael Kamal 92
> 
> thank you, i want ask about few_shot_examples, i should be make like any one 
> 
> like this    ( 'is it place ?', 'yes-or-no')
> 
> or this    ('is it place ?', 'yes',)
> 
> or this     ('is it place ?', 'yes', 'Now guess the keyword')
> 
> or this     ('is it place ?', 'no', 'Now guess the keyword', 'France')
> 
> or this     ('is it place ?', 'yes', 'France')
> 
> any one correct to make question, answer and guess ?
> 
> and another question 
> 
> Gemma train on few_shot_examples ?
> 
> 
> 


---

> ## Yukky_2801
> 
> Hello, i am a starter to kaggle, when i run your notebook
> 
> I got error below:
> 
> tar: gemma/pytorch/7b-it-quant/2: Cannot stat: No such file or directory
> 
> 1.37MiB 0:00:00 [36.4MiB/s] [<=> ]
> 
> tar: Exiting with failure status due to previous errors
> 
> I cannot submit submission.tar.gz with error. 
> 
> I have no idea of this, could you please provide me solution?
> 
> 
> 
> > ## Andres H. Zapke
> > 
> > Obviously you are trying to access this path "gemma/pytorch/7b-it-quant/2". Make sure you have files in that path (look at the right side of the notebook, if you have the gemma model there, copy the path, do they match?
> > 
> > 
> > 
> > ## Aryan Singh
> > 
> > Add the model Gemma 7b-it-quant V2 using the Add Input function. 
> > 
> > Make sure to accept the license first from here: [https://www.kaggle.com/models/google/gemma](https://www.kaggle.com/models/google/gemma)
> > 
> > 
> > 
> > > ## Talal Mufti
> > > 
> > > after ensuring all files where in the path I still faced issues so I edit the bash commands slightly. personally, this worked better for me:
> > > 
> > > !tar --use-compress-program='pigz --fast --recursive | pv' -f submission.tar.gz -c /kaggle/working/submission . -c /kaggle/input/gemma/pytorch/7b-it-quant/2
> > > 
> > > 
> > > 


---

> ## Muhammad Hadi13
> 
> I don't know why I am just copying this file and running and it's note generating an output of more than 1.35 MB which is always failing in the validation episode. where as output for Ryan was around 7GB. Need help!!!
> 
> 
> 
> > ## Muhammad Hadi13
> > 
> > tar: gemma/pytorch: Cannot stat: No such file or directory
> > 
> > 1.37MiB 0:00:00 [36.4MiB/s] [<=>                                               ]
> > 
> > tar: Exiting with failure status due to previous errors
> > 
> > this error occurs for the submission cell block
> > 
> > 
> > 
> > > ## Aryan Singh
> > > 
> > > You need to add Gemma 7b-it-quant V2 first before running the code. 
> > > 
> > > Use Add input functionality in the notebook to add a model. 
> > > 
> > > Make sure to accept the license first from here: [https://www.kaggle.com/models/google/gemma](https://www.kaggle.com/models/google/gemma)
> > > 
> > > 
> > > 


---

> ## Ship of Theseus
> 
> Thank Ryan, greate work! Nice code to run on localhost and sharing to Kaggle Community
> 
> 
> 


---

> ## shiv_314
> 
> Hey folks! Need one help. I am facing an import error for gemma package.
> 
> I have already added the correct system path for python, however I am still facing the same issue. Kindly help!
> 
> 
> 


---

> ## dedq
> 
> Thank Ryan, greate work! Nice code to run on localhost and sharing to Kaggle Community
> 
> 
> 


---

> ## Code Hacker
> 
> I try submit this notebooks output file tar.gz, it failed…
> 
> 
> 
> > ## Code Hacker
> > 
> > I did'n agree model. Click red button as below…
> > 
> > 
> > 


---

> ## JAPerez
> 
> Great work Ryan!
> 
> 
> 


---

> ## philipha2
> 
> Hello I am a beginner in this competition. 
> 
> I was trying to run your notebook and make a submission.
> 
> where do i have to put submission.tar.gz file? 
> 
> After clicking submit agent button, Should I just submit this file? 
> 
> It takes quite a while
> 
> My questions may sound a bit basic but I would thank you alot for replying! 
> 
> 
> 
> > ## Kanchan Maurya
> > 
> > Submitting the file after clicking on Submit agents does the work.It takes a while since the initial simulations are working
> > 
> > 
> > 


---

> ## vj4science
> 
> Thanks Ryan - this is a good head start to the competition! much appreciated!
> 
> 
> 


---

> ## gb_kwon
> 
> Thank you so much for your COOL guidelines!
> 
> 
> 


---

> ## Andres H. Zapke
> 
> In your main.py, you import gemma_pytorch library with: from gemma.config.
> 
> This is not working for me, although import gemma gives no error.
> 
> Have tried everything from manually specifying my local gemma module's path or just importing by python library name. Any ideas ?
> 
> 
> 


---

> ## Duy Thai
> 
> Hello [@ryanholbrook](https://www.kaggle.com/ryanholbrook), I tried your notebook and got the message "An attached model requires additional steps to be accessed. See the Models panel for details.". What should I do about it?
> 
> When I opened the panel I only see this:
> 
> 
> 
> > ## Andres H. Zapke
> > 
> > Go to "Models" in Kaggle, search for Gemma, accept the Model's license.
> > 
> > 
> > 
> > > ## Duy Thai
> > > 
> > > Thank you!
> > > 
> > > 
> > > 


---

> ## Kai_Huang
> 
> hello, i am a starter to kaggle, when i run your code block of !tar --use-compress-program='pigz --fast --recursive | pv' -cf submission.tar.gz -C /kaggle/working/submission . -C /kaggle/input/ gemma/pytorch/7b-it-quant/2
> 
> i got this error:
> 
> tar: gemma/pytorch/7b-it-quant/2: Cannot stat: No such file or directory
> 
> 1.37MiB 0:00:00 [36.4MiB/s] [<=>                                               ]
> 
> tar: Exiting with failure status due to previous errors
> 
> i have no idea of this, could you please tell me what's wrong with it? thanks!
> 
> 
> 
> > ## Kai_Huang
> > 
> > Oh, i got it, i did'n input a model to my notebook😱
> > 
> > 
> > 
> > ## D Prince Armand KOUMI
> > 
> > no model surely, try to add one
> > 
> > 
> > 


---

> ## Qusay AL-Btoush
> 
> it`s very good Ryan 
> 
> 
> 


---

