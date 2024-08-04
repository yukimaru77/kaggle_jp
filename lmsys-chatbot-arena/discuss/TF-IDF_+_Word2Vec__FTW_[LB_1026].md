# TF-IDF + Word2Vec = FTW [LB 1.026]

**Rich Olson** *Thu May 09 2024 15:54:49 GMT+0900 (日本標準時)* (4 votes)

I've posted a new notebook that shows to combine TF-IDF with Word2Vec to get an LB of 1.026:

[https://www.kaggle.com/code/richolson/tf-idf-word2vec-ftw-lb-1-026](https://www.kaggle.com/code/richolson/tf-idf-word2vec-ftw-lb-1-026)

This builds on my prior TF-IDF only notebook (LB 1.038):

[https://www.kaggle.com/code/richolson/lmsys-tf-idf-boosted-trees](https://www.kaggle.com/code/richolson/lmsys-tf-idf-boosted-trees)

As previously - I'm using LGBMClassifier for deciphering things…

In one version of the notebook - I just used Word2Vec - and it alone was good for LB 1.038 (same as TF-IDF):

[https://www.kaggle.com/code/richolson/tf-idf-word2vec-ftw?scriptVersionId=176534641](https://www.kaggle.com/code/richolson/tf-idf-word2vec-ftw?scriptVersionId=176534641)

(this might actually be the more interesting bit - as I don't think anyone has shared a notebook using Word2Vec for this competition yet)

Since both TF-IDF and Word2Vec each score 1.038 on the LB separately - but manage 1.026 together - they presumably are generating features that are a little unique.

I've seen some other notebooks combining TF-IDF with other simple features (like text length) to boost score.  It might be that tossing in Word2Vec can boost things further.



