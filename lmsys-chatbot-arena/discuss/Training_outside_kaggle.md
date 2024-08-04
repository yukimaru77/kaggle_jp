# Training outside kaggle

**Ahmad Al-Husainy** *Sun Jun 16 2024 04:30:02 GMT+0900 (日本標準時)* (3 votes)

Hello, this is my first competition, and I'm curious to know if it's possible to train large pre-trained models in an external environment and then simply upload the weights for submission. 



---

 # Comments from other users

> ## Lorry Zou
> 
> You definitely can do that. It's also what I'm doing. However, since this competition requires internet-off submission, I'm sure I will run into some issues…
> 
> 
> 
> > ## Valentin Werner
> > 
> > Just load it as a kaggle dataset or kaggle model!
> > 
> > You only have to make sure the models you are using are open source. 
> > 
> > 
> > 
> > > ## Ivel afred
> > > 
> > > Does this mean that your model needs to be public on Kaggle? Or it's okay to just make it public on Hugging Face.
> > > 
> > > 
> > > 
> > > ## Valentin Werner
> > > 
> > > It can be private on kaggle, just available for you. You dont have to make it public on huggingface either. Its just important that the model that you finetune is also available for others. (e.g., DeBERTa or Llama are open source; GPT-4 is not - if you finetune GPT-4 for the competition, that would be not fair and you would have to make your GPT-4 tuned model available for everybody in the competition instead (I think))
> > > 
> > > 
> > > 
> > > ## Ivel afred
> > > 
> > > thanks, that helps me a lot
> > > 
> > > 
> > > 
> > ## Ahmad Al-HusainyTopic Author
> > 
> > Thank you for your comment. I want to clarify my approach: I'm currently using Google Colab for model development. When I attempt to train the models on Kaggle, I encounter GPU memory issues and other problems related to the Kaggle environment it self, even though the same code runs smoothly on Colab. I'm considering training the model in Colab and then extracting the best model weights. My plan is to rebuild the model on Kaggle, load the weights, predict on the test dataset, and submit my results. Additionally, the environment on Colab is more extensive than on Kaggle, so training on Kaggle could potentially exceed the 9-hour limit.
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > That is the correct approach
> > > 
> > > 
> > > 


---

> ## Marília Prata
> 
> I think it depends on each competition rules. Though I'm not certain. Maybe Paul Mooney, Sohier Dane or Addison Howard could answer that.
> 
> By the way, welcome to your 1st competition.
> 
> 
> 


---

