# Help! Loss function not behaving as expected!

**Shreyansh Murathia** *Sat Jul 27 2024 22:43:41 GMT+0900 (日本標準時)* (0 votes)

pred = torch.tensor([[1.0, 0.0, 0.0]])

target = torch.tensor([0])

loss_fct = nn.CrossEntropyLoss()

​

loss = loss_fct(pred, target)

loss

​

tensor(0.5514)

Should'nt the loss be 0 or a very small value? Why is it returning 0.5514? 

I am really sorry if this question is very easy. I am fairly new to this loss. 



---

 # Comments from other users

> ## sayoulala
> 
> Answer from gpt4:
> 
> No need to apologize! Your question is absolutely valid, and I'm here to help clarify it for you.
> 
> In your scenario, you are using nn.CrossEntropyLoss from PyTorch, which combines nn.LogSoftmax and nn.NLLLoss (negative log likelihood loss). Let me break down your example and explain why you are getting a loss value of 0.5514.
> 
> CrossEntropyLoss in PyTorch
> 
> nn.CrossEntropyLoss expects:
> 
> pred (predictions): a 2D tensor of raw, unnormalized scores for each class (often called "logits"). Shape: (batch_size, num_classes).
> 
> target: a 1D tensor of the true class indices. Shape: (batch_size,).
> 
> The CrossEntropyLoss applies a LogSoftmax function to the raw scores first, converting them into log-probabilities. It then uses the NLLLoss to compute the negative log likelihood of the correct class.
> 
> In your example:
> 
> python
> 
> import torch
> 
> import torch.nn as nn
> 
> pred = torch.tensor([[1.0, 0.0, 0.0]])
> 
> target = torch.tensor([0])
> 
> loss_fct = nn.CrossEntropyLoss()
> 
> loss = loss_fct(pred, target)
> 
> print(loss)  # Output: tensor(0.5514)
> 
> Step-by-Step Explanation
> 
> Raw logits (pred):
> 
> python
> 
> [[1.0, 0.0, 0.0]]
> 
> Applying LogSoftmax to logits: The LogSoftmax transformation converts logits to log-probabilities. For pred, the resulting log-probabilities are calculated as:
> 
> python
> 
> log_probabilities = torch.log_softmax(pred, dim=1)
> 
> The softmax transformation for your pred would be:
> 
> python
> 
> softmax(pred) = [exp(1.0)/sum(exp(1.0) + exp(0.0) + exp(0.0)),
> 
>                  exp(0.0)/sum(exp(1.0) + exp(0.0) + exp(0.0)),
> 
>                  exp(0.0)/sum(exp(1.0) + exp(0.0) + exp(0.0))]
> 
>              ≈ [0.5761, 0.2119, 0.2119]
> 
> Applying log to the softmax probabilities gives us:
> 
> python
> 
> log_probabilities = [log(0.5761), log(0.2119), log(0.2119)]
> 
>                   ≈ [-0.5514, -1.5514, -1.5514]
> 
> Negative Log Likelihood of the target class: Since the target class is 0 (target = [0]), we take the log-probability of the first element:
> 
> python
> 
> loss = -log_probabilities[0]
> 
>      = -(-0.5514)
> 
>      = 0.5514
> 
> Summary
> 
> The loss value of 0.5514 is not incorrect. It is derived from the log-probability of the correct class (class 0) for your prediction. The fact that the prediction is not perfect (with a raw logit of 1.0 vs. 0.0 for other classes) leads to a non-zero loss.
> 
> Had the logit for class 0 been significantly higher (e.g., [10.0, 0.0, 0.0]), the softmax probability for class 0 would be closer to 1, resulting in a loss closer to 0. Here, the logit of 1 is not high enough to give a near-zero softmax probability and thus results in a non-zero loss.
> 
> Feel free to ask if you have other questions or need further clarification!
> 
> 
> 
> > ## sayoulala
> > 
> > The input should not be probabilities; it should be the values before applying softmax.
> > 
> > 
> > 
> > ## Shreyansh MurathiaTopic Author
> > 
> > Thanks a lot 😊
> > 
> > 
> > 


---

