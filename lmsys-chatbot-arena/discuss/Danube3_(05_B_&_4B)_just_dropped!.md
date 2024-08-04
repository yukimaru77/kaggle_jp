# Danube3 (0.5 B & 4B) just dropped!

**Valentin Werner** *Mon Jul 15 2024 15:57:26 GMT+0900 (日本標準時)* (32 votes)

I have used Danube2 for several experiments and even with QLoRA on Kaggle GPU it seems to be a way better alternative to DeBERTa Large. 

Danube3 just came out as 0.5B and 4B and also comes with a Chat model, which might be an upside for this competition. The 4B model outperforms its 1.5B predecessor on all benchmarks by a lot (also a bit of a size difference), while the 0.5B outperforms Qwen2 0.5B on most benchmarks. However, to me it will be particularly interesting, how the 4B model compares to Phi3-Mini, as this is the only other model I know in its weight class. Maybe this is team Danube's secret? 😉

From my experience smaller models, like 0.5B will still not fit on Kaggle GPUs (it should work on a 4090), so I will focus on the 4B model.

I also want to applaud the H2O Team, which is quite active on Kaggle, on this new release! It is always amazing, when talented researchers and Data Scientists contribute towards the Open LLM efforts (also the sheer speed of new releases). Looking forward to see how good this model is!

Links: 

Model card: [https://huggingface.co/h2oai/h2o-danube3-4b-chat](https://huggingface.co/h2oai/h2o-danube3-4b-chat)

Technical Report: [https://arxiv.org/abs/2407.09276](https://arxiv.org/abs/2407.09276)

Benchmarks:

Some benchmarks I aggrated from the [old open LLM leaderboard](https://huggingface.co/spaces/open-llm-leaderboard-old/open_llm_leaderboard). Danube3 is not included in the leaderboard yet, but reports these values on their model card. I think it is very interesting to see how close Danube3 comes to Gemma-7B and Mistral-7B.

| Category | Benchmark | Danube3-4b-Chat | Danube2-1.8B-Chat | Phi-3-Mini-4K-Ins | Gemma-7B | Mistral-7B Ins 0.2 |
| --- | --- | --- | --- | --- | --- | --- |
| Popular aggregated | MMLU  (5-shot) | 54.74 | 37.77 | 69.08 | 64.56 | 60.78 |
| Language Understanding | HellaSwag (5-shot) | 80.36 | 73.54 | 80.60 | 82.20 | 84.88 |
| Reasoning | ARC Challenge (5-shot) | 58.96 | 43.43 | 62.97 | 61.09 | 63.14 |
|  | TruthfulQA (0-shot) | 47.79 | 39.96 | 59.88 | 44.79 | 68.26 |
|  | WinoGrande (5-shot) | 76.48 | 69.77 | 71.6 | 79.01 | 77.19 |
| Math | GSM8K CoT   (5-shot) | 50.18 | 26.16 | 85.7 | 50.87 | 40.03 |
| Average |  | 61.42 | 48.44 | 69.91 | 63.75 | 63.14 |

Models were chosen based on the models microsoft phi3-mini is reporting against on their model card.



---

 # Comments from other users

> ## chaneyMA
> 
> nice work!!!!
> 
> 
> 


---

> ## madarshbb
> 
> Just for curiosity,
> 
> From my experience smaller models, like 0.5B will still not fit on Kaggle GPUs (it should work on a 4090), so I will focus on the 4B model.
> 
> What do you mean by this? Shouldn't 0.5B model be easier to fit than 4B?
> 
> 
> 
> > ## Valentin WernerTopic Author
> > 
> > I mean 0.5 is just big enough so you can't train it on Kaggle without quantization. This is basically similar size as DeBERTa Large
> > 
> > 
> > 


---

> ## Abhay Ayare
> 
> Fantastic guide! Thank you for sharing these valuable resources and insights on becoming a data scientist. Your passion for data science is inspiring. Looking forward to exploring your book "Kaggle for Beginners."
> 
> 
> 
> > ## Valentin WernerTopic Author
> > 
> > There are plenty of kaggle books, but I certainly have not written one of them 😉
> > 
> > 
> > 


---

> ## sayoulala
> 
> Thanks for you share, May I ask that the scores of this competition by the model ?
> 
> 
> 
> > ## Valentin WernerTopic Author
> > 
> > I have no trained it yet. Some experiments (did not try super hard) got danube2-1.8B to .98x for me
> > 
> > 
> > 


---

> ## The-Hai Nguyen
> 
> You are always shedding light on my learning progress all the way back from the PII-detection competition. Really appreciate and thanks for your sharing, it helps me and the others learn a lot throughout the journey 🙏.
> 
> 
> 


---

