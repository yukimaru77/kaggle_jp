# Prediction Using Generation Header

**Takamichi Toda** *Tue Jul 16 2024 16:07:36 GMT+0900 (日本標準時)* (33 votes)

This is still a tried and tested idea and has not yet been successful in my current environment, but I would like to share it.

Currently, from what I can see in public code, the mainstream approach seems to be to base it on Llama or other LLMs and use LoRA to train a classification head. However, LLMs are originally trained to predict the next token, so I think this method is inefficient as it diverges from the original training of the LLM.

My idea is to use the same generative header (CausalLM) as the original LLM.

I adjust the prompts and use the generation probabilities of the tokens A, B and tie.　The predictions are post-processed using softmax so that they sum to one.

Below is a simple sample code:

```
text = """
### Instruction
Which model's answer is appropriate for the prompt?　If both are appropriate, answer `tie`.

### Prompt
{prompt text}

### A
{response A}

### B
{response B}

### Answer
"""

inputs = tokenizer(text)
out = model(inputs)
pred_token_id = tokenizer.encode("A") + tokenizer.encode("B") + tokenizer.encode("tie")
pred = out.logits[0, -1, pred_token_id].softmax(0)

```

Here is the code that evaluates this method using Llama3 8B.

[https://www.kaggle.com/code/takamichitoda/lmsys-zeroshot-prediction](https://www.kaggle.com/code/takamichitoda/lmsys-zeroshot-prediction)

Llama3 has not undergone any special fine-tuning and is used as loaded from the Kaggle model. The evaluation data uses 1/5 of the competition data, which is equivalent to my current validation strategy (correlates well with the public leaderboard).

As a result, we obtained a score of 1.234. It was surprising to me that I could achieve such a result with ZeroShot.

Currently, I am performing SFT on the competition data and adjusting the prompts. However, models that learn classification headers still score better.

Are there others working on a similar approach?



---

 # Comments from other users

> ## James Day
> 
> I tried a similar experiment, primarily because I was hoping to take advantage of training and inference libraries for causal language models that are faster and more memory efficient than the HuggingFace transformers library, namely unsloth and vLLM. However, I actually finetuned the LLMs, as opposed to just doing zero shot inference like [@takamichitoda](https://www.kaggle.com/takamichitoda)'s initial experiment.
> 
> I got 0.902 (CV) with Llama 3 8B Instruct doing next token prediction, which is almost as good as I've been getting with "normal" Llama 3 based classification models. However, the same approach did not work well with Gemma 2 9B (0.990 CV 🤮), possibly due to Gemma's tied embeddings. My CV scores are pretty consistently ~0.03 lower than the corresponding LB scores, so those results translate to ~0.93 & 1.02 LB, which isn't good enough for me to bother submitting.
> 
> 
> 
> > ## Takamichi TodaTopic Author
> > 
> > Thank you for sharing
> > 
> > 0.9 is a great score for me ;)
> > 
> > By the way, I would like to know if possible, what kind of prompt did you use to perform finetuning?
> > 
> > I am using trl's SFTTrainer and learning only output with DataCollatorForCompletionOnlyLM.
> > 
> > 
> > 
> > > ## James Day
> > > 
> > > I used prompts like:
> > > 
> > > ```
> > > Which one of the chatbots below did a better job responding to the user request? Or were they tied?
> > > 
> > > ~~~~~~~~~~ CONVERSATION WITH BOT A ~~~~~~~~~~
> > > 
> > > ### User: "{initial prompt}"
> > > 
> > > ### Bot A Response: "{initial response}"
> > > 
> > > ### User: "{maybe a follow up prompt if available - I included as many conversation turns as will fit in a 3k token context window, discarding the first part of each conversation if necessary}"
> > > 
> > > ### Bot A Response: "{follow up response}"
> > > 
> > > ~~~~~~~~~~ CONVERSATION WITH BOT B ~~~~~~~~~~
> > > 
> > > ### User: "{...}"
> > > 
> > > ### Bot B Response: "{...}"
> > > 
> > > ### User: "{...}"
> > > 
> > > ### Bot B Response: "{...}"
> > > 
> > > ### BEST RESPONSE:
> > > 
> > > ```
> > > 
> > > It was then trained to output " A", " B", or " Tie". The spaces were part of the response tokens.
> > > 
> > > 
> > > 
> > ## Valentin Werner
> > 
> > Do you have the CV discrepancy only for this experiment or for all your models? We did several experiments where it is way below 0.01 in difference, and some where its similar to yours
> > 
> > 
> > 
> > > ## James Day
> > > 
> > > All experiments.
> > > 
> > > Also, I was oversimplifying for the sake of being able to do the math in my head. A more precise estimate of what 0.902 CV translates to on the leaderboard would be 0.902*0.890 + 0.125 = 0.928. The CV-LB correlation data that is based on is included below.
> > > 
> > > 
> > > 
> > > ## ShelterW
> > > 
> > > I think it is your extra prompts that cause the relatively big difference between CV and LB.
> > > 
> > > By the way, do you use qlora or lora to finetune llm？
> > > 
> > > 
> > > 
> > > ## James Day
> > > 
> > > I use qlora.
> > > 
> > > As for the difference between my CV & LB scores, I doubt it has anything to do with the use of external training datasets not provided by the competition organizers (which I assume is what you meant by "extra prompts"), primarily because I did not observe any significant deviations from the preexisting trendline when adding extra data. I think a more likely explanation is that the data provided by the competition organizers isn't perfectly representative of their test data. For example, they may have partitioned their data based on the date on which each conversation occurred, thereby causing the test data to contain responses from new models that aren't present in the training data (or my cross validation data for that matter).
> > > 
> > > Also, one consequence of the trendline having a slope < 1 is that the discrepancies tend to get bigger as CV & LB scores improve. Extrapolating to a ridiculous extent, a model with perfect accuracy in cross validation (CV 0) would likely score ~0.125 on the leaderboard, which is a huge score discrepancy.
> > > 
> > > 
> > > 


---

> ## AbaoJiang
> 
> Hi [@takamichitoda](https://www.kaggle.com/takamichitoda),
> 
> As you mentioned, the performance of Zeroshot prediction is 1.234, which doesn't surpass the score of 1.098 by predicting the global mean.
> 
> However, it's still an interesting idea to try. Thanks for your sharing!
> 
> 
> 
> > ## Valentin Werner
> > 
> > I think the issue is in the softmax assumption without training the models first. The model has basically no intent to predict "A", "B" or "tie" whatsoever, if it not finetuned to realize it should do so. Therefore, the logits are also pretty much nonesense. 
> > 
> > This simple baseline experiment they did does not speak at all for whether their actual experiment will work or how well it will perform.
> > 
> > To me, at first glance I do not see any benefit over the seq class approach directly, as you still probably need to disable the autoregressive generation etc. But it definetly is an interesting idea
> > 
> > 
> > 
> > ## Takamichi TodaTopic Author
> > 
> > I was able to improve the score to 1.037 with SFT and Prompt Tuning. Although the classification header is still better, I intend to continue verification.
> > 
> > 
> > 
> > > ## ShelterW
> > > 
> > > I used SFT to finetune the llama3-8b and improved the LB score to 0.935 [here](https://www.kaggle.com/code/shelterw/training-llama3-8b-4-bit-qlora-sft), welcome to refer to and make suggestions.
> > > 
> > > 
> > > 


---

