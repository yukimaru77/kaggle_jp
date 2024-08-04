# What is "strategic question answering"?

**marketneutral** *Thu May 16 2024 08:06:58 GMT+0900 (日本標準時)* (5 votes)

From the Overview

```
Each team will consist of one guesser LLM, responsible for asking questions and making guesses, and one answerer LLM, responsible for responding with "yes" or "no" answers. Through strategic questioning and answering, the goal is for the guesser to correctly identify the secret word in as few rounds as possible.

```

The response can only be "yes" or "no", correct? What does it mean to answer strategically in this context?



---

 # Comments from other users

> ## G John Rao
> 
> The phrase is, "Through strategic questioning and answering" - Think of it as a binary search algorithm. 
> 
> 
> 


---

> ## Nicholas Broad
> 
> If your model is bad at answering the questions it will ultimately hurt your own score. Maybe there are different techniques to make sure you answer correctly
> 
> 
> 
> > ## VolodymyrBilyachat
> > 
> > Could be a end game step, where questioner gets all questions and answers and make sure they are right
> > 
> > 
> > 


---

> ## Raki
> 
> I think "correct" is the most obvious and important part for the question answerer and it might help to have a knowledge base here, not just the knowledge embedded in the model weights. 
> 
> The "strategic" can also mean sensible handling of ambiguous cases. 
> 
> EG if the keyword was "Smaug" (dragon from The Hobbit), the "is reptile" property might be ambiguous and it could depend on the situation if you should answer yes/no. 
> 
> 
> 


---

