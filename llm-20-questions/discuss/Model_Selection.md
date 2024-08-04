# Model Selection

**Matthew S Farmer** *Sat Jun 29 2024 00:51:01 GMT+0900 (日本標準時)* (6 votes)

Outside of fine-tuning a model on a specific 20 Q dataset, I've been thinking about how to select the best model for the competition. This has led to me check out the [HF Open LLM Leaderboard](https://huggingface.co/spaces/open-llm-leaderboard/open_llm_leaderboard) and dig into the different benchmarks. 

The key to performance should be deductive reasoning and the model's ability to follow explicit instructions (to help with parsing). That leads me to prioritize two benchmarks:

MUSR and IFEval

MuSR (Multistep Soft Reasoning) (https://arxiv.org/abs/2310.16049) – MuSR is a new dataset consisting of algorithmically generated complex problems, each around 1,000 words in length. The problems include murder mysteries, object placement questions, and team allocation optimizations. Solving these problems requires models to integrate reasoning with long-range context parsing. Few models achieve better than random performance on this dataset.

IFEval (https://arxiv.org/abs/2311.07911) – IFEval is a dataset designed to test a model’s ability to follow explicit instructions, such as “include keyword x” or “use format y.” The focus is on the model’s adherence to formatting instructions rather than the content generated, allowing for the use of strict and rigorous metrics.

- Phi 3, Qwen 2, Openchat 3.5, Yi, Hermes 2… all at the top of the board when considering the benchmarks above. 

- In contrast: Gemma 2 7b it (the starter notebook model) has a MUSR of 12.53 whereas Intel's Neural Chat has a MUSR or 23.02…

Just some things to think about. Happy kaggleing!



---

 # Comments from other users

> ## Azim Sonawalla
> 
> 
> The key to performance should be deductive reasoning and the model's ability to follow explicit instructions (to help with parsing).
> 
> I'm not sure about this assumption.  The bots need reasoning to the extent that they can find a keyword that satisfies up to 20 simultaneous conditions as the questioner/guesser, but actual knowledge of facts in order to come up with late game questions to narrow down the last few candidates.
> 
> I've been toying with the idea that a model trained on a higher token count (e.g. llama3) might do well for this reason, but haven't gotten around to creating an experiment along those lines.
> 
> 
> 
> > ## Matthew S FarmerTopic Author
> > 
> > Interesting objection! Thanks for challenging my assumptions. Following your idea, a multilingual model may be best for this competition since it requires a larger vocabulary training than English only models? 
> > 
> > 
> > 


---

