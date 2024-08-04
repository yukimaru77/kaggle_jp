# Comments 

> ## Ilya Turaev
> 
> Hi [@sercanyesiloz](https://www.kaggle.com/sercanyesiloz) ! Outstanding result with only one XGB. It looks like your cosine similarity function is not working properly because of 
> 
> ```
> vectors = vectorizer.toarray()
> 
> ```
> 
> Do you think modifying it would improve the score? Or these other features are totally enough
> 
> 
> 
> > ## Sercan YeşilözTopic Author
> > 
> > Hey there! In that code, vectorizer is the output of the vectorizer that fitted on train and test sets actually. I don't think there is a mistake.
> > 
> > 
> > 
> > > ## Ilya Turaev
> > > 
> > > It definitely should be, if you overwrite it as:
> > > 
> > > ```
> > > vectorizer = vectorizer.fit_transform([text1, text2])
> > > 
> > > ```
> > > 
> > > Otherwise, vectorizer is still a TfIdf object, and you apply toarray() method to it. Or am I getting it wrong?
> > > 
> > > 
> > > 
> > > ## Sercan YeşilözTopic Author
> > > 
> > > I don't think vectorizer will be a tfidf object after this line of code because when I call the fit_transform function, it returns the transformed values, not tfidf object itself.
> > > 
> > > 
> > > 


---

