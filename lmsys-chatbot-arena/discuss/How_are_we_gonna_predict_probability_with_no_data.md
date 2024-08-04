# How are we gonna predict probability with no data?

**alekh** *Sun May 12 2024 14:13:23 GMT+0900 (日本標準時)* (0 votes)

How are we gonna predict the probability when we have no training data with probabilities that makes sense. The training data is comprised of 1-hot vectors assigning 100% probability to one of the outcomes. That must clearly be wrong. I don't understand what the training set represents. Does it represent the preference of one particular human? Of a random human? If so, are there multiple rows with the same prompt and responses for different people?



---

 # Comments from other users

> ## alekhTopic Author
> 
> Guess I found the answer:
> 
> "The competition dataset consists of user interactions from the ChatBot Arena. In each user interaction a judge provides one or more prompts to two different large language models, and then indicates which of the models gave the more satisfactory response."
> 
> So i guess we have to like do a softmax on the logits to get probabilities.
> 
> 
> 


---

