# Interpreting the metric & why current baselines are basically guessing

**Valentin Werner** *Tue May 07 2024 23:54:57 GMT+0900 (日本標準時)* (16 votes)

As all currently available baselines have a score > 1.0, I wanted to explore how to interprete this.

You can find my exploration in this notebook: [https://www.kaggle.com/code/valentinwerner/log-loss-what-are-good-scores/notebook](https://www.kaggle.com/code/valentinwerner/log-loss-what-are-good-scores/notebook)

Note that I am making some assumptions for simplicity, such as assuming that bad predictions are evenly distributed (e.g., instead of prediction [1,0,0] you are prediting [0.3, 0.35, 0.35] or [0.2, 0.4, 0.4]).

What I noticed it that:

- accuracy and loss are strongly misaligned and I am making the assumption that well calibrated models will get us a long way until we are able to achieve very good accuracy (which I assume is hard to do for this problem).

- current solutions are all basically guessing, as you can see in the graph below



---

 # Comments from other users

> ## bogoconic1
> 
> I feel that one contributing factor is
> 
> - The user doesn’t understand the responses from the LLM. It can arise from lack of domain knowledge of the topic he/she is trying to ask.
> 
> How does the user know if the answer is good in this case, or which one is better ? From personal experience, I have asked and seen LLM responses like this and I don’t know how to rate them
> 
> 
> 
> > ## Valentin WernerTopic Author
> > 
> > Agreed, I showed the tool many of my colleagues and there is a 50/50 chance that we disagree on what the better answer is. This makes it quite interesting. However, if you look at it in terms of individual model winrates, it must be possible to get scores well above the current levels
> > 
> > 
> > 
> > ## Dr. Gopalashivabalasubramanium Chandrashekaran
> > 
> > Similar to what Valentin said. The win rate will speak for itself for some models. Your thought on the subjective understanding of the user prompting is completely valid. It is an unknown. But maybe a weight can be applied to user prompt data based on grammar/length.
> > 
> > 
> > 


---

