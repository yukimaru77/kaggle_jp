# One-Feature Decision Tree

**AbaoJiang** *Wed Jun 05 2024 00:50:58 GMT+0900 (日本標準時)* (3 votes)

Hi everyone,

We've seen many showing that features based on the length difference between response A and B are useful. So, I try to run a quick experiment using DecisionTreeClassifier fed with only a single feature [here](https://www.kaggle.com/code/abaojiang/lmsys-detailed-eda?scriptVersionId=181492294). Following illustrates the decision tree of one fold,

[](https://postimg.cc/Y4YBzCJS)

As can be observed, the model learns the relationship between the length difference feature and winners,

On the right side, the winners are model A, which have longer responses.
In the middle, ties are the majority.
On the left side, the winners are model B.

The approach yields local CV score of 1.0588 with StratifiedKFold, which can't beat our naive baseline. This just another way to explore this important relationship (related to verbosity bias). Hope you find this interesting!



---

 # Comments from other users

> ## Valentin Werner
> 
> Interesting way to show feature value.
> 
> Length is the most valuable feature I found so far, but completely ignores the quality of the answer. I created a feature, that was actually among top 4 of my features, which looks into whether a model says something along the lines of "As an AI I cannot help you with that". This type of qualitative evaluation will be what is needed beyond the structural features such as length (and sadly also the reason why we have to go back go embeddings for some parts).
> 
> 
> 
> > ## AbaoJiangTopic Author
> > 
> > Hi [@valentinwerner](https://www.kaggle.com/valentinwerner),
> > 
> > Thanks for your reply.
> > 
> > I only try structural features so far, and nothing can beat the naive baseline based on the response length difference bucket. Though verbosity bias do exist, there still have much information to be extracted in different ways (e.g., contextual embeddings). Tbh, I'm an NLP newbie, and try to share what I discover during this learning journey. Thanks for your insightful sharing!
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > What baseline are you referring to?
> > > 
> > > Thanks for sharing your insights, its always appreciated!
> > > 
> > > 
> > > 
> > > ## AbaoJiangTopic Author
> > > 
> > > Hi [@valentinwerner](https://www.kaggle.com/valentinwerner),
> > > 
> > > Sorry for the late reply. I mean the naive baseline in the section Length Difference Bucket Mean Prediction of my EDA notebook!
> > > 
> > > 
> > > 


---

> ## KTibow Personal
> 
> A decision tree seemed like an odd choice, so I tried some polynomial regressions. It basically just ends up saying "bigger responses are better".
> 
> 
> 
> > ## AbaoJiangTopic Author
> > 
> > Hi,
> > 
> > The reason why I choose DT is that I want to do comparison with the naive baseline based on the manual binning of response length difference. Because DT itself learns to bin the length difference automatically, I just share that we can observe the similar property from different angles.
> > 
> > Anyway, thanks for your sharing.
> > 
> > 
> > 
> > ## Vishal Maurya
> > 
> > Hii [@ktibow](https://www.kaggle.com/ktibow), thanks for sharing this. Could you share the R2-score of these polynomial models above, I just want to know that how strong and significant relationships are there.
> > 
> > 
> > 


---

