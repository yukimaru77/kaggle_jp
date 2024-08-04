# How to add custom python packages in the submission?

**sakura** *Tue Jun 04 2024 21:04:34 GMT+0900 (日本標準時)* (2 votes)

Hi, all. I'm a new hand to Kaggle. I want to know how can I know what packages are in the online evaluation, and whether I can add new packages (for example, from pip install). It seems that this can be done through submitting a notebook. I'm wondering if I can add custom packages through submitting the tar file? (Such as adding an requirements.txt?). Thanks for any help and response!



---

 # Comments from other users

> ## VolodymyrBilyachat
> 
> pip install -q -U -t /kaggle/working/submission/lib your package
> 
> I was using this
> 
> 
> 
> > ## sakuraTopic Author
> > 
> > Hi, thanks for your response! But if I need to submit a main.py file, where should I put this line in?😀
> > 
> > 
> > 
> > > ## Chris Deotte
> > > 
> > > Hi. Put your main.py file in /kaggle/working/submission/lib and pip install everything into /kaggle/working/submission/lib. Then finally tarball the entire folder /kaggle/working/submission/lib. Afterward submit the tarball to the competition.
> > > 
> > > Also note that inside your main.py file you will need to add to system path so that it can find your pip installs:
> > > 
> > > ```
> > > KAGGLE_AGENT_PATH = "/kaggle_simulations/agent/"
> > > if os.path.exists(KAGGLE_AGENT_PATH):
> > >     sys.path.insert(0, os.path.join(KAGGLE_AGENT_PATH, 'lib'))
> > > else:
> > >     sys.path.insert(0, "/kaggle/working/submission/lib")
> > > 
> > > ```
> > > 
> > > To see an example of tarballing, see code cell #3 and #4 in starter notebook [here](https://www.kaggle.com/code/ryanholbrook/llm-20-questions-starter-notebook). Afterward we submit submission.tar.gz to the competition.
> > > 
> > > 
> > > 
> > > ## sakuraTopic Author
> > > 
> > > I understand now. Thanks a lot!
> > > 
> > > 
> > > 


---

