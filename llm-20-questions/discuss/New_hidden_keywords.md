# New hidden keywords

**Bovard Doerschuk-Tiberi** *Thu Jun 27 2024 09:37:42 GMT+0900 (日本標準時)* (10 votes)

As of now, some of the keywords are pulled from a hidden test set. In this set there are 500 location (from keywords.py), 500 things (from keywords.py), and 1000 new things (the hidden set).

We will reveal the full list of these hidden keywords in a few weeks (and possibly add more). That said we hope to minimize changes to the keyword set and keep these as representative as possible of the final dataset.

We will continue to monitor the leaderboard and agents to make sure we have a robust competition. 

Good luck and happy Kaggling!



---

 # Comments from other users

> ## Sumo
> 
> [@bovard](https://www.kaggle.com/bovard) Sorry if this is already answered somewhere, I've checked all other threads and I'm still confused. So I figured asking this here for me + other people reading this in the future:
> 
> Can you confirm to us which of this is the case for this competition?
> 
> - public LB is from keywords.py + a hidden set of keywords. Private LB is from this same set of hidden keywords
> 
> - public LB is from keywords.py + a hidden set of keywords. Private LB is from a totally different of hidden keywords
> 
> - other?
> 
> Thank you
> 
> 
> 
> > ## Naive Experimentalist
> > 
> > i would bet for the 2nd option
> > 
> > 
> > 
> > ## Bovard Doerschuk-Tiberi
> > 
> > The private LB is from the same set of hidden keywords. Though none of them will be re-used for the final evaluation
> > 
> > 
> > 


---

> ## DJ Sterling
> 
> We've removed the large majority of location keywords due to typos, obscurity, and to help address existing stale agents which were hardcoded for those targets.  We will consider adding new entries to the place category soon as well.
> 
> 
> 


---

> ## Max Brown
> 
> If you've already added these 'hidden set' keywords to the set of keywords that are currently being used during matchups, then what stops us from gleaning them by looking at/scraping the episode replays? Thanks!
> 
> edit: also, the keywords.py file in the "Data" section of this competition only has categories for countries, cities, and landmarks. Where can we see the list of "things"? EDIT: Here is a link to a version of keywords.py that is more complete than the one currently in the Data section of this competition:
> 
> [https://github.com/Kaggle/kaggle-environments/blob/master/kaggle_environments/envs/llm_20_questions/keywords.py](https://github.com/Kaggle/kaggle-environments/blob/master/kaggle_environments/envs/llm_20_questions/keywords.py)
> 
> 
> 
> > ## Matthew S Farmer
> > 
> > Check out the kaggle environment GitHub repo. 
> > 
> > 
> > 


---

> ## Jasper Butcher
> 
> Does this mean once these new keywords are released, the final test set will be the same?
> 
> 
> 


---

> ## VassiliPh
> 
> how the current keyword list was obtained from the full future keyword list?
> 
> I could imagine at least four possible situations:
> 
> Situation 1: Random sampling
> 
> You had a full list of keywords for the future final validation you you randlomly sampled 1000 keywords from it to make the currently used list of keywords.
> 
> It means we can assume that ratio of different groups (countries, cities, mountains, rivers, houshold items, etc) in the final keyword list will be the same as in the currently used 1000 keywords.
> 
> Situation 2: Random sampling from different groups
> 
> You had a full list of keywords for the future final validation as a list of groups (countries, cities, mountains, rivers, houshold items, etc) and you randomly sampled some amoung from each group to get the currently used 1000 keywords.
> 
> It means we can assume that all main groups that will be used in the final keyword list are represented in the current used 1000 keywords but their ratio can be different.
> 
> Situation 3: Taking some groups
> 
> You had a full list of keywords for the future final validation as a list of groups (countries, cities, mountains, rivers, houshold items, etc) and you took come of those groups to get the currently used 1000 keywords.
> 
> It means that groups used in the current keyword list will be taken as it for the future final keyword list but some new groups can be added.
> 
> Situation 4: Soemthing else
> 
> Thank you for answering, this information is indeed critically important to design any reasonable solution.
> 
> 
> 


---

> ## riju3107
> 
> Hey wanted to ask, what are we guessing? Is it limited to places and locations? or are we guessing people? This would be helpful for designing the chatbot. 
> 
> 
> 


---

> ## Marcel0.
> 
> When the final set of words is added and the submissions closed, will they be accessible on the keyword.py file? If so, even if I couldn't modify my code, I could build it to consider only the possibilities in this file.
> 
> 
> 
> > ## Naive Experimentalist
> > 
> > As per my understanding the hidden set of keywords will not be accessible on the keyword. However as more and more people doubt, it is more and more important to answer it clearly by Kaggle team. Their answer may have a great impact on how people implement their solutions.
> > 
> > 
> > 
> > ## Bovard Doerschuk-Tiberi
> > 
> > No, they will not be accessible in the keywords.py file
> > 
> > 
> > 
> > > ## sayoulala
> > > 
> > > Let me confirm my understanding: this means we will not have access to the final keywords, but the final keywords come from the same source as the current leaderboard keywords, correct?
> > > 
> > > 
> > > 


---

> ## Muhammad
> 
> Can we consider the Temple, Effil Tower, Pyramids, etc as a place?
> 
> 
> 


---

> ## Matthew S Farmer
> 
> Will 'person' be added as a category at some point? 
> 
> 
> 
> > ## Matthew S Farmer
> > 
> > Nevermind, I saw this answered elsewhere. 
> > 
> > 
> > 
> > > ## Naive Experimentalist
> > > 
> > > What answer have you found? As per my observation, persons appear in the competition, despite it has been said they would not.
> > > 
> > > 
> > > 
> > > ## OminousDude
> > > 
> > > I saw your discussion about this is just a typo or mistake
> > > 
> > > 
> > > 


---

