# Finetuned --> Quantized vs Quantized--> Finetuned

**Varun Jagannath** *Fri Jul 26 2024 23:22:44 GMT+0900 (日本標準時)* (1 votes)

Which approach is performing better in this competition: fine-tuning a model like Llama 3 and then quantizing it, or taking a low-bit quantized model and fine-tuning it on the dataset ?



---

 # Comments from other users

> ## Valentin Werner
> 
> I hope somebody who tested it actually answers and knows better than me. My intuition is that Finetune -> Quantize should be better, as the finetuning is more precise. Obviously there is also the argument that this precision is quantized later anyways and maybe training in a quantized way makes sure your val / lb is more consistent
> 
> 
> 
> > ## Pranshu Bahadur
> > 
> > Ok so I kind of tested this scenario a bit and I agree with your hypothesis, when I trained gemma 2 9b on bfloat16 training loss went down to 0.44 (definitely a sign of overfitting). I think quantization should be done post-training.
> > 
> > 
> > 
> > ## Maksim Metelskii
> > 
> > LoRa adapters (which are 16 or 32 bit) trained on quantized model may help to fix inaccuracy stemmed from quantization. Like they address both quantization and new specific task inaccuracy. ChatGPT says Quantized--> Finetuned may be more beneficial for accuracy. But really need to be tested though
> > 
> > 
> > 
> > ## Varun JagannathTopic Author
> > 
> > My observation is that earlier TPU train notebook which was published got nearly around 0.98 LB and the latest 0.94LB of Training and Inference with unsloth gemma 2. So really wanted to understand if the quantized followed fine tuning is performing well in this competition. 
> > 
> > 
> > 


---

> ## xiaotingting
> 
> I think fine-tuning after quantization is better because it can make up for the loss caused by quantization. Maybe fine-tuning the quantized model and quantizing after training require different learning rates.
> 
> 
> 


---

