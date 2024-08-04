# Unspecified exception, only when submitted (later = Submission Scoring error)

**RickPack** *Tue May 21 2024 01:00:22 GMT+0900 (日本標準時)* (5 votes)

My [Python notebook](https://www.kaggle.com/code/rickpack/python-average-prob-per-word-no-gpu) and [R notebook](https://www.kaggle.com/code/rickpack/r-average-prob-per-word-no-gpu/) run without issue but when I submit them, I get a "Notebook Threw Exception" error that is only visible on the Submissions screen. The log shows no errors.

Does anyone have a potential solution?

R:             [https://www.kaggle.com/code/rickpack/r-average-prob-per-word-no-gpu/](https://www.kaggle.com/code/rickpack/r-average-prob-per-word-no-gpu/)

Python:   [https://www.kaggle.com/code/rickpack/python-average-prob-per-word-no-gpu](https://www.kaggle.com/code/rickpack/python-average-prob-per-word-no-gpu)

[@sohier](https://www.kaggle.com/sohier), [@addisonhoward](https://www.kaggle.com/addisonhoward) 



---

 # Comments from other users

> ## David.Ricardo.H.X
> 
> i got the same problem
> 
> 
> 


---

> ## RickPackTopic Author
> 
> Reopening this [@sohier](https://www.kaggle.com/sohier), [@addisonhoward](https://www.kaggle.com/addisonhoward) in hopes of getting thoughts, please? Both the R and Python notebooks are failing with a Submission Scoring Error after minor modifications. I see that the row sums of the probabilities are not always exactly 1 (e.g., 1.002, 0.999, 1.000). If that could be the problem, could you please see if you can comment on what might repair that problem? I have tried various kinds of rounding and standardizing as you will see in code. Thank you!
> 
> R:           [https://www.kaggle.com/code/rickpack/r-average-prob-per-word-no-gpu?scriptVersionId=179034682](https://www.kaggle.com/code/rickpack/r-average-prob-per-word-no-gpu?scriptVersionId=179034682)
> 
> Python:  [https://www.kaggle.com/code/rickpack/python-average-prob-per-word-no-gpu?scriptVersionId=179035436](https://www.kaggle.com/code/rickpack/python-average-prob-per-word-no-gpu?scriptVersionId=179035436)
> 
> 
> 
> > ## Fae Gaze
> > 
> > [@rickpack](https://www.kaggle.com/rickpack) , I think that the reason that the issue of row sum of the probabilities suggested that you may have a normalization issue. Also different scores of R and python may suggest that they handle the data differently. I mean, even if the same statistical methods or the same algorithm, their implementation in r and Python libraries can differ in terms of numerical precision or optimizations. 
> > 
> > 
> > 


---

> ## RickPackTopic Author
> 
> Fixed! I have not studied why but I appeared to not get a prediction for every record. By left joining test on my predictions and imputing predictions where missing, both notebooks produced unimpresssive scores. Interesting that little differences between the notebooks yielded different scores.
> 
> 
> 
> > ## Fae Gaze
> > 
> > [@rickpack](https://www.kaggle.com/rickpack) , I suggest that the columns used to join datasets are correctly specified and contain matching data formats. After the join, I think it is better to identify any rows where predictions are missing
> > 
> > 
> > 
> > > ## RickPackTopic Author
> > > 
> > > Thank you for your reply. I did not have any NA values in the data frame because of a replacement the code included. However, this version justworked ([https://www.kaggle.com/code/rickpack/r-average-prob-per-prompt-word-no-gpu?scriptVersionId=185084007](https://www.kaggle.com/code/rickpack/r-average-prob-per-prompt-word-no-gpu?scriptVersionId=185084007)) after I included a 3rd decimal place (zeros!) in the assignment of values to the 3 target columns where NA occurs. Compare to this version that failed to generate a score ([https://www.kaggle.com/code/rickpack/r-average-prob-per-prompt-word-no-gpu?scriptVersionId=184945388](https://www.kaggle.com/code/rickpack/r-average-prob-per-prompt-word-no-gpu?scriptVersionId=184945388))
> > > 
> > > 
> > > 


---

