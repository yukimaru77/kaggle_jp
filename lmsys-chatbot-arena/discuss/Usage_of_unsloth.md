# Usage of unsloth

**Varun Jagannath** *Mon Jul 08 2024 01:16:33 GMT+0900 (日本標準時)* (0 votes)

Has anyone used unsloth in the competition as it says that training and inferencing is much with it. Looking forward for suggestions.



---

 # Comments from other users

> ## Ivan Vybornov
> 
> They do not have kernels for classifier yet.
> 
> 
> 
> > ## Cristóbal Mackenzie
> > 
> > Exactly, and I think the "axolotl" library which is also being very widely used doesn't support classification models yet.
> > 
> > 
> > 
> > ## Varun JagannathTopic Author
> > 
> > ok, thanks for the input. But do you think it would be too much of a task if we give prompts and then ask model to predict the classes.
> > 
> > 
> > 
> > ## Takamichi Toda
> > 
> > In the CausalLM header can use the probabilities of generation of tokens A, B and tie as predictions.
> > 
> > ```
> > inputs = tokenizer(text)
> > out = model(inputs)
> > pred_token_id = tokenizer.encode("A") + tokenizer.encode("B") + tokenizer.encode("tie")
> > pred = out.logits[0, -1, pred_token_id].softmax(0)
> > 
> > ```
> > 
> > 
> > 
> > > ## Varun JagannathTopic Author
> > > 
> > > Tried this method as well, but it always predicts or weighs towards one class. Even I have checked your notebook. Model A is always having higher weight. I guess the classification head is working well in this competition.
> > > 
> > > 
> > > 
> > > ## Takamichi Toda
> > > 
> > > In my experiment as well, the classification head has been producing better results so far. I am currently in the process of trial and error to see if improvements can be made with fine-tuning (in [this discussion](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/520470#2925128), it seems they were able to achieve 0.902 with the generation head).
> > > 
> > > 
> > > 


---

