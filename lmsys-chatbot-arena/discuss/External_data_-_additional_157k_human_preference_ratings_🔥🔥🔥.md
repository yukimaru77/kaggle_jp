# External data - additional 157k human preference ratings 🔥🔥🔥

**Darek Kłeczek** *Fri May 03 2024 07:09:30 GMT+0900 (日本標準時)* (96 votes)

I'm super excited to see if smaller models (Kaggle GPU compatible) can effectively rate responses from much larger LLMs. To help you improve your models, I published a dataset with external data:

[https://www.kaggle.com/datasets/thedrcat/llm-human-preference-data-ultrafeedback/data](https://www.kaggle.com/datasets/thedrcat/llm-human-preference-data-ultrafeedback/data)

This is based on Ultrafeedback dataset published on HF by Argilla. I additionally converted it into the competition train data format. 

EDIT: Note that Ultrafeedback uses GPT4 as a judge as a proxy for human raters. I also added ties between models in version 2 that were previously filtered out. See original dataset paper [here](https://arxiv.org/pdf/2310.01377). Thanks [@nbroad](https://www.kaggle.com/nbroad) for catching this. 

Enjoy ❤️🙏👍



---

 # Comments from other users

> ## Dlond Mike
> 
> no use…but just for my notebook
> 
> 
> 


---

> ## Rich Olson
> 
> I added 50k of the items from this to my "Deberta + TF-IDF + Word2Vec + Length" notebook (it's public - I'd post a link - but Kaggle thinks I'm spamming).
> 
> got an identical 1.011 on the LB.  Had same experience with [this dataset](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/500973).
> 
> I take this as indication the data is probably good (or at least not bad) - it's just my notebook isn't able to benefit from the extra data.
> 
> 
> 


---

> ## Nicholas Broad
> 
> How do you think the tie should be handled? If the scores are equal, it should be a tie? (Your dataset only has "model a" winning)
> 
> Update:
> 
> I read more into how they processed the dataset and I noticed a few things:
> 
> I don't think this is human preferences. I think this is using [GPT-4 to rate the responses](https://github.com/OpenBMB/UltraFeedback/tree/main?tab=readme-ov-file#introduction)
> [Ultrafeedback intentionally filters out ties](https://huggingface.co/datasets/argilla/ultrafeedback-binarized-preferences/blob/main/README.md#dataset-processing), whereas the LMSYS dataset has roughly even split between model a winning, b winning, and ties.  
> 
> 
> > ## Darek KłeczekTopic Author
> > 
> > Great catch, thanks! I'll update the thread. I think this can be still useful for pretraining or pseudolabeling. Also found the paper here: [https://arxiv.org/pdf/2310.01377](https://arxiv.org/pdf/2310.01377)
> > 
> > 
> > 
> > > ## Darek KłeczekTopic Author
> > > 
> > > I'll see if I can reproduce the binarization while keeping ties too. 
> > > 
> > > 
> > > 
> > > ## Darek KłeczekTopic Author
> > > 
> > > Version 2 of the [dataset](https://www.kaggle.com/datasets/thedrcat/llm-human-preference-data-ultrafeedback) has ties between models added now. 
> > > 
> > > 
> > > 
> > > ## Turbo
> > > 
> > > Intersting dataset.
> > > 
> > > Did you use this dataset and boost your score?
> > > 
> > > 
> > > 


---

> ## eli plutchok
> 
> Wouldn't you expect gpt-4 rankings to be very different than human rankings? 
> 
> 
> 
> > ## Darek KłeczekTopic Author
> > 
> > There's research pointing that GPT-4 correlates well with human ratings, for example [here](https://arxiv.org/pdf/2306.05685):
> > 
> > The agreement […] between GPT-4 and humans reaches 85%, which is even higher than the agreement among humans (81%). This means GPT-4’s judgments closely align with the majority of humans.
> > 
> > 
> > 
> > > ## eli plutchok
> > > 
> > > Wow. Have you tested GPT4 on the training examples to see how well it scores?
> > > 
> > > 
> > > 


---

> ## justin1357
> 
> Is any data from kaggle covered in this dataset?
> 
> 
> 


---

