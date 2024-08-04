# Trying to understand the strength of the models with the highest ties

**Dr. Gopalashivabalasubramanium Chandrashekaran** *Sat Jun 08 2024 09:37:46 GMT+0900 (日本標準時)* (-1 votes)

Good evening everyone,

I had a go at this data and made myself a list of the models with the highest tie rate. It made sense that the non-winner models will be the ones tie-ing. It was interesting to see the models that were subpar tie-ing with each other. 

My question here is: How do I assess the strength of the model based on the count of its ties? It is easy to judge it based on its number of wins. 

Anyone have any findings on this?

Also, if you have time, see my notebook. Would appreciate any feedback.



---

 # Comments from other users

> ## tanaka
> 
> lmsys's elo rating is calculated something like following.
> 
> It means, when ties, higher rank player's score may decrease slightly, while lower-ranked player's score may increase slightly.
> 
> ```
> def compute_online_elo(battles, K=4, SCALE=400, BASE=10, INIT_RATING=1000):
>     rating = defaultdict(lambda: INIT_RATING)
> 
>     for rd, model_a, model_b, winner in battles[['model_a', 'model_b', 'winner']].itertuples():
>         ra = rating[model_a]
>         rb = rating[model_b]
>         ea = 1 / (1 + BASE ** ((rb - ra) / SCALE))
>         eb = 1 / (1 + BASE ** ((ra - rb) / SCALE))
>         if winner == "model_a":
>             sa = 1
>         elif winner == "model_b":
>             sa = 0
>         elif winner == "tie" or winner == "tie (bothbad)":
>             sa = 0.5
>         else:
>             raise Exception(f"unexpected vote {winner}")
>         rating[model_a] += K * (sa - ea)
>         rating[model_b] += K * (1 - sa - eb)
> 
>     # calibrate llama-13b to 800
>     delta = (800-rating["llama-13b"])
>     for model in battles["model_a"].unique():
>         rating[model] += delta
> 
>     return rating
> 
> ```
> 
> Refs
> 
> - [https://colab.research.google.com/drive/1KdwokPjirkTmpO_P1WByFNFiqxWQquwH#scrollTo=hytEb0aXfcwm](https://colab.research.google.com/drive/1KdwokPjirkTmpO_P1WByFNFiqxWQquwH#scrollTo=hytEb0aXfcwm)
> 
> 
> 


---

> ## Valentin Werner
> 
> 
> It was interesting to see the models that were subpar tie-ing with each other.
> 
> It is important to acknowledge that the prompt matters a lot. When presenting prompting in my company, I show a tool a bit like the lmsys arena to raise understanding for when you need the "big guns". On a simple questions, llama2-7B can easily tie gpt4-turbo, such as "what is 2+2?" - you will not need that many parameters to answer this. Now, one model may say "4" and the other one says "Adding 2+2 results in 4." and you may prefer one of the answers. Oops, suddenly Llama2-7B "outperformed" GPT-4?
> 
> Further, we always expect models of the same category to tie more often - not sure if I fully understood your point.
> 
> How do I assess the strength of the model based on the count of its ties? It is easy to judge it based on its number of wins.
> 
> This is what LMSYS is doing on the website. For this competition, we are also predicting ties - so knowing that a model ties a lot should be as good as winning a lot.
> 
> 
> 


---

