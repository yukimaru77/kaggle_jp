# Both the A and B responses are [null]

**Takamichi Toda** *Mon May 13 2024 09:43:54 GMT+0900 (日本標準時)* (22 votes)

During the data analysis, I found samples where the responses for both A and B were [null]. 

Most of these cases arewinner_tie, so it would be best to handle them with rules rather than using ML model.

```
import pandas as pd
train_df = pd.read_csv(f"/kaggle/input/lmsys-chatbot-arena/train.csv")

row = train_df[train_df["id"] == 57180984].iloc[0]
res = row[["response_a", "response_b", "winner_model_a", "winner_model_b", "winner_tie"]].to_dict()
print(res)
# {'response_a': '[null]', 'response_b': '[null]', 'winner_model_a': 0, 'winner_model_b': 0, 'winner_tie': 1}

```

On the other hand, there are some cases where both are [null] yet a winner is determined. 

```
row = train_df[train_df["id"] == 867270727].iloc[0]
res = row[["response_a", "response_b", "winner_model_a", "winner_model_b", "winner_tie"]].to_dict()
print(res)
# {'response_a': '[null]', 'response_b': '[null]', 'winner_model_a': 1, 'winner_model_b': 0, 'winner_tie': 0}

```

How should this be interpreted? 

|  | n_sample | id |
| --- | --- | --- |
| winner_tie | 12 | 57180984, 249576331, 563620901, 939431975, 1224714333, 1433968841, 1833691834, 2624561104, 3013893052, 3697544388, 3731007975, 3870030183 |
| winner_model_b | 4 | 2369712796, 2542474454, 3044249115, 3174500072 |
| winner_model_a | 3 | 867270727, 2941706797, 3235570281 |

For now, it seems better to exclude both [null] data from the training data.



---

 # Comments from other users

> ## Lisa DunlapCompetition Host
> 
> While we removed any single turn conversations with null values with both responses, we chose to not filter these out in multi turn conversations.
> 
> Two things to take into consideration when interpreting the data are: (1) nothing prevents users on Chatbot Arena from voting erratically; and (2) users on Chatbot Arena vote one time per conversation (even for multi-turn conversations).
> 
> For example, if someone submits multiple prompts in rapid back-to-back succession, or if there is some sort of platform error, this can introduce null responses into a conversation that also has valid responses, and then it is up to the individual user how they want to rank the full conversations.
> 
> 
> 
> > ## Lisa DunlapCompetition Host
> > 
> > Correction: it looks like there are a few instances of single turn conversations with "[null]" values in the dataset. Since this appears very rarely, we will not be making any changes to the training dataset
> > 
> > 
> > 
> > > ## Takamichi TodaTopic Author
> > > 
> > > [This thread](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/502449) has also been discussed in this thread, and it seems like it will make for an interesting problem setting as a noisy problem.
> > > 
> > > Thank you for your reply.
> > > 
> > > 
> > > 
> > ## Kaizhao Liang
> > 
> > is it safe to assume this edge case will also be in the test set? mostly coming from how we should parse the inputs.
> > 
> > 
> > 
> > > ## Lisa DunlapCompetition Host
> > > 
> > > yes this could appear as a (very rare) edge case in the test set
> > > 
> > > 
> > > 


---

> ## Valentin Werner
> 
> You either ignore these cases completely and add these rules to your prediction post-processing OR you fix the labels to tie and train on that, hoping that your model learns it. 
> 
> 
> 
> > ## Takamichi TodaTopic Author
> > 
> > Thanks for the reply.
> > 
> > I am going to try to rule it out for now.
> > 
> > 
> > 


---

