# Additional 21k Labelled Conversations 🚀

**Abdullah Meda** *Wed May 08 2024 01:17:13 GMT+0900 (日本標準時)* (75 votes)

This dataset was from the authors themselves at [https://huggingface.co/datasets/lmsys/chatbot_arena_conversations](https://huggingface.co/datasets/lmsys/chatbot_arena_conversations)

The format was quite different to the one being used here for the competition. I have processed it to be in a similar format. Here they are:

- Dataset: [kaggle.com/datasets/abdullahmeda/lmsys-additional-33k-labelled-conversations](https://www.kaggle.com/datasets/abdullahmeda/lmsys-additional-33k-labelled-conversations)

- Processing Script: [kaggle.com/code/abdullahmeda/33k-lmsys-chatbot-arena-conversations/](https://www.kaggle.com/code/abdullahmeda/33k-lmsys-chatbot-arena-conversations/)

An upvote on the [dataset](https://www.kaggle.com/datasets/abdullahmeda/lmsys-additional-33k-labelled-conversations) would be greatly appreciated. Thank you! 🙏

I'll check if there are any duplicates between the datasets if I do get the time tomorrow. Happy coding!

UPDATE: Using the prompts column as deduplication criteria brings the sample count to around 21k. The dataset and script have been updated.



---

 # Comments from other users

> ## eli plutchok
> 
> Hi [@abdullahmeda](https://www.kaggle.com/abdullahmeda) , I tested adding in this training data, and for some reason  it makes the submission score a lot worse.
> 
> 
> 


---

> ## eli plutchok
> 
> Hey, I just realized that a lot of the lines are already on the main dataset. Maybe you can make a new cleaned version of this removing all the duplicates. I'm not sure about the percentage.
> 
> 
> 
> > ## eli plutchok
> > 
> > I think about a third are duplicates from the main training set, but there are also many duplicates within the data set, and I think there are additional ones that are very similar but not exact duplicates.
> > 
> > 
> > 
> > > ## Abdullah MedaTopic Author
> > > 
> > > [@eliplutchok](https://www.kaggle.com/eliplutchok) You may be right when you say that. I have dropped all rows that have similar prompts for now. More columns can be used as a subset when dropping rows, but I have noticed that lesser rows were dropped when using multiple columns. Using just the prompts as deduplication criteria brings the number down to just 21k new samples. I have updated the script as well as the dataset to reflect this. I'll update the post in a bit
> > > 
> > > ```
> > > superset = pd.concat([external_data, train]).reset_index(drop=True)
> > > external_data_deduplicated = superset.drop_duplicates(subset=['prompt'], keep='last')
> > > external_data_deduplicated = external_data_deduplicated[external_data_deduplicated.index.isin(external_data.index)]
> > > 
> > > len(external_data_deduplicated)
> > > >>> 21187
> > > 
> > > ```
> > > 
> > > 
> > > 
> > > ## eli plutchok
> > > 
> > > Btw, I realized another thing. It seems that the lines that had "tie (both bad)" as the winner, you just left blank, but these should all be counted as ties, or else you are left with only 10% ties u unlike the main dataset which has 30% ties.
> > > 
> > > 
> > > 
> > > ## Abdullah MedaTopic Author
> > > 
> > > [@eliplutchok](https://www.kaggle.com/eliplutchok) Thank you for pointing this out. I have made the respective changes!
> > > 
> > > ```
> > > >>> external_data[['winner_model_a', 'winner_model_b', 'winner_tie']].sum(axis=1).all()
> > > True
> > > 
> > > ```
> > > 
> > > 
> > > 


---

> ## Rich Olson
> 
> I just submitted a version of my 1.011 LB notebook which adds the de-duped version to train:
> 
> [https://www.kaggle.com/code/richolson/deberta-tf-idf-word2vec-length](https://www.kaggle.com/code/richolson/deberta-tf-idf-word2vec-length)
> 
> I'll post what I find out.
> 
> 
> 
> > ## Rich Olson
> > 
> > I got an identical 1.011 on the LB (see version 6 of above notebook).
> > 
> > Same results with using 50k items from the "[ultrafeedback](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/499756)" dataset.
> > 
> > I take this as indication the data is probably good (or at least not bad) - it's just my notebook isn't able to benefit from the extra data.
> > 
> > 
> > 
> > ## Ivan Vybornov
> > 
> > A bulk of data comes from the models that are not present in the actual train set, I doubt this will complement tf-idf approach.
> > 
> > 
> > 


---

> ## xiaotingting
> 
> After adding this dataset, the results are significantly better. The use of additional datasets is indeed useful.
> 
> 
> 
> > ## Erik
> > 
> > Hi, both cv and lb at the same time improved?
> > 
> > 
> > 
> > > ## KeShuang Liu
> > > 
> > > Why did I perform better on cv but worse on lb after using the dataset?
> > > 
> > > 
> > > 


---

> ## eli plutchok
> 
> Have you tried it yet with a submission? I'm scared that taking any external data may unintentionally make my model's predictions on the test data worse.
> 
> 
> 
> > ## Sparsh Tewatia
> > 
> > Bro if you try please update the results here too
> > 
> > 
> > 
> > > ## eli plutchok
> > > 
> > > k, will let you know, I hope to try this tomorrow (for me - I'm in NY).
> > > 
> > > 
> > > 
> > > ## go
> > > 
> > > before add data cv is 1.01
> > > 
> > > after add data cv is 1.03…
> > > 
> > > but I haven't submit this version
> > > 
> > > 
> > > 


---

