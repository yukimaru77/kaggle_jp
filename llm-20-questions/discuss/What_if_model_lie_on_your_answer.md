# What if model lie on your answer?

**VolodymyrBilyachat** *Sun May 19 2024 08:36:24 GMT+0900 (日本標準時)* (0 votes)

Going through the logs i see that there is not negative reward if answerer lie.

That way the game is a bit odd even if questioner  ask reasonable question lies from answerer can redirect you to wrong path.



---

 # Comments from other users

> ## Chris Deotte
> 
> It is my understanding that the questioner and answerer are teammates. The questioner asks a yes or not question. Then Kaggle responds with yes or no (and Kaggle will not lie). Then your teammate the answerer guesses a possible word. Then Kaggle responds if your are correct or not (and Kaggle will not lie).
> 
> Your team of two bots is competing against another team of two bots to discover the word first.
> 
> UPDATE: Read Nicholas' comment below
> 
> 
> 
> > ## Nicholas Broad
> > 
> > [@cdeotte](https://www.kaggle.com/cdeotte) ,
> > 
> > I believe the questioner also is the guesser. The answerer only responds yes/no.
> > 
> > Here is how I think it goes.
> > 
> > Keyword: France
> > 
> >   Questioner turn 1: Is it a place?
> > 
> >   Answerer turn 1: Yes
> > 
> >   Questioner guess 1: USA
> > 
> >   Kaggle guess checker: Incorrect
> > 
> >   Questioner turn 2: Is it in Europe?
> > 
> >   Answerer turn 2: Yes
> > 
> >   Questioner guess 2: France
> > 
> >   Kaggle guess checker: Correct
> > 
> > 
> > 
> > > ## Chris Deotte
> > > 
> > > Yes, i think you are correct
> > > 
> > > 
> > > 


---

> ## Nicholas Broad
> 
> The answerer wants you to win because they get the same points as the questioner. There is no incentive to produce bad answers
> 
> 
> 
> > ## VolodymyrBilyachatTopic Author
> > 
> > Yes I finally got the idea. Its always 2 teams. If you lie the opponent will get confused and will not get an right answer so you both get lower scores. Thank you
> > 
> > 
> > 
> > ## Kamal Das
> > 
> > what if the reverse, the answerer lies and says OK, right answer to any guess?
> > 
> > that helps the bit pair?
> > 
> > 
> > 
> > > ## Rob Mulla
> > > 
> > > I don't think the agent is responsible for determining if a guess is right, unless I'm missing something, it looks like it's checked using this function from llm_20_questions.py, I'm assuming by the system?
> > > 
> > > ```
> > > def keyword_guessed(guess: str) -> bool:
> > >     def normalize(s: str) -> str:
> > >       t = str.maketrans("", "", string.punctuation)
> > >       return s.lower().replace("the", "").replace(" ", "").translate(t)
> > > 
> > >     if normalize(guess) == normalize(keyword):
> > >       return True
> > >     for s in alts:
> > >       if normalize(s) == normalize(guess):
> > >         return True
> > > 
> > >     return False
> > > 
> > > ```
> > > 
> > > 
> > > 
> > > ## Bovard Doerschuk-Tiberi
> > > 
> > > Yes, the engine code will check the validity of a guesses.
> > > 
> > > 
> > > 


---

