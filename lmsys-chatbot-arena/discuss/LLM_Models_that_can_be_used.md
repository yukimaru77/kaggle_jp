# LLM Models that can be used

**superferg** *Sat Jul 06 2024 21:28:26 GMT+0900 (日本標準時)* (26 votes)

May I ask which models everyone has tried? I tried the following model，Randomly select 20% of the samples as the validation set.：

| Model | Local Validation | Public Leaderboard |
| --- | --- | --- |
| Llama3-8B-instruct | 0.9419 | 0.954 |
| Llama3-8B | 0.9818 | 0.987 |
| Gemma2-9B-instruct | 0.9262 | 1.206 |
| Gemma2-9B | 0.9499 | 1.299 |

Gemma2-9B has obtained abnormal results, I guess it might be a problem with the inference. Does anyone have similar problems?

UPDATE:

With the [new public notebook](https://www.kaggle.com/code/emiz6413/inference-gemma-2-9b-4-bit-qlora), the correct results were obtained.

| Model | Local Validation | Public Leaderboard |
| --- | --- | --- |
| Llama3-8B-instruct | 0.9419 | 0.954 |
| Llama3-8B | 0.9818 | 0.987 |
| Gemma2-9B-instruct | 0.9262 | 0.930 |
| Gemma2-9B | 0.9499 | TODO… |


---

 # Comments from other users

> ## Valentin Werner
> 
> gonna leave this one here 😉
> 
> 
> 
> > ## superfergTopic Author
> > 
> > The current local validation set is 0.91X, I still can't migrate to LB. LoL
> > 
> > 
> > 
> > ## SAY WHAT
> > 
> > so funny！！！
> > 
> > 
> > 


---

> ## Valentin Werner
> 
> Gemma2-9B came out recently. The 9B makes it even harder to train, but it tops the performance benchmarks among these models
> 
> 
> 
> > ## Cody_Null
> > 
> > Were you able to pull the gemma2-9B into kaggle from huggingface or are you using the Gemma 2 · gemma-2-9b-pt · V1 on kaggle models? 
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > We pulled gemma2-9b from huggingface into kaggle.
> > > 
> > > 
> > > 
> > ## s111mple
> > 
> > Finetuned model donnot get fine results~ Have you tried it?
> > 
> > 
> > 


---

> ## xiaotingting
> 
> It seems that the validation set index is positively correlated with the public score, and there is still room for further improvement of the index.
> 
> 
> 


---

> ## Xiot1206
> 
> thanks for providing these key information
> 
> 
> 


---

> ## lllleeeo
> 
> As an nlp newbie, I'd like to ask a possibly stupid question, how did you determine how many parameters you needed to use to participate in the fine-tuning, did you try them one by one? How much is generally best based on experience, is it different for different models, I observed that the public laptop fine-tuning in liama 8b only used 0.02% of the parameters is this too little?
> 
> 
> 
> > ## superfergTopic Author
> > 
> > If there is not enough computing power, using the Lora fine-tuning method may be the only choice.
> > 
> > 
> > 
> > > ## lllleeeo
> > > 
> > > Thanks for your reply! I've rented an A100 and a 4090 and want to do some experiments in parallel, I'm wondering if I can try more parameters based on that computing power, but I'm not sure how much I should start trying.
> > > 
> > > 
> > > 
> > > ## superfergTopic Author
> > > 
> > > The first step can try the top-level public notebook.
> > > 
> > > 
> > > 
> > > ## lllleeeo
> > > 
> > > Thank you it works！
> > > 
> > > 
> > > 


---

> ## Mr.T
> 
> How do you load gemma 2-9b during inference?
> 
> 
> 
> > ## superfergTopic Author
> > 
> > Please refer to the notebook below：
> > 
> > [https://www.kaggle.com/code/emiz6413/inference-gemma-2-9b-4-bit-qlora](https://www.kaggle.com/code/emiz6413/inference-gemma-2-9b-4-bit-qlora)
> > 
> > 
> > 


---

> ## EISLab_hwlee
> 
> Can the Gemma2-27B-instruct model perform better?
> 
> 
> 
> > ## EISLab_hwlee
> > 
> > As a result of the experiment, it was observed that the performance was poor.
> > 
> > 
> > 
> > > ## superfergTopic Author
> > > 
> > > I still can't complete the reasoning of 27B within 9 hours, theoretically, 27B should achieve better results.
> > > 
> > > 
> > > 
> > > ## EISLab_hwlee
> > > 
> > > I also failed to submit it.
> > > 
> > > However, in training, the loss did not fall below 1.0, and the evaluation loss did not fall below 1.0.
> > > 
> > > 
> > > 


---

> ## hn
> 
> Just curious, what was the missing piece that lead to your poor inference results from Gemma2? I see that you mentioned it’s fixed with the public notebook 
> 
> 
> 
> > ## superfergTopic Author
> > 
> > I don't have enough time to figure out the reason, but you can analyze the reason by comparing the following two notebooks.
> > 
> > [https://www.kaggle.com/code/emiz6413/llama-3-8b-38-faster-inference](https://www.kaggle.com/code/emiz6413/llama-3-8b-38-faster-inference)
> > 
> > [https://www.kaggle.com/code/emiz6413/inference-gemma-2-9b-4-bit-qlora](https://www.kaggle.com/code/emiz6413/inference-gemma-2-9b-4-bit-qlora)
> > 
> > 
> > 


---

> ## Mukatai
> 
> In a recent public notebook, a score of 0.941 was recorded with fine-tuning of Gemma2, but this table shows a score of 0.930 with Gemma2-9B-instruct. Is there any difference?
> 
> 
> 
> > ## superfergTopic Author
> > 
> > I am using my own training script, so there should be some differences, I can make it public after the competition ends.
> > 
> > 
> > 
> > > ## Mukatai
> > > 
> > > Thank you. Is Gemma's training conducted on Kaggle? With a public notebook, training on a single dataset exceeds the 30-hour weekly limit
> > > 
> > > 
> > > 


---

> ## Femca7
> 
> May I ask the results you get is from pre-trained or finetuned model ?
> 
> 
> 
> > ## superfergTopic Author
> > 
> > You can see the details in the table I provided, those with an 'instruct' suffix are fine-tuned models.
> > 
> > 
> > 


---

> ## yechenzhi1
> 
> May I ask if Instruct model is better than the base model? I have only tried Instruct model.
> 
> 
> 
> > ## superfergTopic Author
> > 
> > According to my local testing, Llama3-8B instruct is better than Llama3-8B. But perhaps the appropriate hyperparameters for  Llama3-8B have not been found.
> > 
> > 
> > 
> > ## ducnh279
> > 
> > I also had a similar question in the early days when I started with fine-tuning decoder-only models for text classification! 
> > 
> > I asked [@rasbtn](https://www.kaggle.com/rasbtn) (a prominent researcher/educator) on Twitter! He replied:
> > 
> > I also conducted some experiments, and the results indicate that using instruction-tuned versions often gives better performance and faster convergence compared to the base model.
> > 
> > 
> > 
> > > ## yechenzhi1
> > > 
> > > Thanks! That's really helpful!
> > > 
> > > 
> > > 


---

