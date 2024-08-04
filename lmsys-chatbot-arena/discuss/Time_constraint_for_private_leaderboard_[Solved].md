# Time constraint for private leaderboard [Solved]

**raconion** *Fri Jul 05 2024 11:15:47 GMT+0900 (日本標準時)* (2 votes)

There are roughly 25,000 rows in the test set. Among them, 26% are used for public lb while the rest 74% are used for private lb. 

Since in Overview section, the time constraint is 9 hrs, does this mean that our notebook has to finish the inference for 74%*25,000 =18,500 rows in the test set? Or this time constraint is for public lb and will be scaled according to the number of rows when it comes to private lb?

[@addisonhoward](https://www.kaggle.com/addisonhoward) [@mylesoneill](https://www.kaggle.com/mylesoneill) Would really appreciate if you can clarify this!

Update:

Our notebook will be run for all 25k rows but only 26% shown on public lb. Thanks for the comment [@lizhecheng](https://www.kaggle.com/lizhecheng) 

This comment also clarify this issue: [link](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/516995#2904512)



---

 # Comments from other users

> ## Enter your display name
> 
> As long as you can see your public score, your private score has also been calculated, but you just can't see it for now. Thus you don't need to worry about that.
> 
> 
> 
> > ## jiangli59
> > 
> > I vote for that. Is it possible to extend the time budget over 9 hrs? Or, Do we have other opinions to solve that? My code is extremely overwhelmed for the inference budget.  
> > 
> > 
> > 
> > > ## raconionTopic Author
> > > 
> > > I don't think the time constraint can be extended unless the competition host decides so. There are way arounds though such as all kinds of efficient inference techniques.
> > > 
> > > 
> > > 


---

