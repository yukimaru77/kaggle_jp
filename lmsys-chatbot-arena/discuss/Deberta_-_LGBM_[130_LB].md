# Deberta -> LGBM [1.30 LB]

**Rich Olson** *Sat May 11 2024 10:04:01 GMT+0900 (日本標準時)* (3 votes)

Just shared my Deberta-feature-extraction -> LGBM notebook here:

[https://www.kaggle.com/code/richolson/deberta](https://www.kaggle.com/code/richolson/deberta)

Score is 1.030 on the LB.

I train / submit on the same run.  Runtime is about 3 hours on P100.  Most of that is Deberta doing feature extraction (LGBM train / inference is comparatively fast).

Submission is probably about 90 minutes longer (since feature extraction needs to be done on test also).

I'm using deberta-base (presumably this would run faster with a smaller model).

One note - I'll typically do quick-test-runs with 1-5k prompts to see if things are generally working.  That was enough for TF-IDF to show some results.  For whatever reason - this produced zero results with Deberta.

Once I started training on 10k+ samples - then things started to converge for me.

So - if your Deberta model isn't doing anything - maybe try more data…

I also have a related kitchen-sink notebook that's currently scoring:

[https://www.kaggle.com/code/richolson/deberta-tf-idf-word2vec](https://www.kaggle.com/code/richolson/deberta-tf-idf-word2vec)



