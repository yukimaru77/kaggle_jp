# How to get the vector representation of sentences using Llama3?

**godmysalary** *Fri Jun 28 2024 17:22:14 GMT+0900 (日本標準時)* (0 votes)

Hi everyone! Now most public noteboks directly use "LlamaForSequenceClassification" for fine-tuning and getting the predicted probability. I was wondering how I can get the learned embeddings of response_a and response_b besides the predictions since I think the embeddings can be fed into other different classifiers. I don't want to employ another LLM due to the time constraint. So could anybody tell me how I can getting the embeddings of responses as a byproduct of the fine-tuned Llama3? Thanks.



---

 # Comments from other users

> ## RB
> 
> You can pass output_hidden_states=True when initializing model , something like this 
> 
> ```
> model  = AutoModelForCausalLM.from_pretrained(model_path, quantization_config=quantization_config, output_hidden_states=True)
> 
> out = model(input_ids = tokenized['input_ids'], attention_mask = tokenized['attention_mask'])
> 
> out.hidden_states
> 
> ```
> 
> 
> 
> > ## godmysalaryTopic Author
> > 
> > thank you!
> > 
> > 
> > 


---

> ## Enter your display name
> 
> I think what you want is the last hidden state of the model's output?
> 
> 
> 
> > ## godmysalaryTopic Author
> > 
> > exactly. So is there one way to obtain this? thanks
> > 
> > 
> > 


---

