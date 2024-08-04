# Explanation on the prediction that the model must perform

**GregReds** *Thu Jul 11 2024 05:15:59 GMT+0900 (日本標準時)* (1 votes)

Hello everyone!

I am a master's degree student and I am using this competition for an exam; for educational purposes, I must primarily rely on the use of word embedding. My question and my doubt is: to make predictions and to determine whether to award the win to model a or model b, should the model only check the structure of the responses, or also their correctness?

Let me give an example to be more explicit:

If the prompt were: What is the capital of France?

response_a: The capital of France is Paris.

response_b: The capital of France is Rome.

Typically, a model like word2vec, if not too well-trained, might base its evaluation on the structure rather than the correctness, focusing on the fact that the sentences are structured similarly and this predicting a tie. However, model A should win because the actual capital is indeed Paris, not Rome.

Therefore, it might be useful to utilize word embedding models like Bert that theoretically also check the correctness of the response.

I hope I have made myself clear! Thanks everyone.

[Screenshot 2024-07-10 alle 22.14.58.png](https://storage.googleapis.com/kaggle-forum-message-attachments/2916192/20917/Screenshot 2024-07-10 alle 22.14.58.png)

