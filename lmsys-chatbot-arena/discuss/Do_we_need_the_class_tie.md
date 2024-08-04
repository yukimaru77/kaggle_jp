# Do we need the class "tie"?

**Anh Bui** *Fri May 03 2024 15:50:05 GMT+0900 (日本標準時)* (4 votes)

I have a question about why there is a class 'tie', when based on the probabilities (winner_model_a/winner_model_b) = (0.5, 0.5), it can be determined whether the two models have a 'tie'.



---

 # Comments from other users

> ## Marília Prata
> 
> Hi Anh Bui (bibanh),
> 
> On the original dataset instead of "winner_tie"  they have "winner" column (where the Rows are: model_a, model_b, tie AND tie (bothbad)
> 
> Battles No ties
> 
> battles_no_ties = battles[~battles["winner"].str.contains("tie")]
> 
> Battles without ties
> 
> visualize_battle_count(battles_no_ties, "Battle Count for Each Combination of Models (without Ties)")
> 
> Counting ties
> 
> visualize_battle_count(battles[battles['winner'].str.contains("tie")], "Tie Count for Each Combination of Models")
> 
> [https://colab.research.google.com/drive/1KdwokPjirkTmpO_P1WByFNFiqxWQquwH#scrollTo=PbTdhkLQp113](https://colab.research.google.com/drive/1KdwokPjirkTmpO_P1WByFNFiqxWQquwH#scrollTo=PbTdhkLQp113)
> 
> That's what the authors wrote:
> 
> "Statistics
> 
> "The authors allowed the user to declare a tie between the pairs of models. To collect additional data, later in the tournament they also allowed the user to declare a tie in which both models were bad. There were a significant portion of tied outcomes."
> 
> I hope it could help to clarify. I didn't read anything else about the ties on that Notebook or in their paper too.
> 
> 
> 


---

> ## bogoconic1
> 
> I would think it is necessary for reason (B)
> 
> A tie could mean
> 
> (A) The user rates both responses as equally good
> 
> (B) The user rates both responses as equally bad. The 2 models can answer in different ways, of which both responses are hallucinated (by making up completely different facts etc) or not answering the question
> 
> For (B) I’m pretty sure the 2 classes will not be predicted as (0.5, 0.5) 🧐
> 
> 
> 


---

> ## Rich Olson
> 
> For my first submission - I tried filling in "winner_tie" with all 0's.
> 
> That got me a score of 11.73 (almost last-place).  At least - I'm assuming "winner_tie" being 0's was a factor.
> 
> For my next entry - I'm going to try to fill in winner_tie based on the confidence of A or B winning.  Hopefully this improves things…
> 
> In the train data - it seems ties are very common (about 1 out of 3).
> 
> 
> 


---

