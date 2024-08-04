# How to choose a suitable model

**KeShuang Liu** *Wed Jul 24 2024 13:48:06 GMT+0900 (日本標準時)* (0 votes)

When I was fine-tuning, log_dass started oscillating around 1. Do I need to choose a point with the lowest loss to submit, or do I submit the final result



---

 # Comments from other users

> ## Valentin Werner
> 
> This looks like a training loss, right? Your validation loss should be more stable. 
> 
> Selecting a model should never be done based on training loss, as training loss does not represent the way the model can predict on unseen data. From my experience, it is either best to train with CV to find best parameters and then do a full train for a fixed length, that worked best for all the CV models OR you train a single model, use a validation set and submit that single model.
> 
> You would then select the model / parameter which minimizes the validation loss. Note, that you can still overfit on validation loss, as you might take a specific point of the epoch which has the lowest validation loss. Small differences in validation loss do not necessarily reflect capability of the model on new data. So, it is fine to you the leaderboard submissions as "test set", which basically validates your validation loss. If your model has a lower validation loss and leaderboard score (which is loss in this case), this is a promising model.
> 
> Hope this helps you out!
> 
> 
> 
> > ## KeShuang LiuTopic Author
> > 
> > Thank you very much. I just checked and confirmed that this is indeed a training loss rather than a validation set loss. I will use the validation set loss to select the model and also try to use the training method you mentioned. Thank you for your reply
> > 
> > 
> > 


---

> ## Casmir Sunny
> 
> I will suggest that you submit the model corresponding to the checkpoint with the lowest validation loss rather than the final model. This approach ensures you are submitting the most generalizable and best-performing version of your model.
> 
> 
> 
> > ## Valentin Werner
> > 
> > This does not have to be the case. You can definetly overfit on validation data by blindly following this approach, particularly when only using a smaller subset of data as validation data. It also makes sense to compare validation loss with training loss, and decide from there. 
> > 
> > 
> > 


---

> ## Yi-Fu Chen
> 
> About Trainer
> 
> My understanding is that "Training Loss" is the last loss calculated during training, and there is no average, while "Validation Loss" is the average loss of the entire Validation dataset.
> 
> So "Validation Loss" may be smoother and "Training Loss" may be jumpier.
> 
> 
> 


---

