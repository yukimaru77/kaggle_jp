# How to work with Gemma Keras 1.1_7b instruct _en WITHOUT Google Cloud? On the 1.1_2b_instruct_en No Memory issue.

**Marília Prata** *Fri May 10 2024 10:43:46 GMT+0900 (日本標準時)* (17 votes)

I'm facing some memory issue with Gemma Keras 1.1 -7b- instruct-en.  It appeared that message "Your notebook tried to allocate more memory than is available. It has restarted".   Go to Google Cloud or dismiss it.

I even ran:

os.environ["XLA_PYTHON_CLIENT_PREALLOCATE"]="false"

  os.environ["XLA_PYTHON_CLIENT_MEM_FRACTION"]=".XX"

  os.environ["XLA_PYTHON_CLIENT_ALLOCATOR"]="platform"

Besides, I reduced the number of rows.

When I ran GemmaCausalLM the message that "The notebook tried to allocate more memory than is available" popped-up.

# Is there a way to work with Gemma Keras 1.1- 7b instruct -en WITHOUT  Google Cloud?

For the record, that doesn't occur on the other 7b models (7 billion parameters) that were pinned on this LMSYS competition.

Fortunately, I found Awsaf's code and published my 1st (Gemma 1.1-7b-instruct-en just 34 min. ago on May 10, 2024)

[Gemma 1.1 7B Int8 Load](https://www.kaggle.com/code/awsaf49/gemma-1-1-7b-int8-load) By Awsaf.

Thanks in advance,

Marília. 



---

 # Comments from other users

> ## Adnan Alaref
> 
> Hi [@mpwolke](https://www.kaggle.com/mpwolke) ,try to reduce batch size,restart the kernel
> 
> 
> 
> > ## Marília PrataTopic Author
> > 
> > My  batch_size = 1    Could it be lower? Zero or negative 😆
> > 
> > 
> > 


---

> ## Kaizhao Liang
> 
> I don't think we could load any pretrained model bigger than 1B, since the RAM runs out.
> 
> 
> 
> > ## Marília PrataTopic Author
> > 
> > I don't know how the model works on a submission due to its memory. However, I was facing issues even without submitting. Just at the beginning of the code.
> > 
> > Fortunately, I found Awsaf's code: [Gemma 1.1 7B Int8 Load](https://www.kaggle.com/code/awsaf49/gemma-1-1-7b-int8-load) and published my 1st (Gemma 1.1-7b-instruct-en just 34 min. ago)
> > 
> > Thank you Kaizhao.
> > 
> > 
> > 


---

> ## Matin Mahmoudi ✨
> 
> Try reducing the batch size, using mixed precision (float16), or lowering the memory fraction to handle Gemma Keras 1.1-7b. If that doesn't work, maybe go for a smaller model or use gradient accumulation [@mpwolke](https://www.kaggle.com/mpwolke).
> 
> 
> 
> > ## Marília PrataTopic Author
> > 
> > Hi Matin,
> > 
> > The batch size is only 1.
> > 
> > I changed to Gemma Keras 1.1_2b_instruct_en to reach at the end of the code (instead of the 7b).
> > 
> > Though the hosts pinned the 7b.
> > 
> > Thank you.
> > 
> > 
> > 


---

