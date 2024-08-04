# What is the calculation of the loss & log_loss?

**Anya** *Sun Jun 30 2024 16:14:27 GMT+0900 (日本標準時)* (0 votes)

I happened to meet a situation that loss & log_loss was NaN. 

I know in programming it would happen when 0 is taken as the dividend or something like that. 

Now I need to know the calculation of the loss & log_loss so I could find out the cause.

I appreciate every answer.🙏



---

 # Comments from other users

> ## Valentin Werner
> 
> Kaggle uses the sklearn implementation, which is quite well documented: [https://scikit-learn.org/stable/modules/generated/sklearn.metrics.log_loss.html](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.log_loss.html)
> 
> The log loss does not use any division, but it uses the logarithm. This technically could produce nan values if your predictions are < 0, but this is not happening in the sklearn logloss.
> 
> Anyways, I think you should always softmax your predictions before calculating the log loss.
> 
> Hope this helps!
> 
> 
> 
> > ## AnyaTopic Author
> > 
> > Thanks a lot. I switched to another GPU with larger memory, and the error got solved.
> > 
> > Maybe the data overflow cause a value out of logarithm's definition domain.
> > 
> > 
> > 


---

