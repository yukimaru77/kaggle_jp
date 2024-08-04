# Using XGBoost and Graident Boosting Techniques

**Royy** *Mon Jul 08 2024 17:59:56 GMT+0900 (日本標準時)* (0 votes)

Here, the provided code defines several functions to compute various text analysis metrics to understand the quality of the prompt and responses. The functions are defined to calculate word count, character count, sentence count, average word length, average sentence length, type-token ratio, word frequency, bigram frequency, and readability scores using the nltk and textstat libraries. 

The readability scores function calculates several readability indices, including the Flesch-Kincaid score, Gunning Fog index, SMOG index, and Automated Readability Index (ARI).

After defining these functions, the code applies them to the "prompt", "response_a", and "response_b" columns of the DataFrame. For each of these columns, it calculates the word count, character count, sentence count, average word length, and average sentence length by applying the respective functions and creates new columns in the DataFrame to store these metrics. 

Here, in the notebook  I have just tried a few of these metrics to achieve a log loss of 1.05.

Ways you can enhance this code to decrease it's log loss:

Add more hyperparameters.
Try out the other metrics (which are commented on in the code).
Also, add more variables like the Jaccard index and cosine similarity between response a, b, and prompt.
Increase the number of iterations for each model per fold.

These can easily improve the model output and decrease the log loss on the test dataset.

Also, upload the textstat library as the internet is turned off for this competition.

Notebook URL: [https://www.kaggle.com/code/nehalroy/using-xgboost-and-gb-using-nltk](https://www.kaggle.com/code/nehalroy/using-xgboost-and-gb-using-nltk)



---

 # Comments from other users

> ## Valentin Werner
> 
> Hey [@nehalroy](https://www.kaggle.com/nehalroy) - please beware that Pyphen is not released as open source / commercially available package and is therefore one of the few packages that is not allowed in this competition. 
> 
> 
> 
> > ## RoyyTopic Author
> > 
> > Thank you [@valentinwerner](https://www.kaggle.com/valentinwerner) for the heads up. Highly appreciated.
> > 
> > Although, I just shared this as a technique that can be used to design a Gradient Boosting model for this certain problem.
> > 
> > 
> > 


---

