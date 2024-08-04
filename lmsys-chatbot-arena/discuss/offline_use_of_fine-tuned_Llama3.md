# offline use of fine-tuned Llama3

**nahyat** *Thu Jun 20 2024 16:00:07 GMT+0900 (日本標準時)* (1 votes)

Inspired by Kishan Vavdara's wonderful notebook, I fine-tuned the Llama3-8b model in colab. I got the basemodel from huggingface's Llama3-8b model instead of the kaggle dataset.（MODEL_NAME = 'meta-llama/Meta-Llama-3-8B'）

When I tried to use the fine-tuned model in kaggle, I was faced with a situation where I could not load the weights of the model I created because huggingface could not be authenticated in the offline environment.

After loading the basemodel from the kaggle dataset, I also failed to load the weights of my model.

Is it because the models in huggingface and kaggle dataset are not compatible, which is why the loading fails?

Note: Llama3 license applications for the kaggle dataset are also allowed.

Thank you for watching



---

 # Comments from other users

> ## Kishan Vavdara
> 
> I'm glad you found my notebook helpful. Can you share the error you're facing ? and did you use LoRA for fine-tuning?
> 
> 
> 
> > ## nahyatTopic Author
> > 
> > Thank you for watching!
> > 
> > I wasn't getting any errors, but I was worried that the processing was too fast (compared to your model) when loading the weights of the fine-tuned model into the basemodel. ↓
> > 
> > model_0.load_state_dict(torch.load(WEIGHTS_PATH), strict=False)
> > 
> > I noticed that the results of inference were surprisingly low, so I guessed that there was some kind of problem when loading the model parameters.
> > 
> > However, when I reviewed the code in a local environment, I confirmed that there was a discrepancy in the variable names in the training flow, which caused the correct labels required for backward to fail to be obtained. (I don't know why trainer.train() worked without an error.)
> > 
> > I'm sorry for taking the time to watch it…
> > 
> > 
> > 
> > > ## Kishan Vavdara
> > > 
> > > No worries, It's great to hear that you found the discrepancy and resolved the issue. Happy finetuning) 
> > > 
> > > 
> > > 


---

> ## Lorry Zou
> 
> How long did it take to fine-tune on Colab? I'm also trying to fine-tune on Colab but it'll take over 20 hours using A100, which is much longer than the max session length of Colab (12 hours). How did you make it shorter than 12 hours? Thank you so much.
> 
> 
> 


---

