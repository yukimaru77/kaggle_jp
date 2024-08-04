# New Q20LLM dataset with >78k questions

**ivan** *Tue May 28 2024 02:34:18 GMT+0900 (日本標準時)* (3 votes)

Hi, recently on [Mistral AI hackathon](https://x.com/MistralAILabs/status/1788970688172245256) I've build a new dataset [Q20LLM](https://huggingface.co/datasets/cvmistralparis/Q20LLM) using provided APIs from [Mistral API](https://docs.mistral.ai/api/) and [Groq Cloud](https://docs.mistral.ai/api/).

AFAIK there is no dataset with dialog questions from general to specific. I tried to build such dialogs with LLMs. I also tried to fine-tune "instruction following" model on this dataset, but no success. The model tends to ask as many questions as it saw during training.



