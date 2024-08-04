# TF-IDF -> Boosted Trees [LB 1.038]

**Rich Olson** *Tue May 07 2024 10:44:19 GMT+0900 (日本標準時)* (1 votes)

Hey all -

Sharing my first (working) effort at this:

[https://www.kaggle.com/code/richolson/lmsys-tf-idf-boosted-trees](https://www.kaggle.com/code/richolson/lmsys-tf-idf-boosted-trees)

Simple idea is to use TF-IDF for vectorizing the texts - then see if a gradient boosted tree framework (LightGBM) can figure it out.

The TF-IDF vectorizer is fitted on prompt, response_a and response_b.

Vectorization is done on response_a and response_b separately and then combined in an hstack - and then LightGBM is trained on the whole mess.

(Using prompt for training didn't seem to obviously improve performance).

Vectorization + training takes about 30 minutes on CPU.  I don't have a time estimate on inference - but it's fast on just CPU.

I had minimal luck when vectorizing with ngram_range=(3, 5).  Performance improved a bunch when I changed that to ngram_range=(1, 5).  This approach working may be a lot about simple word frequency.

Another version of the notebook uses XGBoost - which trains much slower (about 2.5 hours).  That one is still scoring as I type this (I suspect it will have an LB score about the same).  I tried speeding up XGBoost using GPU - but for some reason it wouldn't converge.

Since I'm able to train-on-submission - one interesting option might be to try fitting the vectorizer on the test data (and then using that to vectorize the training data)…

Hope this is helpful to someone!

-Rich

Side note: I just noticed validation on LightGBM reported a log-loss score of 1.036.. - shockingly close to my LB of 1.038! I can't recall another time I've had that happen…



---

 # Comments from other users

> ## Rich OlsonTopic Author
> 
> The XGBoost version finished scoring - 1.039 on the LB.
> 
> Considering XGBoost took much, much longer to train - I'll stick with LightGBM for this notebook.
> 
> If you're curious to see the XGBoost code - just look a version 8 of this notebook.
> 
> 
> 


---

