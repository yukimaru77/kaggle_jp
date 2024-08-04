# The magic behind Gemma2

**Yixiao Yuan** *Thu Jul 25 2024 05:32:05 GMT+0900 (日本標準時)* (45 votes)

According to other benchmarks, llama3.1 8B should be better than Gemma2. But from our experiments and other discussions, in this competiton, gemma2 is better. We found a possible reason in Gemma2's tech report. Gemma2 is pretrained on LMSYS. 🤣



---

 # Comments from other users

> ## Cody_Null
> 
> LMSYS-Chat-1M?? Does that mean there is a dataset of 1M for LMSYS?
> 
> 
> 
> > ## Kishan Vavdara
> > 
> > Yes, but it only contains conversation. [Here](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/499800)  the earlier discussion. 
> > 
> > 
> > 
> > ## Robson
> > 
> > I found this paper: [https://arxiv.org/pdf/2309.11998](https://arxiv.org/pdf/2309.11998)
> > 
> > 
> > 


---

> ## Valentin Werner
> 
> They trained on it - so you don't have to. 
> 
> It is interesting that they only use prompts, not responses, so the use case is very different from ours. I do not see a large benefit from it, but maybe somebody else can explain to me why this could help?
> 
> At the end of the day, many prompts in the lmsys dataset are VERY bad.
> 
> 
> 
> > ## Sparsh Tewatia
> > 
> > It is good with diffrerentiating between a good and bad answers for these type of prompts but don't know when it should be a tie.
> > 
> > 
> > 


---

> ## yechenzhi1
> 
> Hi, can you share the link to Gemma2's tech report?
> 
> 
> 
> > ## Yixiao YuanTopic Author
> > 
> > [https://storage.googleapis.com/deepmind-media/gemma/gemma-2-report.pdf](https://storage.googleapis.com/deepmind-media/gemma/gemma-2-report.pdf)
> > 
> > 
> > 


---

> ## yuanzhe zhou
> 
> it seems that there are many similar open source dataset?
> 
> 
> 


---

