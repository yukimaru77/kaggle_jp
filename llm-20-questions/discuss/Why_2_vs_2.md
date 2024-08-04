# Why 2 vs 2

**kosirowada** *Wed Jul 10 2024 00:29:36 GMT+0900 (日本標準時)* (0 votes)

I don't understand why the bot is 2vs2. Is this for reducing computation costs?



---

 # Comments from other users

> ## Chris Deotte
> 
> It requires a more generalized and meaningful solution. If one Kaggler made both the Questioner and Answerer, then they don't need to use LLM but could rather ask specific questions about word spelling (knowing that the answerer will always answer correctly) and binary search one million words alphabetically in 20 guesses.
> 
> 
> 
> > ## mhericks
> > 
> > This is not solved by the 2 vs 2, but by the fact that an agent is paired with another agent, no? One could also pair random agents, evaluate them (see if / in how many steps they can find the keyword). This establishes for each agent, how well he cooperates with another agent. Especially, a 2 vs 2 is not necessarily required. 
> > 
> > 
> > 
> > > ## CchristoC
> > > 
> > > But then it will turn into account luckiness as an important factor (luckiness of getting an easy or hard to guess keyword. By having 2 pairs, it removes this luckiness factor. (If one of the pair can do it, then it's proven to be not that hard. Except if both can't do it, then points reduced on all players aren't much.)
> > > 
> > > 
> > > 
> > > ## mhericks
> > > 
> > > Again, no 2 vs 2 is needed. The evaluation just needs to ensure that each keyword is evaluated by multiple pairs. Then, the performance of a team can easily be compared relative to all other teams having played that keyword. In a 2 vs 2 setting, you get signal from 2 other team playing the keyword (which is high variance). In the more general setting, you have a much richer signal as you can compare against all pairs that ever played that keyword. 
> > > 
> > > 
> > > 


---

> ## Bhanu Prakash M
> 
> Also its pretty easy to "leak" the keyword to the questioner/guesser by the 5th step if you are the answerer. So I assume that is why we are playing a 2v2.
> 
> 
> 
> > ## mhericks
> > 
> > Can you elaborate?
> > 
> > 
> > 
> > > ## Bhanu Prakash M
> > > 
> > > It would be possible to store the keyword using a global variable and cheat very easily if the same person were assigned as both 'ans' and 'question/guesser'.
> > > 
> > > But since we are having a 2v2 that would render this piece of information useless.
> > > 
> > > 
> > > 
> > > ## mhericks
> > > 
> > > That is not really fixed by 2v2 format, but by the fact that an agent is not paired with itself. Especially, this is also not a problem in the separate evaluation described below. Moreover, the kaggle environment ensures that each agent run in separate containers and can interact exclusively through the environment. 
> > > 
> > > 
> > > 


---

> ## CchristoC
> 
> It's a race of who correctly guesses the keyword first. So since 1 game needs a questioner and answerer, there will be 2 teams hence 4 people.
> 
> 
> 


---

