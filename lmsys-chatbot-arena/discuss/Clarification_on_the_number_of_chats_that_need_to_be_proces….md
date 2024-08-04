# Clarification on the number of chats that need to be processed

**Gabriel Mirea** *Thu Jul 04 2024 21:04:10 GMT+0900 (日本標準時)* (0 votes)

Hi,

The dataset description says 

When your submission is scored, this example test data will be replaced with the full test set. There are 55K rows in the training data, and you can expect roughly 25,000 rows in the test set.

and the leaderboard says

This leaderboard is calculated with approximately 26% of the test data. The final results will be based on the other 74%,

So should we expect that the final submission on the private leaderboard will need to process ~75.000 rows?



---

 # Comments from other users

> ## RB
> 
> 
> So should we expect that the final submission on the private leaderboard will need to process ~75.000 rows?
> 
> No, total 25000 samples 
> 
> Public LB - 26% => 6500 Samples
> 
> Private LB - 74% => 18500 Samples
> 
> Total Test Set = 25000
> 
> When you make a submission, your code is doing inference for all 25000 samples, we only see public LB with 6500 samples, remaining after competition ends
> 
> 
> 
> > ## Gabriel MireaTopic Author
> > 
> > Thanks! That makes sense, so if the submission scores on the LB it got through all the samples. And the final score is hidden so that people don't probe, I guess?
> > 
> > My main concern was if the notebook will have to deal with more samples later. That's clear now, thank you again.
> > 
> > 
> > 


---

