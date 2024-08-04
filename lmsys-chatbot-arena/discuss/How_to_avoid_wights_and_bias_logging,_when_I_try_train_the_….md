# How to avoid wights and bias logging, when I try train the model, it was asking wights and bias token id

**suri@7** *Wed Jul 10 2024 18:24:36 GMT+0900 (日本標準時)* (0 votes)

when I try train the model, it was asking wights and bias token id. I don't want to wights and bias to my model.

```
training_args = TrainingArguments(
  output_dir="./kaggle/input/lmsys-chatbot-arena/bert_model",
  learning_rate=2e-5,
  per_device_train_batch_size=3,
  per_device_eval_batch_size=3,
  num_train_epochs=2,
  weight_decay=0.01,
  evaluation_strategy="epoch",
  save_strategy="epoch",
  load_best_model_at_end=True,
)
trainer = Trainer(
  model=model,
  args=training_args,
  train_dataset=train_dataset,
  eval_dataset=test_dataset,
  tokenizer=tokenizer,
  data_collator=data_collator,
  #compute_metrics=compute_metrics,
)
trainer.train()

```



---

 # Comments from other users

> ## waechter
> 
> Set report_to='none' in TrainingArguments if you don't want to use remote logging
> 
> report_to (str or List[str], optional, defaults to "all") — The list of integrations to report the results and logs to. Supported platforms are "azure_ml", "clearml", "codecarbon", "comet_ml", "dagshub", "dvclive", "flyte", "mlflow", "neptune", "tensorboard", and "wandb". Use "all" to report to all integrations installed, "none" for no integrations. 
> 
>   From [https://huggingface.co/docs/transformers/en/main_classes/trainer](https://huggingface.co/docs/transformers/en/main_classes/trainer)
> 
> 
> 
> > ## suri@7Topic Author
> > 
> > Thanks for your help [@waechter](https://www.kaggle.com/waechter) ,, I would like to know after training my model how, can I can submit the prediction offline, When saving the model Kaggle input path, It does not load when submitted to p predictions.
> > 
> > 
> > 
> > > ## waechter
> > > 
> > > output_dir="./kaggle/input/lmsys-chatbot-arena/bert_model",
> > > 
> > > I think this is wrong because you trying to write to the kaggle/input directory (which is read only)
> > > 
> > > You should save the pretrained model to kaggle/working dir : output_dir="kaggle/working/bert_model"
> > > 
> > > 
> > > 
> > > ## suri@7Topic Author
> > > 
> > > ok, Thanks
> > > 
> > > 
> > > 


---

