# Scope of keywords.py

**Khoi Nguyen** *Thu May 16 2024 17:49:23 GMT+0900 (日本標準時)* (20 votes)

A few questions since there is no description (yet):

- Are the keywords there also the ones actually used for the first phase or are they just for debugging?

- Will the second phase (private test) contains categories outside of the 3 in there?



---

 # Comments from other users

> ## Duke Silver
> 
> It feels like public leaderboard doesn't really represent the private leaderboard very well.
> 
> 
> 
> > ## Chris Deotte
> > 
> > True. The solutions which are successful on public LB will be much different than successful models on private LB. (Because we have list of possible keywords for public LB but do not for private LB). None-the-less both offer learning opportunities for the other.
> > 
> > 
> > 
> > > ## Duke Silver
> > > 
> > > It seems like it could be better to train models on words outside of the keywords given as well to make the model more adaptive
> > > 
> > > 
> > > 


---

> ## Bovard Doerschuk-Tiberi
> 
> [@suicaokhoailang](https://www.kaggle.com/suicaokhoailang) We are considering a few options here on expanding the word list and giving guidance on categories for the second phase. We will make an announcement when it's decided.
> 
> 
> 


---

> ## Rob Mulla
> 
> I have similar questions. From what I gather reading the competition description and looking at the keywords used in games on the leaderboard:
> 
> - Current games look like they only use the subsection of keywords provided in keywords.py
> 
> - After the submission deadline there will be a new set of keywords used.
> 
> From the [evaluation section](www.kaggle.com/competitions/llm-20-questions/overview/evaluation): 
> 
> "At the submission deadline on August 13, 2024, submissions will be locked. From August 13, 2024 to August 27th, 2024 we will continue to run episodes against a new set of unpublished, secret words. At the conclusion of this period, the leaderboard is final."
> 
> This might mean that the "pre-deadline" leaderboard is going to be overfit to these words unfortunately.
> 
> 
> 
> > ## G John Rao
> > 
> > The keywords will be within those three categories? This is the real question that needs to be answered by the hosts
> > 
> > 
> > 
> > > ## Bovard Doerschuk-Tiberi
> > > 
> > > Stay tuned, we'll make an announcement to address this. Thank you!
> > > 
> > > 
> > > 
> > > ## Chandresh J Sutariya
> > > 
> > > any update??
> > > 
> > > 
> > > 


---

> ## alekh
> 
> Is the keyword.py file included in the environment? i.e. can i read it and feed it to my agent?
> 
> 
> 
> > ## Bovard Doerschuk-Tiberi
> > 
> > keyword.py is indeed contained in the kaggle-environment pip package. However I advise against using it, agents will not have access to the final list published after the submission deadline:
> > 
> > Final Evaluation
> > 
> >   At the submission deadline on August 13, 2024, submissions will be locked. From August 13, 2024 to August 27th, 2024 we will continue to run episodes against a new set of unpublished, secret words. At the conclusion of this period, the leaderboard is final.
> > 
> > 
> > 
> > > ## VolodymyrBilyachat
> > > 
> > > Will it be just new keywords in those categories or new categories too?
> > > 
> > > 
> > > 
> > > ## Gavin Cao
> > > 
> > > "agents will not have access to the final list published after the submission deadline."  does it mean agent could not read keyword.py after August 13? or the final list will be different from the content of  keyword.py?
> > > 
> > > 
> > > 


---

> ## Sheema Zain
> 
> Looks like there is just those 3 categories!
> 
> 
> 


---

> ## VolodymyrBilyachat
> 
> Looks like there is just those 3 categories
> 
> 
> 


---
