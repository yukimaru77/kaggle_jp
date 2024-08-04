# Comments 

> ## Lorry Zou
> 
> Anyone managed to get LB score <0.92 with Gemma2 by tuning hyperparams? The best score I can get is 0.926.
> 
> 
> 
> > ## Pranshu BahadurTopic Author
> > 
> > Wait you were able to do inference?
> > 
> > 
> > 
> > > ## Lorry Zou
> > > 
> > > I used Pytorch, not TF
> > > 
> > > 
> > > 
> > ## cm391
> > 
> > if you pre-process the data easy 0.89 val, with aug I'm getting 0.87… Why do Keras make such nice training code and no distributed inference code??
> > 
> > 
> > 
> > > ## Pranshu BahadurTopic Author
> > > 
> > > I wish I knew haha, there is a way to figure it out by quantization but I've been a bit busy
> > > 
> > > 
> > > 


---

> ## ano
> 
> Thank you for your great work! I'm not encouraging you to implement further, but maybe we can also save optimizer to resume training?
> 
> 
> 
> > ## Pranshu BahadurTopic Author
> > 
> > I don't think you need a optimizer state since I didn't use any schedulers. Same optimizer config can work for further finetuning
> > 
> > 
> > 
> > > ## ano
> > > 
> > > My bad. You're right. No need to save for this optimizer. 
> > > 
> > > 
> > > 


---

> ## lightsource<3
> 
> If you need to save only LoRA weights, then you can use the following code:
> 
> ```
> model.get_layer("gemma_backbone").save_lora_weights("model.lora.h5")
> 
> ```
> 
> 
> 
> > ## Pranshu BahadurTopic Author
> > 
> > Thanks - I'll try this out -
> > 
> > 
> > 
> > ## Pranshu BahadurTopic Author
> > 
> > Hey can you link the docs for this?
> > 
> > 
> > 
> > > ## lightsource<3
> > > 
> > > [https://keras.io/api/keras_nlp/base_classes/backbone/](https://keras.io/api/keras_nlp/base_classes/backbone/)
> > > 
> > > until I managed to properly save and quantize the trained model for inference on the GPU, it turned out to be not so easy :(
> > > 
> > > 
> > > 


---

> ## Dai LinLing
> 
> Thank you for sharing. That's a good note!
> 
> 
> 


---

> ## kaggk
> 
> Good Work!
> 
> 
> 


---

> ## RobsonDSP
> 
> Could someone share some info about the performance of the model? What is the log_loss after 1 or more epochs? 
> 
> 
> 
> > ## Pranshu BahadurTopic Author
> > 
> > Training loss: ~1.08; Val loss: 0.9286
> > 
> > 
> > 


---

> ## Turbo
> 
> Nice work!
> 
> How to inference?
> 
> 
> 
> > ## Pranshu BahadurTopic Author
> > 
> > [https://www.kaggle.com/code/pranshubahadur/inference-tf-gemma-2-9b-lmsys?scriptVersionId=189454678](https://www.kaggle.com/code/pranshubahadur/inference-tf-gemma-2-9b-lmsys?scriptVersionId=189454678)
> > 
> > just save lora weights in training and load them here!
> > 
> > 
> > 


---

> ## Sparsh Tewatia
> 
> How much training , validation loss , after whole epoch ? 
> 
> 
> 
> > ## Pranshu BahadurTopic Author
> > 
> > You can check this out in version 13 
> > 
> > 
> > 


---

