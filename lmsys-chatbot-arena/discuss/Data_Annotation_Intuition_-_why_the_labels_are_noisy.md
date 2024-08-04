# Data Annotation Intuition - why the labels are noisy

**Valentin Werner** *Mon May 13 2024 23:10:26 GMT+0900 (日本標準時)* (32 votes)

I see that there are several ongoing discussions regarding label quality. As someone, who has spent a significant amount of time annotating data (and asking other people to annotate data for me), I want to share an opinion and intution of mine too.

In Data Annotation, you generally want professionals to annotate the data. They are supposed to (but sometimes do not do so) read the data carefully, select the labels carefully etc.; the annotated data is considered the GROUND TRUTH as these experts should be able to objectively decide the correct label (given same understand of the problem and annotation task). 

Then you generally compute an Inter-Annotator Agreement (are n people giving the same label on the same text), which was often seen as a ceiling for performance. Although this is not always the case in reality, this makes sense, because that means that your model is able to learn the intersection of knowledge from multiple annotators. 

Why is this important? The data we are training on is annotated by random people who wanted to try LLMs. While LMSYS is a great tool that I often use and recommend, it is for our problem mostly an annotation tool where the annotator can decide what question they want to annotate for and the data to annotate is generated in real time. 

However, there are several issues with this for our challenge:

- Users are not experts in using or understanding LLMs

- Users are often not experts in the topic they are asking about (and are often not fact-checking the responses)

- Unless users specify the same prompt and receive the same response, there is no way to evaluate Inter-Annotator Agreement

- LMSYS does not allow to undo or redo annotations (e.g., misclicked the wrong side)

- And most importantly: users have different preferences. This annotation task is not objective at all but PURELY subjective

This means we have NOISY labels and should employ techniques to deal with this; there are techniques such as active learning, ensembling, changing loss etc. which might work to address this issue - all of this needs to be tested (although ensembling is something we will do anyways 😉).



---

 # Comments from other users

> ## aotiandragon
> 
> Thanks a lot, It helped me to know the datas
> 
> 
> 


---

> ## Pranav Belhekar
> 
> Thanks for sharing your point. It helped me to analyze the competition.
> 
> 
> 


---

> ## Fae Gaze
> 
> Excellent insights on label noise! You might also explore robust loss functions like focal loss to mitigate noise impact, and consider frameworks like Snorkel to efficiently manage training data through programmable labeling functions
> 
> 
> 
> > ## Valentin WernerTopic Author
> > 
> > Have not heard of Snorkel yet - can you recommend some literature? 
> > 
> > 
> > 


---

> ## Takamichi Toda
> 
> Thank you for sharing. And I was thinking the same thing just now.
> 
> There are some samples in the training data consisting only of very short prompts (one word). A typical example is when the prompt is just "hey". The responses of LLMs to this can generally be divided into two patterns:
> 
> Simply respond with "Hello!".
> After saying "Hello", provide a cue to continue the conversation, such as "How can I assist you today?".
> 
> I think 2 seems to be better, but the training data shows that there were a reasonable number of tie and cases where 1 was winning.
> 
> |  | n_sample | id |
> | --- | --- | --- |
> | hello_lose | 5 | 189242591, 211357242, 326037335, 458677274, 3947327386 |
> | tie | 4 | 1329170872, 3422926530, 4197301939, 4265282380 |
> | hello_win | 2 | 1655058446, 2171261721 |
> 
> The "hay" pattern trend seems to be more to my liking (2 mostly), but there are many other patterns like this that need to be treated as a NOISY label, as you say.
> 
> 
> 
> > ## Valentin WernerTopic Author
> > 
> > And I think is one on the more obvious side, where people just voted a side eventhough both models give the same answer. These people were obviously not thinking of poor ML Developers that need to explain why they did it 😉
> > 
> > I think evaluating how truthful the responses are (if there is a good way to do it) could also be a good feature for training our models
> > 
> > 
> > 


---

> ## Lisa DunlapCompetition Host
> 
> I think this is an amazing point: one of the big challenges with this challenge (no pun intended) - the data is crowdsourced with very minimal filtering so learning how to deal with label noise is incredibly important!
> 
> 
> 


---

> ## JunHua Liao
> 
> I have also discovered the issue of labels noise, mainly due to the same prompt and reponses, where there is a winner, which should be winner_tie. The two solutions currently in mind are: (1). Change the label to winner_tie; (2) Delete noise data
> 
> 
> 
> > ## Lisa DunlapCompetition Host
> > 
> > It may also be beneficial to look in to prompt deduplication or down weighting overrepresented prompts
> > 
> > 
> > 


---

> ## xiaotingting
> 
> At present, cleaning data and selecting models have the greatest impact on the results. I feel that no matter what field you are in, even if you use a large model, the quality of the data is very important.
> 
> 
> 
> > ## Valentin WernerTopic Author
> > 
> > Looking forward to see how you cleaned data, we tried it a bit but were not able to get it to a point where it actually helped
> > 
> > 
> > 
> > > ## Fae Gaze
> > > 
> > > Hi, that is right. Too much cleaning will affect on the score adversely
> > > 
> > > 
> > > 


---

> ## AbChk
> 
> Thanks for sharing your point. It seems like this issue makes us wonder if the test data also has noisy labels?
> 
> 
> 
> > ## Valentin WernerTopic Author
> > 
> > very likely so. I (maybe not so) boldly assume that they did not manually check 25k samples for quality. It is like chosen based on label distribution and models.
> > 
> > 
> > 
> > ## Fae Gaze
> > 
> > the test is also noisy. But, we are not able to clean the noise. Even cleaning the training will affect the score
> > 
> > 
> > 


---

