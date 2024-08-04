# I am still confused about scorring

**VolodymyrBilyachat** *Thu May 30 2024 08:00:42 GMT+0900 (日本標準時)* (0 votes)

My understanding that questioner and answerer works together. If they guess the word they will get points so i would assume if they dont work nicely both gets negative reward.



---

 # Comments from other users

> ## Chris Deotte
> 
> Your change in points depends on the scores of your teammate and opponents.
> 
> Before game started, you had 659, Learning Curve had 599, Raki had 603, and Lathashree had 594. Afterward you all tied. So all scores move toward the average of the 4 teams. This means your score decreases while the other 3 increase.
> 
> Here is a approximate summary:
> 
> - If you tie with teams scored lower than yourself, your score decrease
> 
> - If you tie with teams scored higher than yourself, your score increase
> 
> - If you win, your score increase
> 
> - If you lose, your score decrease.
> 
> 
> 
> > ## Chris Deotte
> > 
> > Here is quote from evaluation page [here](https://www.kaggle.com/competitions/llm-20-questions/overview/evaluation)
> > 
> > Ranking System
> > 
> >   After an episode finishes, we'll update the rating estimate for all bots in the episode. If one bot pair won, we'll increase their μ and decrease the opponent's μ -- if the result was a tie, then we'll move the μ values closer towards their mean. The updates will have magnitude relative to the deviation from the expected result based on the previous μ values, and also relative to each bot’s uncertainty σ. We also reduce the σ terms relative to the amount of information gained by the result. The score by which your bot wins or loses an episode does not affect the skill rating updates.
> > 
> > 
> > 
> > ## VolodymyrBilyachatTopic Author
> > 
> > Okay now it make sense. Thanks for explanation
> > 
> > 
> > 


---

