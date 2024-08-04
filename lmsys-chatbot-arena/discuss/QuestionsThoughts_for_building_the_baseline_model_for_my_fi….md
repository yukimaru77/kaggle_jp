# Questions/Thoughts for building the baseline model for my first submission

**Dr. Gopalashivabalasubramanium Chandrashekaran** *Sat Jun 08 2024 10:10:08 GMT+0900 (日本標準時)* (0 votes)

I see that there is no model name in the test data.

I've listed my thoughts below. Would love to hear your input. 

So, basically, we have to analyze the response (a/b) of the unknown model and decide which one wins. 
The user prompt has to be filtered for anything that would cause the model to give a null response or a default reply
The model response, we have to categorize it somehow with the model name. Which means there would be features to look for in a model response to attach it to a named model.
Lastly, once the models are identified, we can refer to some type of weight for each model based on its win percentage versus whatever other model it is facing and decide whether it wins or loses or ties.
Slap all this into a submission file and win.


---

 # Comments from other users

> ## Valentin Werner
> 
> Step 1: Load data
> 
> Step 2: ?
> 
> Step 3: Slap all into a submission file and win 😉
> 
> 
> 


---

