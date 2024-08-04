# How to tokenize prompts and responses efficiently

**irishu** *Sun Jul 28 2024 13:56:19 GMT+0900 (日本標準時)* (6 votes)

# Experiment

I have tried the following three methods so far, and the first has performed the best in LB.

### Methods

tokenize up to the max_tokens by joining strings like prompt + responseA + responseB
allocate one-third of the max_tokens to each sentence and tokenize up to the limit
allocate the number of tokens in the appropriate ratio(ex;1:2:2)

### Conditions

- using Gemma-2 9b 4-bit QLoRA

- max_tokens = 1024

- using only the last prompt and responses 

- 1 epoch using all train data

- referring to the excellent work [[Training] Gemma-2 9b 4-bit QLoRA fine-tuning](https://www.kaggle.com/code/emiz6413/training-gemma-2-9b-4-bit-qlora-fine-tuning)

# Question

### Don't you think there is a more efficient way than the simple method1?

Looking at the distribution of the number of tokens in the prompt and response (only the last one), it appears that around 10% of them contain more than 1024 tokens in total. That is, in some cases, response B may not contain enough information.

### How much would a larger max_tokens improve the score?

I have not been able to test this yet due to computational resources.



---

 # Comments from other users

> ## irishuTopic Author
> 
> I changed max_tokens to 2048 in learning and inference and the score improved.
> 
> Now I am wondering if I should adjust the token length with padding.
> 
> 
> 


---

