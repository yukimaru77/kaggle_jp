# Did you try to explode the conversation responses?

**Mattia Vanzetto** *Thu Aug 01 2024 04:42:15 GMT+0900 (日本標準時)* (0 votes)

Hello guys,

I saw that the ~86% of the training conversations is composed by just a single prompt + response, but 14% is not. I saw also that, at least in the public notebooks, the fine-tuned models usually have a maximum sequence lenght of 2000/2400 characters, and often the prompt assembled for the models are just prompt_list + response_a_list + response_b_list, which surely lead to cases where the response_b is completely truncated, or anyway to a loss of information.

Did you try to explode the responses, fine-tune a model and then aggregate the predictions on the single piece of the conversation?

The mean/median length of the single piece of conversation "prompt_i + response_a_i + response_b_i" is between 2000 and 2400 characters, which seems perfect for this expirement.

I would like to try myself, but I have no fine-tuning experience, no computing power, and no time 😂

For what it's worth, I tried with a simple xgboost, same features preparation, same optimization procedure, the exploding+aggregating approach got 1.03 on the leaderboard vs 1.04 of the standard approach.

Another expirement I would have liked to do is to build a binary classifier considering just prompt + response_X, with target the relative winner_model_X, basically duplicating the number of rows, without considering the "opponent's response", and then aggregate all back.

I am really looking forward to see the solutions after the competitions ends. 

Good luck for the last days of the competition 🍀



---

 # Comments from other users

> ## JM
> 
> I tried, it increase the inference time and did not see any improvement to public LB myself
> 
> 
> 


---

> ## Yi-Fu Chen
> 
> 
> Another expirement I would have liked to do is to build a binary classifier considering just prompt + response_X, with target the relative winner_model_X, basically duplicating the number of rows, without considering the "opponent's response", and then aggregate all back.
> 
> I have thought about a similar concept, but the intuition seems unreasonable because winning and losing are compared.
> 
> 
> 
> > ## Mattia VanzettoTopic Author
> > 
> > Do you mean loosing and tie? These two would be "compared" doing so.
> > 
> > 
> > 


---

