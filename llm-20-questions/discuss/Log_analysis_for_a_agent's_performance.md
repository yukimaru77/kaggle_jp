# Log analysis for a agent's performance 

**VijayaragavanRamasamy** *Mon Jun 03 2024 00:33:46 GMT+0900 (日本標準時)* (1 votes)

How to decipher logs? There are 4 players and multiple guesses as well as answers in json. How do I find the guesses or questions asked by my agent?



---

 # Comments from other users

> ## waechter
> 
> I made [https://www.kaggle.com/code/waechter/llm-20-questions-games-dataset](https://www.kaggle.com/code/waechter/llm-20-questions-games-dataset) to download json logs, and format them into an easy to use dataset
> 
> In [https://www.kaggle.com/code/waechter/llm-20-questions-leaderbord-analyze-best-agents](https://www.kaggle.com/code/waechter/llm-20-questions-leaderbord-analyze-best-agents) i use the dataset to analyse games from the current best agents. You can use it to analyze your own games 
> 
> Example:
> 
> df.loc[df.guesser='your_team_name']
> 
> Hope this help!
> 
> 
> 
> > ## VijayaragavanRamasamyTopic Author
> > 
> > Thanks. I will try analysing json logs using this approach 
> > 
> > 
> > 


---

