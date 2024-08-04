# Data Understanding: Why prompt is list of strings?

**Siddhantoon** *Mon May 06 2024 20:36:28 GMT+0900 (日本標準時)* (19 votes)

| prompt examples |
| --- |
| ["Is it morally right to try to have a certain percentage of females on managerial positions?","OK, does pineapple belong on a pizza? Relax and give me fun answer."] |
| ["hey","write \"lollipop\" reversed"] |
| ["What's the difference between a sine and a line?","can you explain it even simpilier to me using examples?","how does a sine keep going or whats an analogy using sine the expresses a continuation?","What if AI becomes better than humans at everything. Maybe come up with an analogy involving geometry, thanks"] |

For some the output of model a and b is also list of 2 strings for some it is single string.



---

 # Comments from other users

> ## steubk
> 
> 87% of train samples are chats with single prompt, while others have more prompts and responses
> 
> 
> 


---

> ## namtran
> 
> Thank you for your finding. I will try to extract individual conversations and see if it improves the model.
> 
> 
> 


---

> ## Valentin Werner
> 
> I recommend playing around with the tool in general. This might also gives you a better feeling for the data and competition in general!
> 
> The answer is pretty simple: You are not evaluating individual prompts, but full chats.
> 
> While this opens a new question of "What happens if you evaluate a chat after every prompt" (which is possible) - I don't think it matters for the competition and assume that the data provided is always until the first evaluation.
> 
> 
> 
> > ## SiddhantoonTopic Author
> > 
> > So actually we aren't evaluating a "prompt and response", technically we are evaluating a "chat". This increases the complexity on how long the chat is in the data
> > 
> > 
> > 


---

> ## Rich Olson
> 
> great find.  looking through the data - it seems like this is very common.  
> 
> often the prompts seem disconnected from each-other - but sometimes they are clearly a continuing conversation.
> 
> 
> 


---

> ## Sparsh Tewatia
> 
> Even data is corrupt for around 200 rows, some null values , syntax errors. Will have to check for it in the test data
> 
> 
> 


---

