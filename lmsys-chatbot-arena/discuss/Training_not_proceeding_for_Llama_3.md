# Training not proceeding for Llama 3

**JamshaidSohail** *Sun Jul 14 2024 20:29:44 GMT+0900 (日本標準時)* (0 votes)

Hi. I am trying to train the Llama 2 model from the [notebook](https://www.kaggle.com/code/kishanvavdara/lmsys-llama-3-tpu-train/notebook) shared by [@kishanvavdara](https://www.kaggle.com/kishanvavdara). But my training is not proceeding as shown in the figure. Any help would be appreciated.  



---

 # Comments from other users

> ## Valentin Werner
> 
> If you have the tqdm per epoch, I recommend changing it to the inner loop (steps within the epoch) to see if it actually does something:
> 
> ```
> for epoch in range(CFG.NUM_EPOCHS):
>     ste = time()
>     for step in tqdm(range(STEPS_PER_EPOCH)):
>         # Zero Out Gradients
>         OPTIMIZER.zero_grad()
> 
> ```
> 
> Also, the first samples sometimes take multiple minutes (I once had 300 seconds for the first batch) but then it will speed up afterwards. The notebook shared works well technically, so if you havent changed anything, I would just recommend factory reset and try again.
> 
> 
> 
> > ## JamshaidSohailTopic Author
> > 
> > The only changes I need to do is the addition of HF_TOKEN for my own account in the tokenizer as well as in the model loading area as below. 
> > 
> > ```
> > model_id = "meta-llama/Meta-Llama-3-8B-Instruct"
> > tokenizer = AutoTokenizer.from_pretrained(model_id,use_auth_token=HF_TOKEN)
> > 
> > base_model = LlamaForSequenceClassification.from_pretrained(model_id,
> >                                                             use_auth_token=HF_TOKEN,
> >                                                             torch_dtype=torch.bfloat16,
> >                                                             num_labels=3)    
> > 
> > ```
> > 
> > Now i followed your advice and added the tqdm to the STEPS_PER_EPOCH line as well and watching the training goes inside. 
> > 
> > 
> > 
> > > ## JamshaidSohailTopic Author
> > > 
> > > It is working now. Thank you for your comment and help 😀
> > > 
> > > 
> > > 


---

