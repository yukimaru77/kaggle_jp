# [Solved] trainer.train("checkpoint-1000") ignores the first samples?: Resuming training in Transformers library. 

**ano** *Thu Aug 01 2024 15:27:59 GMT+0900 (日本標準時)* (0 votes)

My question is if trainer.train("checkpoint-x") ignores the first samples?

For example, I first trained using 4000 samples as train_dataset and got checkpoint-200, 400, 600, 800 and the last checkpoint as checkpoint-1000. And then I resumed training using 4800 samples by trainer.train("checkpoint-1000") and I got only checkpoint-1000 and checkpoint-1200 (no directory corresponding to 200-800). Does that mean the first 4000 samples were skipped?

In order to resume training using new training datasets, do we need to add the first samples as "dummy"? 



---

 # Comments from other users

> ## yechenzhi1
> 
> Yes, resuming training involves bypassing the previously processed data. If you wish to modify your dataset, you can specify 'model_name' as 'checkpoint-1000' and subsequently fine-tune it using your 4800 samples.
> 
> However, if you do so, your model will see the 4000 samples twice, is this what you want?
> 
> 
> 
> > ## anoTopic Author
> > 
> > Thank you for clarifying!
> > 
> > In my case, I trained with dataset_a and retrained with dataset_b from the checkpoint, but it seemed like the first samples in dataset_b was ignored. That's why I experimented a bit and asked this question here. Your answer is very helpful. Thank you so much!
> > 
> > 
> > 


---

