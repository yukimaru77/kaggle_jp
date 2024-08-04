# Comments 

> ## Yichuan Gao
> 
> I'm having a hard time reproduce the results from this notebook. Specifically, I've simply downloaded this notebook, and changed only input path, removed the sample(100) and nothing else.
> 
> After training on a 4090, train_loss can only lower to ~1.0 and eval_loss is also ~0.98, which is much worse than claimed 0.937 CV loss. I have tried run training on different machines with different GPU configuration and different batch_size, all give similar bad results. 
> 
> So I'm really puzzled, what could be the possible reasons here? Any suggestions are welcomed.
> 
> 
> 
> > ## skurita
> > 
> > I am experiencing the same issue. 
> > 
> > I also downloaded the notebook, changed only the input path, and removed sample(100). 
> > 
> > However, my train/eval loss only decreases as shown in the graph, which is much worse than the claimed 0.937 CV loss. 
> > 
> > I trained "unsloth/gemma-2-9b-it-bnb-4bit" over 4 epochs, and the validation was calculated after each epoch. 
> > 
> > Does anyone know how to reproduce the results from this train notebook? 
> > 
> > Any insights or suggestions would be greatly appreciated.
> > 
> > I will also mention the author. [@emiz6413](https://www.kaggle.com/emiz6413) 
> > 
> > Thank you.
> > 
> > 
> > 


---

> ## S J Moudry
> 
> [@emiz6413](https://www.kaggle.com/emiz6413)  thank you so much for sharing your training and inference notebooks, I've learned immensely from them and upvoted all your work.  I have a few questions:
> 
> What was the accuracy of your model on evaluation after the epoch of training?
> What platform do you use for training? Do you have any recommendations?
> Do you have any tips for hyperparameter tuning, or how you arrive at your hyperparameters?  Did you train on the full dataset multiple times or do a few test runs to gauge effectiveness?
> 
> 
> > ## Eisuke MizutaniTopic Author
> > 
> > Thanks for the comment. 
> > 
> > - log loss on eval set after one epoch was 0.9371.
> > 
> > - I'm using paperspace. I can recommend that platform if you wanna do many experiments with a reasonable fixed price.
> > 
> > - I haven't spent much time on hyperparameter tuning as it takes very long time to train gemma2. I did a few runs and watched the learning curve and manually aborted the unpromising ones. So, I guess there're plenty of room to tune the hyperparameters.
> > 
> > 
> > 


---

> ## Lorry Zou
> 
> Why didn't you reuse the Llama3 training notebook you publicized before? You can still train on TPU for ~6 hours by just changing the model name/path from llama3 to gemma2. 
> 
> 
> 
> > ## Eisuke MizutaniTopic Author
> > 
> > I suppose you are talking about kishanvavdara's notebook (I have't publish a a training notebook).
> > 
> > I trained my model on GPU and was not sure how to reproduce it on TPU. Especially quantization is not supported on TPU, although quantization is not necessary if no OOM occurs.
> > 
> > Are you able to train gemma2 on TPU?
> > 
> > 
> > 
> > > ## Lorry Zou
> > > 
> > > Yes, I was talking about Kishanvavdara's notebook. He posted two Gemma 2 notebooks earlier [https://www.kaggle.com/code/kishanvavdara/gemma-2-9b-part-1](url)
> > > 
> > > with "gemma-2-9b-hf" as an uploaded dataset. I was able to train it on TPU and it was fast.
> > > 
> > > 
> > > 
> > > ## Eisuke MizutaniTopic Author
> > > 
> > > Did you just train a catboost (or whatever) classifier on top of the frozen gemma's last hidden state?
> > > 
> > > What happened to me was loading gemma2-9b resulted in OOM and quantization is not supported for TPU. So I had no choice but to give up using TPU for finetuning gemma's weight.
> > > 
> > > 
> > > 


---

> ## Muhammad Haroon ul Hasnain
> 
> Nice Notebook with explanation.
> 
> 
> 


---

> ## Mohamadreza Momeni
> 
> Excellent work.
> 
> Great job dear [@emiz6413](https://www.kaggle.com/emiz6413) 
> 
> 
> 


---

> ## floriandev
> 
> First of all [@emiz6413](https://www.kaggle.com/emiz6413) huge thanks for these notebook!!!
> 
> Unfortunately I got the following error after finetuning -> pushing resulting MODEL to hugging face -> invoking your inference notebook with the MODEL from hf:
> 
> … leads to this error…
> 
> 
> 
> > ## Lorry Zou
> > 
> > I think if you do not specify num_classes=3, its default value=2.
> > 
> > 
> > 
> > > ## floriandev
> > > 
> > > Hi Lorry, thx for your quick reply!!!
> > > 
> > > The training / inference notebooks are from the same author and I used his model for the training on the unaltered notebook, it gave back acc and loss etc. just fine, but after saving, loading into inference notebook it gives this error?
> > > 
> > > I suppose the trained model should match the inference model architecture wise…hmmm
> > > 
> > > Btw. how would I introduce the number of classes in the inference notebook, as it seems there is one additional parameter in the newly trained model?
> > > 
> > > Let me know, appreciate your support,
> > > 
> > > Florian.   
> > > 
> > > 
> > > 
> > > ## floriandev
> > > 
> > > ohh, just found (and currently trying) to use the locally generated checkpoint…will report in a bit!
> > > 
> > > 
> > > 
> > > ## floriandev
> > > 
> > > ok, could be solved by the thread [https://www.kaggle.com/code/emiz6413/training-gemma-2-9b-4-bit-qlora-fine-tuning/comments#2928021](https://www.kaggle.com/code/emiz6413/training-gemma-2-9b-4-bit-qlora-fine-tuning/comments#2928021) answered by [@raconion](https://www.kaggle.com/raconion). All good now ;-)
> > > 
> > > Real issue: Training output was used for the gemma_dir.
> > > 
> > > Solution: Used training output for the lora_dir. 
> > > 
> > > 
> > > 


---

> ## Nikhil Tumbde
> 
> Hi thanks for the notebooks.
> 
> I had a question about the fp16 training argument, what would happen if I use bf16 instead of fp16 for finetuning? I noticed with llama 3 8b (base model) when I used 4 bit quantization with fp16 the gradients became NaNs after few thousand steps. Any thoughts?
> 
> 
> 
> > ## Eisuke MizutaniTopic Author
> > 
> > I guess bf16 is generally safer option if it's available on your device.
> > 
> > 
> > 


---

> ## Vavilkin Alexander
> 
> Hello [@emiz6413](https://www.kaggle.com/emiz6413)! Thank you so much for your notebook, it is very usefull for practice in fine-tuning llm. Could you tell me please how you saved the entire model? As far as I understand during fine-tuning with "Trainer" only the weights of the adapter are saved, but the weights of classification head are not. Also the model in inference notebook is not an ordinary quantized model, but already with a head for classification. I will be very glad to receive a comment from you about it
> 
> 
> 
> > ## Eisuke MizutaniTopic Author
> > 
> > The classification head is wrapped as ModulesToSaveWrapper, so it is automatically saved by Trainer.
> > 
> > When loading from the checkpoint, the trained weight is loaded to the classification head.
> > 
> > 
> > 
> > > ## Vavilkin Alexander
> > > 
> > > I got it thanks!
> > > 
> > > 
> > > 


---

> ## Mattia Vanzetto
> 
> Sorry about the question, I am a newbie to this, but once the notebook is done and you got the output, which are the steps to save the output and reloaded it in the inference notebook?  Thanks!
> 
> 
> 
> > ## raconion
> > 
> > There should be an output folder in the same level of your notebook. Use the subfolder with the largest number (steps) for inference. In this case it should be 5748
> > 
> > 
> > 


---

> ## raconion
> 
> Hi! Thank you for this wonderful notebook. I ran this notebook in H100*2 and it turns out that there are 11495 steps instead of 5748 in your result. Also the cv score is slightly worse: 0.964697.
> 
> After reading some comments, I felt like it is also the issue with batch size.
> 
> My settings are
> 
> ```
> class Config:
>     output_dir: str = "output"
>     checkpoint: str = "unsloth/gemma-2-9b-it-bnb-4bit"  # 4-bit quantized gemma-2-9b-instruct
>     max_length: int = 1024
>     n_splits: int = 5
>     fold_idx: int = 0
>     optim_type: str = "adamw_8bit"
>     per_device_train_batch_size: int = 2
>     gradient_accumulation_steps: int = 2  # global batch size is 8 The effective batch size is per_device_train_batch_size * gradient_accumulation_steps * num_devices.
>     per_device_eval_batch_size: int = 8
>     n_epochs: int = 1
>     freeze_layers: int = 16  # there're 42 layers in total, we don't add adapters to the first 16 layers
>     lr: float = 2e-4
>     warmup_steps: int = 20
>     lora_r: int = 16
>     lora_alpha: float = lora_r * 2
>     lora_dropout: float = 0.05
>     lora_bias: str = "none"
> 
> ```
> 
> And
> 
> ```
> training_args = TrainingArguments(
>     output_dir="output",
>     overwrite_output_dir=True,
>     report_to="none",
>     num_train_epochs=config.n_epochs,
>     per_device_train_batch_size=config.per_device_train_batch_size,
>     gradient_accumulation_steps=config.gradient_accumulation_steps,
>     per_device_eval_batch_size=config.per_device_eval_batch_size,
>     logging_steps=10,
>     eval_strategy="epoch",
>     save_strategy="steps",
>     save_steps=200,
>     optim=config.optim_type,
>     fp16=True,
>     learning_rate=config.lr,
>     warmup_steps=config.warmup_steps,
> )
> 
> ```
> 
> I would like to know if you actually use different settings when you actually train the model. Thanks!
> 
> 
> 
> > ## Eisuke MizutaniTopic Author
> > 
> > Are both GPUs visible in your code? 
> > 
> > 
> > 
> > > ## raconion
> > > 
> > > I directly reused your notebook code. According to device map, it seems like model parallelization is used. nvidia-smi shows that both GPUs are used as well.
> > > 
> > > Device map:
> > > 
> > > ```
> > > {'model.embed_tokens': 0, 'model.layers.0': 0, 'model.layers.1': 0, 'model.layers.2': 0, 'model.layers.3': 0, 'model.layers.4': 0, 'model.layers.5': 0, 'model.layers.6': 0, 'model.layers.7': 0, 'model.layers.8': 0, 'model.layers.9': 0, 'model.layers.10': 0, 'model.layers.11': 0, 'model.layers.12': 0, 'model.layers.13': 0, 'model.layers.14': 0, 'model.layers.15': 0, 'model.layers.16': 1, 'model.layers.17': 1, 'model.layers.18': 1, 'model.layers.19': 1, 'model.layers.20': 1, 'model.layers.21': 1, 'model.layers.22': 1, 'model.layers.23': 1, 'model.layers.24': 1, 'model.layers.25': 1, 'model.layers.26': 1, 'model.layers.27': 1, 'model.layers.28': 1, 'model.layers.29': 1, 'model.layers.30': 1, 'model.layers.31': 1, 'model.layers.32': 1, 'model.layers.33': 1, 'model.layers.34': 1, 'model.layers.35': 1, 'model.layers.36': 1, 'model.layers.37': 1, 'model.layers.38': 1, 'model.layers.39': 1, 'model.layers.40': 1, 'model.layers.41': 1, 'model.norm': 1, 'score': 1}
> > > 
> > > ```
> > > 
> > > I think in this case if we use 
> > > 
> > > per_device_train_batch_size: int = 2
> > >     gradient_accumulation_steps: int = 2
> > > 
> > > the global batch size will be 4. When you are doing training, do you set per_device_train_batch_size and gradient_accumulation_steps differently to ensure global batch size of 8?
> > > 
> > > 
> > > 
> > > ## Eisuke MizutaniTopic Author
> > > 
> > > [@raconion](https://www.kaggle.com/raconion) 
> > > 
> > > Sorry for the delayed response.
> > > 
> > > I set per_device_train_batch_size and gradient_accumulation_steps in a way global batch size becomes 8. Global batch size 4 resulted in worse score.
> > > 
> > > 
> > > 


---

> ## HZM
> 
> HI Eisuke, have you tried other llm like Llama3, which did not work for me 
> 
> 
> 
> > ## Eisuke MizutaniTopic Author
> > 
> > I've tried Llama3 and got somewhere around 0.98
> > 
> > 
> > 


---

> ## Kim Kumuha
> 
> How long did the training take?
> 
> 
> 


---

> ## yuanzhe zhou
> 
> hello, may I ask what is your result after 1 epoch running of this notebook?
> 
> 
> 
> > ## Eisuke MizutaniTopic Author
> > 
> > Log loss on the eval set (id % 5 == 0) is 0.9371.
> > 
> > You can reproduce the result using the checkpoint [here](https://www.kaggle.com/datasets/emiz6413/73zap2gx/data).
> > 
> > 
> > 


---

