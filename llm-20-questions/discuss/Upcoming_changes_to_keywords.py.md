# Upcoming changes to keywords.py

**Bovard Doerschuk-Tiberi** *Sat Jun 01 2024 08:35:32 GMT+0900 (日本標準時)* (21 votes)

There will be a few changes to keywords.py (this is the list of possible words to guess for the game).

Categories will be simplified into person, place, or thing.
Change will happen next week (first week of June)
Half way through the competition more words will be added

As stated in the rules, after the FINAL submission deadline, the words will be swapped for a set that is NOT accessible by your agents. This word set will have the same 3 categories

IMPORTANT: Do not rely on knowing the full list of possible words ahead of time!

EDIT: This will now roll out early next week, sorry for the delay!

This has been implemented, see details here: [https://www.kaggle.com/competitions/llm-20-questions/discussion/512955](https://www.kaggle.com/competitions/llm-20-questions/discussion/512955)



---

 # Comments from other users

> ## Adam Kulik
> 
> I have a question regarding person and place category. Will it always be a specific person or place, or can it be generic, e.g. a doctor, a plumber?
> 
> 
> 
> > ## OminousDude
> > 
> > I also wanted to know this I used to think it would be specific people's names (celebrities, influencers, etc) but now I believe it will be occupations. On the other hand occupations aren't people but jobs so I am completely dumbfounded on this topic.😂
> > 
> > 
> > 


---

> ## David
> 
> Would the formatting of the keywords change after final submission deadline? Like can we always expect it to be no more than 2 words? Can we ever expect things like "Guinea-Bissau" with hyphens?
> 
> 
> 
> > ## RS Turley
> > 
> > In the code for the competition, it looks like punctuation and capitalization are ignored when comparing guesses to the keyword, so hyphens shouldn't matter. Here is the code used:
> > 
> > ```
> > def keyword_guessed(guess: str) -> bool:
> >     def normalize(s: str) -> str:
> >       t = str.maketrans("", "", string.punctuation)
> >       return s.lower().replace("the", "").replace(" ", "").translate(t)
> > 
> >     if normalize(guess) == normalize(keyword):
> >       return True
> >     for s in alts:
> >       if normalize(s) == normalize(guess):
> >         return True
> > 
> >     return False
> > 
> > ```
> > 
> > 
> > 


---

> ## mhericks
> 
> Can we assume that keywords.py and the keywords used for the evaluation of the private leaderboard are a random partition of a "large" dataset, i.e. keywords.py contains a random sample of a dataset and the remaining keywords are used for the private evaluation?
> 
> Especially, can we assume that the distribution of keywords among categories is the same between the two subsets?
> 
> 
> 


---

> ## Lucas Fernandes
> 
> Hi, what do you mean by 'thing' for example would a dog be a 'thing' or is that a word that won't be apart of the dataset.
> 
> Thank you 
> 
> 
> 
> > ## Bovard Doerschuk-Tiberi
> > 
> > Yes, a dog would count in the "thing" category.
> > 
> > I don't have a precise definition of what will count as a thing, but when you see the released word list you'll have a better idea. Generally a thing should be a physical object or being (like a rock or dog), not an abstract concept (like GDP)
> > 
> > 
> > 


---

> ## Saatvik Pradhan
> 
> Thats great
> 
> 
> 


---

> ## Rafael Yakupov
> 
> Hello, thank you very much for the information. I have a question, will the categories remain the same after changing the word set after FINAL submission deadline?
> 
> 
> 
> > ## Bovard Doerschuk-Tiberi
> > 
> > yes, the categories will always be person, place, or thing going forward
> > 
> > 
> > 
> > > ## AAElter
> > > 
> > > The 20 questions game I played when young was animal, vegetable, or mineral.  With this game, I would think "thing" (oh, Thing!) would encompass all animals except humans, vegetables and minerals, and manmade objects made out of those things.
> > > 
> > > 
> > > 


---

