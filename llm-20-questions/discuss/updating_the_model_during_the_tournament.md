# updating the model during the tournament

**Afordancja** *Thu May 30 2024 22:11:48 GMT+0900 (日本標準時)* (0 votes)

Can the model save data/update the mode during the tournament and will this data be available during subsequent fights?

whether the model must be completely trained locally and after uploading each new fight starts in the same zero state



---

 # Comments from other users

> ## Chris Deotte
> 
> My understanding is that we cannot change a submitted model. Once it is submitted, the weights are fixed.
> 
> We can however, download all the game history, train a new model locally to use past games, and then submit a new version of our model.
> 
> 
> 
> > ## AfordancjaTopic Author
> > 
> > 
> > My understanding is that we cannot change a submitted model. Once it is submitted, the weights are fixed.
> > 
> > yes, we cant, but questions is that the model can do it byself.
> > 
> > 
> > 
> > > ## Bovard Doerschuk-Tiberi
> > > 
> > > Any local files or changes made during a match will be discarded at the end of a match. The only thing that is loaded into a match is your submission bundle. So no, your model can't update itself across matches.
> > > 
> > > 
> > > 


---

> ## loh-maa
> 
> I think agents are called by the environment only to get responses, so any online training would have to take place during their turns/moves… on top of that, I don't think agents can have access to anything but their pre-loaded data, and their online experience, which probably would be too short to be useful..
> 
> 
> 


---

