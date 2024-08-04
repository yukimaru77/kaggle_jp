# Why LLAMA3 dominates the leaderboards, not deberta.

**kagglethebest** *Fri Jul 05 2024 22:41:58 GMT+0900 (日本標準時)* (6 votes)

When I looked at the public notebook, I was surprised to find that LLAMA3 had the highest score, not Deberta. I have the impression that there are competitions about text classification tasks (let's say this competition is also text classification tasks), and basically Deberta is the optimal solution, at least not by a large margin.

I think there could be two reasons for this:

We haven't found a more suitable categorical loss function for deberta.
Decoder Only models such as LLAMA are more sensitive to the text output by LLMs.

ps: Please let me know if anyone uses Deberta to exceed the score of the best LLAMA notebook.



---

 # Comments from other users

> ## Valentin Werner
> 
> I think your second reason definetly applies. But you should also acknowledge that Llama3-8B has 20x amount of parameters compared to DeBERTa and was pre-trained accordingly. It will be able to represent language much better. Simply adding an classification head will make up the difference between encoding and decoding.
> 
> If I am not mistaken, the architectural differences between encoder-only (DeBERTa) and decoder-only (LLama) for seq classification are marginal, as the decoder are no longer in need to generate the next tokens auto-regressively and instead will generate the classification, just like encoders do.
> 
> Often, the amount of parameters only makes a small difference towards a better score, however, as this problem his very nuanced (even a human could not predict the dataset very well), the sheer amount of parameters helps learning these nuances. This problem is simply too complex for DeBERTa, in my opinion.
> 
> 
> 
> > ## Cristóbal Mackenzie
> > 
> > This makes sense, since I gave a couple of shots using TinyLlama and absolutely failed. Amount of parameters seems to be key for learning anything at all in this problem.
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > I heard some people had some success with Deberta XS regarding "anything at all". But my best DeBERTa (Large) got barely below 1.0, which already included some secret sauce
> > > 
> > > 
> > > 
> > > ## justin1357
> > > 
> > > Could llama be much better?
> > > 
> > > 
> > > 


---

