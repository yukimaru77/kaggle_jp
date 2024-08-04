# Is it possible to use gemma-2-27B with vLLM?

**yechenzhi1** *Tue Jul 23 2024 00:34:19 GMT+0900 (日本標準時)* (1 votes)

Inspired by [@cdeotte](https://www.kaggle.com/cdeotte)'s great [work](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/521294), I'm trying to use gemma-2-27B with vLLM. First I use GPTQmodel to quantinize it to 4-bit, then use vLLM-0.5.2 to do the infer. But we have to use flashinfer as the backend because of gemma-2's logits capping, then the problem comes, it's said flashinfer only supports GPU with compute [capability >= 8.0](https://github.com/vllm-project/vllm/issues/6173#issuecomment-2214759644), and T4 is 7.5. So is gemma-2-27b impossible for this competition?



---

 # Comments from other users

> ## Yixiao Yuan
> 
> I think we can't run gemma-2 with vLLM, but we can run it by huggingface. vLLM is much better for generation task due to PagedAttention. However, if we only generate one token or use classification head (we don't need KV cache in such cases), the performance should be similar.
> 
> 
> 
> > ## yechenzhi1Topic Author
> > 
> > bad news here, it seems only vllm/sglang can infer [quantized gemma-2-27b](https://github.com/ModelCloud/GPTQModel/issues/140#issuecomment-2242221690) correctly right now. 
> > 
> > 
> > 
> > ## yechenzhi1Topic Author
> > 
> > But thanks! I'll try it anyway!
> > 
> > 
> > 
> > > ## beanpotato
> > > 
> > > Could you share if you can run gema-2-27b with vLLM?🥰
> > > 
> > > 
> > > 
> > > ## yechenzhi1Topic Author
> > > 
> > > No, T4 GPU doesn't support FlashInfer. I stopped trying gemma-2-27B after a few days.
> > > 
> > > 
> > > 


---

> ## ShelterW
> 
> Is it possible to use gemma-2-27B with vLLM now?
> 
> 
> 
> > ## Somesh88
> > 
> > I've been trying to use gemma 2 with vllm the weights over kaggle doesn't contain config file. If I try to load it form transformers then I have to keep internet access enabled which is not allowed in submission. have you found any workround for this? 
> > 
> > 
> > 
> > > ## Kishan Vavdara
> > > 
> > > you can create kaggle dataset of configs, packages, weights, etc. and add to your inference notebook, then you can use it without enabling internet. 
> > > 
> > > 
> > > 


---

