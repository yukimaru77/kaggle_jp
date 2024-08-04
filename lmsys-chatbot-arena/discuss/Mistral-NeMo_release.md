# Mistral-NeMo release

**Ashwani** *Fri Jul 19 2024 01:09:26 GMT+0900 (日本標準時)* (22 votes)

Mistral-NeMo 12B released 

- Outperforms Gemma2 9B and Llama3 8B

- 128K context window

- Multilingual in 100+ languages: excels in European, Asian & Indian languages

- Quantization-Aware Training at FP8

- Apache 2.0 license

Blog: [https://mistral.ai/news/mistral-nemo/](https://mistral.ai/news/mistral-nemo/)

HF Weights (Base): [https://huggingface.co/mistralai/Mistral-Nemo-Base-2407](https://huggingface.co/mistralai/Mistral-Nemo-Base-2407)

HF Weights (Instruct): [https://huggingface.co/mistralai/Mistral-Nemo-Instruct-2407](https://huggingface.co/mistralai/Mistral-Nemo-Instruct-2407)



---

 # Comments from other users

> ## James Day
> 
> FYI, it appears finetuning for Mistral-NeMo is currently broken in the transformers library (see [https://huggingface.co/mistralai/Mistral-Nemo-Instruct-2407/discussions/6](https://huggingface.co/mistralai/Mistral-Nemo-Instruct-2407/discussions/6)). A fix should be released soon ([https://github.com/huggingface/transformers/pull/32065](https://github.com/huggingface/transformers/pull/32065)).
> 
> As usual, I'm inclined to wait at least a couple days for bugs to be discovered and fixed before attempting to use any new model 😉.
> 
> 
> 


---

> ## Lorry Zou
> 
> I just fune-tuned the instruct model yesterday, seems like it's not even on par with Gemma2 9b…Weird
> 
> 
> 
> > ## Valentin Werner
> > 
> > Might be the bugs James mentioned. These bugs are not always not always black and white, as in they raise Exceptions. Could also be that a different attention mechanism is used, which the model was not trained on or such (not sure if that is actually a thing and if it would cause an Exception, but you probably get the gist)
> > 
> > 
> > 
> > ## Eisuke Mizutani
> > 
> > I installed the latest transformers from source and could run training without error.
> > 
> > But as Lorry Zou mentioned, the result was not so good (even worse than llama3 in my case).
> > 
> > 
> > 


---

> ## EISLab_hwlee
> 
> It's very difficult to implement the code…
> 
> 
> 


---

> ## Valentin Werner
> 
> Release Season going hard in the last 5 weeks of the competition 🚀
> 
> 
> 
> > ## Psi
> > 
> > Thankfully, only three weeks left :)
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > It's quite funny with the GenAI Hype. You may have a breakthrough in the NLP competitions not by modelling techniques, but by sheer coincidence, having companies like H2O, Google or Mistral (& NVIDIA) release some high quality models. Not so long ago, we used to train Mistral-7B for peak performance - now it seems like a 3rd choice model.
> > > 
> > > 
> > > 


---

> ## gentle bird
> 
> new model. who is trying this?
> 
> 
> 


---

