# How much data to train Llama 3?

**ano** *Thu Jul 11 2024 08:00:45 GMT+0900 (日本標準時)* (3 votes)

How much data are you using for training Llama 3? I use half of all the given training data for training and the other half as validation data, with cv: 0.968, lb: 0.979.

I want to know about the relationship between the amount of training data and accuracy. I remember reading a discussion somewhere that said using all the data for training does not change the score, but I lost track of that discussion.



---

 # Comments from other users

> ## James Day
> 
> Hesitant to share details about my experiments until the end of the competition, but it is possible to achieve significant accuracy improvements by scaling from tens of thousands of training examples to hundreds of thousands, so I would not expect your models to be saturating at 50% of the data we received from the competition organizers. Using more than 200% is better than 80%. I never scaled down to only training on 50%.
> 
> Broadly speaking, my intuition is that adding more data is almost always beneficial (albeit with diminishing returns) so long as that data is sufficiently high quality (not too repetitive, mislabeled, or different from the test data) and your model has sufficiently high capacity to learn from that data (which shouldn't be a problem for Llama 3 8B with a decent LoRA config).
> 
> 
> 
> > ## anoTopic Author
> > 
> > Thank you for the valuable information! It seems I was mistaken in thinking that a small amount of training data would be sufficient. I'll try optimizing by adding training data (including external data) and changing the parameters.
> > 
> > 
> > 
> > ## Cody_Null
> > 
> > You have already shared a friendly amount of information so feel free to hold back, are you generating new data from the training data?
> > 
> > 
> > 
> > > ## James Day
> > > 
> > > I don't want to elaborate on where my extra data came from until the end of the competition. 🤐
> > > 
> > > 
> > > 
> > > ## Sparsh Tewatia
> > > 
> > > Thats enough for the smart one to know. 😀
> > > 
> > > 
> > > 


---

