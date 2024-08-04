# [FIXED] - The Top 9 LB is the result Errors

**Chris Deotte** *Wed May 29 2024 23:00:06 GMT+0900 (日本標準時)* (19 votes)

On May 29 at 14:00 UTC, I noticed the top 9 agents on the LB were all the result of gaining points from their teammate throwing an error. (The top 9 teams at 14:00 UTC were: Dapeng, Agney, Neel, Mitul, Neige, Agney, Gol-eel, tr, Mesmerized).

For each of the top 9 agents on LB, I reviewed their most recent game where they achieved positive points. I display these below. In each case, they received points because their teammate errored.

Is this the intended scoring mechanism? [@develra](https://www.kaggle.com/develra) [@addisonhoward](https://www.kaggle.com/addisonhoward) Should luck be the reason teams climb the LB?

IMO, when an agent throws an error, I suggest that the defective bot loses points and all 3 other bots ignore the game. (i.e. the other 3 bots get zero points and they immediately get a new game to replace the erroneous game). 

Guessing the keyword is difficult and there shouldn't be an easy way to gain lots of free points. (And on private LB, guessing will be even more difficult without a list of keywords).

## 1st Place

## 2nd Place

## 3rd Place

## 4th Place

## 5th Place

## 6th Place

## 7th Place

## 8th Place

## 9th Place



---

 # Comments from other users

> ## Chris DeotteTopic Author
> 
> UPDATE. I notice the same thing happening on May 30th at 14:00 UTC. The new first place jumped up to LB 660 because their teammate had an error. This destabilizes the leaderboard because now the original top LB bots will play with and against these bots whose true score is under 600. 
> 
> ## New 1st Place
> 
> ## New 5th Place
> 
> and the new 5th jumped there because their teammate had an error:
> 
> 
> 
> > ## OminousDude
> > 
> > The creators of this competition really need to fix this quickly.😑
> > 
> > 
> > 
> > > ## OminousDude
> > > 
> > > I am looking through the top 25 LB and out of the top 25 11 of them are boosted by errors.
> > > 
> > > 
> > > 


---

> ## OminousDude
> 
> Hi, the first place error bot is mine I have no idea why it is erroring I am fi I am finding out now thank you for alerting me to this. I had no intention of "illegally" giving top places points.
> 
> 
> 
> > ## OminousDude
> > 
> > My bot is also 3rd 😭. I have decided to submit three of my older bots to overwrite the offending error bots. This is my temporary solution since I do not want to be contributing to an unfair leaderboard.
> > 
> > 
> > 
> > ## Chris DeotteTopic Author
> > 
> > Hi OminousDude. There is no need to apoligize. Everybody's bots will make errors from time to time as we develop solutions. Earlier versions of my bots had errors and each day I remove errors and improve my bots. So don't worry about submitting bots with errors. Continue to try new things and submit whatever you want.
> > 
> > I think the competition metric should be updated so that bot errors do not help other bots.
> > 
> > 
> > 
> > > ## OminousDude
> > > 
> > > Yes, that would be the optimal solution but again the temporary solution is for me to remove the bots until their errors are fixed. Thank you for informing me on the issues of my bots. Because it was very weird that my agent improves almost all the time more or less +10 each time it goes up against another bot; however, its score is still always low.
> > > 
> > > 
> > > 


---

> ## Bovard Doerschuk-Tiberi
> 
> Taking a look at this now, thanks for reporting.
> 
> 
> 
> > ## Bovard Doerschuk-Tiberi
> > 
> > A fix for this should be rolling out tomorrow. The reward when an agent fails after this should be net zero. For example the failing agent might get -21 and the other three get an average of +7 each.
> > 
> > Penalizing the failing agent is important to keep the leaderboards clear and not allow a "error on purpose" strategy to exist. (eg if an agent hasn't guessed after X rounds and knows the average game at their level is X + 1, they could error on purpose if there was no penalty for doing so). 
> > 
> > 
> > 
> > > ## Bovard Doerschuk-Tiberi
> > > 
> > > This is rolled out now
> > > 
> > > 
> > > 


---

> ## Giba
> 
> I support what Chris says. I observed the same behaviour in LB, agent errors distribute free points to other agents.
> 
> 
> 


---

> ## Chris DeotteTopic Author
> 
> [@bovard](https://www.kaggle.com/bovard) I noticed that Mohammad just received 130 points (on June 4th) when his teammate (me Chris) errored. Other teams on the LB need to successfully win 5+ games to get 130 points (which requires the difficult accomplishment of guessing 5+ words correctly versus the lucky result of teammate error). 
> 
> FYI, Kaggle said they fixed awarding points for teammates of error teams but this doesn't look fixed:
> 
> 
> 
> > ## Bovard Doerschuk-Tiberi
> > 
> > Yeah I saw that as well. Looks like there was a bug if the agent errors on the last round of the competition. This has been fixed in [https://github.com/Kaggle/kaggle-environments/pull/275](https://github.com/Kaggle/kaggle-environments/pull/275)
> > 
> > 
> > 


---

> ## Andres H. Zapke
> 
> Hello!
> 
> One question, where does the answerer even come from? Is this supposed to be a separate LLM that has to be trained independently? 
> 
> And did I get it right, that because the answerer is not answering correctly, the "correct" guesses aren't being graded accordingly?
> 
> 
> 
> > ## Chris DeotteTopic Author
> > 
> > Each match has 4 Kaggle teams which are Questioner + Answerer versus Questioner + Answerer. So it is 2 vs. 2.
> > 
> > Each Answerer knows the correct answer and responds to their teammate the Questioner.
> > 
> > 
> > 
> > > ## Andres H. Zapke
> > > 
> > > Yes, but the Answerer cannot be a hard-coded bot, since it has to interpret the question correctly. I thought he is responsible for grading our "Questioner LLMs", so I think it should be universal to all games. 
> > > 
> > > Question: How and why does the Answerer respond to its teammate and not to the enemy Questioner?
> > > 
> > > 
> > > 


---

