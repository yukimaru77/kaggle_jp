# how to save qlora_trained model weight with pytorch

**YEI0907** *Sat Jul 13 2024 14:23:51 GMT+0900 (日本標準時)* (0 votes)

because of some problems,I can`t use qlora to train my model  with transformers.Trainer,so,I trained my qlora model with my own pytorch training script and save my weights with torch.save directly,but when i use my weights to inference,i found that when i run my notebook ,my predictions is different in each turns .so,i think my model saving method might be wrong,so, how can i save my trained weights after qlora training with pytorch training script? can i use torch.save directly? or is there any other problems during my inference?Thanks very much for answering my question



---

 # Comments from other users

> ## Valentin Werner
> 
> If you load the model with the peft library, you simply also use model.save_pretrained. This will only save the adapter and not the full model. So we are talking < 100 MB instead of multiple GB.
> 
> Code snippet as example:
> 
> ```
> if test_loss < best_val and epoch != 0:
>     model.save_pretrained(
>         f"my_newest_model_{epoch+1}_{step}"
>     )
> 
> ```
> 
> You will later load it by first loading the model itself (e.g., LlamaForSequenceClassification), getting the PEFT model and then loading the QLoRA weights
> 
> ```
> # Get peft
> model_0 = get_peft_model(base_model_0, peft_config).to(device_0) 
> # Load weights
> model_0.load_state_dict(torch.load(CFG.LORA_PATH), strict=False)
> model_0.eval()
> 
> ```
> 
> 
> 
> > ## YEI0907Topic Author
> > 
> > thanks!,I use torch.save directly to save my model,code just like this
> > 
> > ```
> > if score < best_score:
> >             best_score = score
> >             if int(os.environ["RANK"]) == 0:
> >                 torch.save({
> >                     'epoch': epoch,
> >                     'model_state_dict': dict([(k, v) for k, v in model.module.named_parameters() if v.requires_grad]),
> >                     'optimizer_state_dict': optimizer.state_dict(),
> >                     'scheduler_state_dict': scheduler.state_dict()
> >                 }, model_path)
> > 
> > ```
> > 
> > and my model loading method is same as yours,
> > 
> > so you mean I should use peft_model.save_pretrained() insteat of torch.save?
> > 
> > addtionaly,i test my weights in kaggle by using train_data and my loss is 1.8xxxx,but in my traing, the eval_sets loss is 0.9XX and train_sets loss is also 0.9xx
> > 
> > by the way,i learned a lot from your notebooks, thank you for sharing your notebook!
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > Happy to be of help :)
> > > 
> > > I highly recommend saving adapters separately and loading them separately. I do not see any value in saving full models as long as you are not adding any layers to the model. If you create a custom model with additional layers, you will need to save these weights to, in that case it might make sense to save full models.
> > > 
> > > However, if you load Llama3 like this:
> > > 
> > > ```
> > > base_model = LlamaForSequenceClassification.from_pretrained(model_id, token=HF_TOKEN, num_labels=CFG.NUM_LABELS, torch_dtype=CFG.TORCH_DTYPE, trust_remote_code=True)   
> > > 
> > > ```
> > > 
> > > The sequence classification head is always initialized in the same way, just random values. Things that can help achieve the same result is setting the seed, so the weights are randomly initialized exactly as they were initialized during training.
> > > 
> > > ```
> > > def set_seeds(seed):
> > >     """Set seeds for reproducibility """
> > >     os.environ['PYTHONHASHSEED'] = str(seed)
> > >     random.seed(seed)
> > >     np.random.seed(seed)
> > >     torch.manual_seed(seed)
> > >     if torch.cuda.is_available():
> > >         torch.cuda.manual_seed(seed)
> > >         torch.cuda.manual_seed_all(seed)
> > >     # Set seed for all TPU cores
> > >     xm.set_rng_state(seed, device=xm.xla_device())  
> > > 
> > > ```
> > > 
> > > Doing this helped me to achieve a better LB <-> CV relationship.
> > > 
> > > Further, you may want to save the tokenizer or replicate and deterministic changes you did to it during training (e.g., if you changed pad_token_id or such). Make sure you are exactly tokenizing the same way (also input formats etc.) as you did during training. This can easily switch a lot for your score too.
> > > 
> > > 
> > > 
> > > ## YEI0907Topic Author
> > > 
> > > thanks,this provide a new idea for me to ensure consistency between train and test ;for my model , i had added some my custom modules,and i will re-train the model and save the weight with two part,one for llama3 with peft.save_pretrained(),one for my custom module with torch.save directly.T_T，the previous weight resulted in my LB score reaching 3.x
> > > 
> > > 
> > > 
> > > ## Ilya Turaev
> > > 
> > > All my life I've been thinking that classification heads for decoders were pretrained on some benchmarks or other data. Glad that I've busted this myth and misunderstanding now…
> > > 
> > > 
> > > 


---

