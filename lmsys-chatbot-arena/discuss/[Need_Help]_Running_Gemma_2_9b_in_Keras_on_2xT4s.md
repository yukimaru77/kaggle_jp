# [Need Help] Running Gemma 2 9b in Keras on 2xT4s

**Pranshu Bahadur** *Mon Jul 22 2024 12:28:59 GMT+0900 (日本標準時)* (3 votes)

Hey guys!

I made this notebook to train Gemma 2 9b on TPUs.

But the competition doesn't allow TPUs for submission….which is a bit awkward haha

So I'm enlisting your help to figure this out!

Would really appreciate any feedback, I am looking to learn!

Training nb (~3 hrs for 1 epoch):

[https://www.kaggle.com/code/pranshubahadur/tf-gemma-2-9b-lmsys-training-tpu](https://www.kaggle.com/code/pranshubahadur/tf-gemma-2-9b-lmsys-training-tpu)

Unsolved inference nb:

[https://www.kaggle.com/code/pranshubahadur/unsolved-inference-tf-gemma-2-9b-lmsys](https://www.kaggle.com/code/pranshubahadur/unsolved-inference-tf-gemma-2-9b-lmsys)



---

 # Comments from other users

> ## Pranshu BahadurTopic Author
> 
> Update: Inference works now, out of tpu quota will update on saturday
> 
> 
> 
> > ## Somesh88
> > 
> > what did you do to make inference run?
> > 
> > 
> > 
> > > ## Pranshu BahadurTopic Author
> > > 
> > > mainly device allocation followed by a custom prediction loop and set_floatx('float16')
> > > 
> > > no quantization was needed 
> > > 
> > > you can check out my inference nb linked above
> > > 
> > > 
> > > 


---

