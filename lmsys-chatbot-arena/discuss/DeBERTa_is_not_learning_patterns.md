# DeBERTa is not learning patterns?

**Valentin Werner** *Mon May 06 2024 18:08:22 GMT+0900 (日本標準時)* (6 votes)

Hello everybody - I am currently facing the issue that my starter notebook always predicts label 0 (which is most prevalent in the subset of the dataset that I am using).

I did not have this experience in the past, where even though labels are balanced, the model is not learning.

Did you experience the same and were you able to solve it?



---

 # Comments from other users

> ## Rich Olson
> 
> I had the same experience with deberta:
> 
> [https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/501848](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/501848)
> 
> Short version: Things didn't converge for me until I started training with more data.  
> 
> Definitely had that "huh - this isn't work" feeling training on a small subset.  Got LB 1.030 after training on all the data.
> 
> Notebook here:
> 
> [https://www.kaggle.com/code/richolson/deberta](https://www.kaggle.com/code/richolson/deberta) (copy and paste as you please)
> 
> 
> 
> > ## Valentin WernerTopic Author
> > 
> > Interesting! 1.030 is definetly an improvement, did you also evaluate accuracy? wondering whether it is still in the 30s/40s..
> > 
> > 
> > 
> > > ## Rich Olson
> > > 
> > > Well - my validation on 20% of train is:
> > > 
> > > Log Loss: 1.0217662463425792
> > > 
> > > Accuracy: 0.48329853862212946
> > > 
> > > Considering my LB score is a little lower - I'd guess mid 40s at best.
> > > 
> > > Since the amount of train data seems to be a factor - wondering if tossing a bunch more train at it might help. (there are some datasets…)
> > > 
> > > Considering run-time is about 3 hours - could maybe double the train data.  I haven't really looked at if I can do anything to speed things up yet though.
> > > 
> > > 
> > > 
> > > ## Gaurav Rawat
> > > 
> > > Nice how do the loss curves look they seems to be like fluctuating with no end . Also the accuracy you got at what step earlier or later epochs . As I see that also fluctuates 
> > > 
> > > 
> > > 
> > > ## Rich Olson
> > > 
> > > so - in another notebook that uses deberta - I've gone up to 1000 LGBM iterators - and it still seems like loss is slowly falling… (and LB score improving…)
> > > 
> > > [https://www.kaggle.com/code/richolson/deberta-tf-idf-word2vec-length](https://www.kaggle.com/code/richolson/deberta-tf-idf-word2vec-length) (LB 1.011 on last run)
> > > 
> > > I've added tf-idf, word2vec and length features in that one - so hard to say what's going on…  taking it as a suggestion I may need to use something more than LGBM to fully use the deberta embeddings…
> > > 
> > > 
> > > 


---

> ## Huang Jing Stark
> 
> Facing same issue here, my eval_loss is not decreasing 
> 
> 
> 


---

> ## Valentin WernerTopic Author
> 
> Code in case you care
> 
> Config:
> 
> ```
> class CFG:
>     model = "microsoft/deberta-v3-small"
>     add_tokens = ["<[PROMPT]>","<[RESP_A]>","<[RESP_B]>","<[...]>","\n"]
>     output_dir="."
>     learning_rate=2e-5
>     per_device_train_batch_size=2
>     per_device_eval_batch_size=2
>     num_train_epochs=2
>     weight_decay=0.01
>     evaluation_strategy="epoch"
>     save_strategy="epoch"
>     max_length=2048
>     warmup_ratio=0.1
>     fp16=True
> 
> ```
> 
> Tokenizer (note that I also tried without new tokens and got same result)
> 
> ```
> # Prepare Tokenizer
> tokenizer = AutoTokenizer.from_pretrained(CFG.model)
> 
> new_tokens = set(CFG.add_tokens) - set(tokenizer.vocab.keys())
> tokenizer.add_tokens(list(new_tokens))
> 
> def tokenize(examples):
>     """use with huggingface datasets"""
>     return tokenizer(
>         examples["train_input"], 
>         truncation=True,
>         max_length=CFG.max_length
>     )
> 
> data_collator = DataCollatorWithPadding(tokenizer=tokenizer)
> 
> [... dataset preparation ...]
> 
> ```
> 
> Model loading (note that I also tried without num_labels and got same result):
> 
> ```
> # Initialize model
> model = AutoModelForSequenceClassification.from_pretrained(
>     CFG.model,
>     num_labels=3
> )
> model.resize_token_embeddings(len(tokenizer))
> 
> ```
> 
> Metric used:
> 
> ```
> accuracy = evaluate.load("accuracy")
> 
> def compute_metrics(eval_pred):
>     predictions, labels = eval_pred
>     predictions = np.argmax(predictions, axis=1)
>     return accuracy.compute(predictions=predictions, references=labels)
> 
> ```
> 
> Training:
> 
> ```
> training_args = TrainingArguments(
>     output_dir=CFG.output_dir,
>     learning_rate=CFG.learning_rate,
>     per_device_train_batch_size=CFG.per_device_train_batch_size,
>     per_device_eval_batch_size=CFG.per_device_eval_batch_size,
>     num_train_epochs=CFG.num_train_epochs,
>     weight_decay=CFG.weight_decay,
>     evaluation_strategy=CFG.evaluation_strategy,
>     save_strategy=CFG.save_strategy,
>     fp16=CFG.fp16
> )
> 
> trainer = Trainer(
>     model=model,
>     args=training_args,
>     train_dataset=ds["train"],
>     eval_dataset=ds["test"],
>     tokenizer=tokenizer,
>     data_collator=data_collator,
>     compute_metrics=compute_metrics,
> )
> 
> trainer.train()
> 
> ```
> 
> 
> 
> > ## Ho Dinh Trieu
> > 
> > hi [@valentinwerner](https://www.kaggle.com/valentinwerner),does the train takes long? 
> > 
> > 
> > 
> > > ## Valentin WernerTopic Author
> > > 
> > > No, I sample 10% of the training data and only train 2 epochs. Takes about 35 min on kaggle GPU.
> > > 
> > > I also noticed that other notebooks have the same issue.
> > > 
> > > 
> > > 
> > > ## Gaurav Rawat
> > > 
> > > What was the best loss you got from the baseline not getting it past 1 right now and seems not converging at this moment for me . 😀 
> > > 
> > > 
> > > 
> > > ## Valentin WernerTopic Author
> > > 
> > > Same for me, I also tried rephrasing the task but cannot make it lear at all.
> > > 
> > > Loss is stuck at 1.07 or so; which is what you get when you just predict the distribution
> > > 
> > > 
> > > 


---

