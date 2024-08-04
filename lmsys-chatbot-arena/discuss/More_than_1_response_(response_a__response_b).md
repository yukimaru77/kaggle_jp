# More than 1 response (response_a / response_b)

**Samar Jaffri** *Tue Jul 02 2024 04:01:26 GMT+0900 (日本標準時)* (0 votes)

Some of the rows in the test/train dataset have 2 or more response(s). Do anyone know if we need to make prediction based on all of the responses i.e., user will chose of of response_a or one of response_b.

Or if there is anything specified about that, that I am missing..?



---

 # Comments from other users

> ## waechter
> 
> The data come from [https://chat.lmsys.org/](https://chat.lmsys.org/) , you can try it to help you understand
> 
> 📜 Rules: You can continue chatting until you identify a winner.
> 
> There are the same number of responses as there are prompts, users vote for their favorite conversation
> 
> 
> 
> > ## Valentin Werner
> > 
> > Exactly this. We are not classifying responses, but conversations. However, if you think that the last response is the one that triggers the user to press "a is better", you are probably right in most cases.
> > 
> > 
> > 
> > > ## Yichuan Gao
> > > 
> > > Haven't thought about this! Wonder how much will only using the last response affects the prediction😂
> > > 
> > > 
> > > 


---

