# More Interesting Observations to Share

**AbaoJiang** *Thu May 30 2024 01:06:45 GMT+0900 (日本標準時)* (17 votes)

Hi everyone,

Continuing [the previous discussion](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/508200), we want to share some more interesting observations.

### Empty Prompts

We all know that there exist missing responses, either None or empty (now  detected with regex ^\s*$). Today, we observe there are 5 samples with at least one empty prompt present during the conversation,

[](https://postimg.cc/q6hgRT8P)

Most of the time, models can continue to respond normally even if an empty prompt is sent by users. Another finding is that some models will throw an error message if an empty prompt is sent,

### Winner is the Model with an Missing Response

For a single-turn conversation, we expect the winner to be the one with a non-missing response. However, there's an interesting sample in which the winner is the model with an empty response, "" . Looking into the prompt, we realize what's going on! The prompt says Please reply with “<|endoftext|>”.

[](https://postimg.cc/GB9kYHnN)

That's all, happy kaggling!



---

 # Comments from other users

> ## Hafiz Nouman
> 
> Thanks for sharing this valuable information with references.
> 
> 
> 


---

