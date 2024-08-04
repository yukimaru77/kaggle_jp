# predict the model of the response to to a classification?

**Lee** *Sun May 26 2024 18:24:03 GMT+0900 (日本標準時)* (2 votes)

Hello, I'm new to Kaggle and I've got an idea: What if we shift from simply evaluating responses to a 3-class classification, to a  64-class classification? Here's the plan:

First, use our training data to train a classification model. This model will help us predict which among the 64 models a given response belongs to.

Then, during the inference phase, armed with our trained classifier, we'll categorize each response into one of the 64 model types.

With this information in hand, we can ascertain which two models are in competition. Leveraging the training dataset as our prior knowledge, we'll then proceed to predict the likely winner between these two models.

[Translated from chatGPT] Sorry for your uncomfortable reading, I am not a naive English speaker🙏



---

 # Comments from other users

> ## Valentin Werner
> 
> I think this can be a valuable proxy or feature for prediction. But you should keep in mind that the best model had ~65% winrate, so even if you know the model, it is difficult to predict whether it will win.
> 
> As such, I can imagine that this is one feature among text embeddings or the length feture. But predicting the model that wrote a response is similar difficult to predicting the win directly. You will have less training data per class etc.
> 
> I think a similar strategy was also proposed in the Detect AI Generated Text Competion.
> 
> 
> 
> > ## Ivan Vybornov
> > 
> > Model of a response is an immensely valueable feature. Tried adding it to the lgbm locally: a few features like length of prompt and responses alongside with model name gives a score of around 0.99 with CV. 
> > 
> > Though I am concerned that new models might appear in the private set (not sure if it is a reasonable concern).
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > I dont think it is a reasonable concern. If you are able to reliably predict the model, than a new model will likely fall into the "next best" category. It would probably reduce score compared to if you know all models but you would likely still gain. 
> > > 
> > > also from my knowledge the model distribution seems not immensely imbalanced to the point where only a few responses exist for a model. Therefore, I imagine this would not be the case
> > > 
> > > 
> > > 


---

