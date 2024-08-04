# Submission Scoring Error

**RomanZubarev** *Wed Jun 12 2024 20:49:41 GMT+0900 (日本標準時)* (2 votes)

Hi! I'm a newbie and it's my first time participating in a competition here. Can anyone tell me why I get "Submission Scoring Error"? Everything seems to be under the rules and expectations of the result.

[2024-06-12 14-44-23.png](https://storage.googleapis.com/kaggle-forum-message-attachments/2868474/20808/2024-06-12 14-44-23.png)

---

 # Comments from other users

> ## Ahmad Al-Husainy
> 
> Was the notebook execution successful, or did it fail? If it succeeded, the only other possible reason I can think of, aside from what other Kagglers mentioned about probabilities summing up to more than one, could be the data format in the columns . If the notebook failed, you should check the execution logs, which will show you where it failed. 
> 
> 
> 


---

> ## Valentin Werner
> 
> You can try setting index=False during saving the csv, that caused problems for me before I think.
> 
> Is it because (winner_model_a + winner_model_b + winner_tie) > 1?
> 
> I don't think this should matter, as the log loss implementation is a wrapper for sklearn, where this is not an issue from my experiments
> 
> 
> 


---

> ## Masayuki Takahashi
> 
> Is it because (winner_model_a + winner_model_b + winner_tie) > 1?
> 
> 
> 
> > ## Anya
> > 
> > Good remind! I found my submission data has this problem.
> > 
> > 
> > 


---

