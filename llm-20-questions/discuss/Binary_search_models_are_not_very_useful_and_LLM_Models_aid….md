# Binary search models are not very useful and LLM Models aiding binary search models is not beneficial

**OminousDude** *Fri May 31 2024 03:16:05 GMT+0900 (日本標準時)* (1 votes)

First of all, I will advise against binary models because as one of the competition creators says

"We will be changing out the list of words after the submission deadline and then we'll wait for the scores to stabilize. Any agent assuming a fixed word list will perform quite poorly."

Secondly, I recently saw in my logs that I (and many other people) were going against binary search strategies. The main type of which is letter guessing strategies in which the guesser will ask if the keywords' first letter is between a-g then g-m and so on. To help my model I decided to implicitly tell it the first letter of the keyword. So inside my prompt-engineering/context, I told my model

The keyword is "{keyword}" and the first letter of the keyword is "{keyword[0]}"

This however does not help the model and instead hinders its performance and score by quite a bit. I could not imagine why this would happen and if someone had any ideas I would love to see them in the comment section.

I made this discussion to advise against helping (and using) binary search models as they will also eventually be almost completely useless in the private leaderboard at the end since practically all the keywords will change.

If you find this discussion helpful please upvote. Thank you for reading and I hope this helps you!



---

 # Comments from other users

> ## waechter
> 
> Thanks for sharing your thoughts !
> 
> This however does not help the model and instead hinders its performance and score by quite a bit
> 
> How did you mesure the performance ? I think the leaderboard score is too random to consider right now, and it's better to check if the question are answered correctly.
> 
> From what i saw in [my notebook](https://www.kaggle.com/code/waechter/llm-20-questions-leaderbord-analyze-best-agents?scriptVersionId=180667811&cellId=30) your agent answer questions like is the last letter of the keyword in this list correctly. So maybe your model don't need that extra help ? 
> 
> 
> 
> > ## OminousDudeTopic Author
> > 
> > I decided to subimt my models at the same time and take the average of all the movements from all games. And this
> > 
> > From what i saw in my notebook your agent answer questions like is the last letter of the keyword in this list correctly. So maybe your model don't need that extra help ?
> > 
> > is weird because I saw my model fail on these cases but it might have bean an older version.
> > 
> > 
> > 
> > > ## OminousDudeTopic Author
> > > 
> > > This might be useful for your model but for my model it did not improve.
> > > 
> > > 
> > > 


---

> ## Lucas Fernandes
> 
> why do you assume the binary search model wouldn't have access to all words? and LLM will also need to use datasets to find an answer the same way the binary search model would
> 
> 
> 
> > ## Marek Przybyłowicz
> > 
> > Exactly my thoughts. A dictionary of all english words (around 0.5m) is barely 5MB. Why not load them all?
> > 
> > Where I would see a problem is the speed of finding the answer. 
> > 
> > 
> > 
> > > ## Lucas Fernandes
> > > 
> > > the way I’m working on it is the search corresponds to the questions asked so it’s actually fast enough the challenge is making the tree in a way that every word has a unique path that can be found in under 20 questions 
> > > 
> > > 
> > > 


---

