# [Insights] on 165k Dataset and Model Performance

**justin1357** *Thu Aug 01 2024 20:21:38 GMT+0900 (日本標準時)* (39 votes)

In the past two days, I attempted to integrate the 165k dataset proposed in the discussion area three months ago into the training pipeline. However, this attempt failed on the leaderboard. Therefore, I carefully reviewed the information of this dataset.

Deduplication: I performed deduplication on the 165k dataset and the 55k Kaggle dataset at the prompt and response level. There was no significant duplication found, indicating that the performance decline was not due to overfitting on duplicate data.

Data Source Analysis: After ruling out technical issues, I examined the source of the data. Many people know that this dataset comes from UltraFeedback. However, what most people do not know is that the prompts are not human-generated but sourced from various evaluation datasets such as UltraChat, ShareGPT, Evol-Instruct, TruthfulQA, FalseQA, and FLAN. I believe this is the main reason for the performance drop—the distribution of human prompts from Chatbot Arena differs significantly from the prompts in professional evaluation datasets, which misleads the model.

Model Performance Explanation: This also explains why LLama-3.1, despite performing exceptionally well on various evaluation datasets, did not perform well in this competition. LLama-3.1 uses DPO (Direct Preference Optimization), which essentially "overfits" the professional evaluation prompts. However, these differ from the prompt distribution collected by ChatBot Arena, leading to different standards for evaluating responses.

Successful Models Analysis: This also explains why models like Gemma-2 and LLama-3 performed well in this competition. They share a common feature in the post-training phase: using RLHF (Reinforcement Learning from Human Feedback). Although this method is more costly compared to automatic learning methods like DPO, it aligns more closely with the real human prompt distribution, allowing the model to better understand real human prompts.

Testing Results: I also tested several Gemma-2 models fine-tuned with DPO or SimPO on the UltraFeedback dataset, and their performance was unsatisfactory. This indirectly reflects the issues with DPO-like methods.

I hope these insights are helpful to you. If you found this response useful, I would greatly appreciate your vote.



---

 # Comments from other users

> ## xiaotingting
> 
> Yes, I feel that the processing of data in this competition may be an important point for the increase in the later stage.
> 
> 
> 


---

