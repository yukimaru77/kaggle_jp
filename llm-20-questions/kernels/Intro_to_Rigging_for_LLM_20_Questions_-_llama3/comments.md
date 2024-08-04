# Comments 

> ## Bhanu Prakash M
> 
> Hi [@robikscube](https://www.kaggle.com/robikscube),
> 
> Can I know how you got the vLLM server to run? because after I set the debugging to true, it gives the following error
> 
> INFO 06-18 21:44:58 selector.py:69] Cannot use FlashAttention-2 backend for Volta and Turing GPUs.
> 
> INFO 06-18 21:44:58 selector.py:32] Using XFormers backend.
> 
> and a long Traceback error with the final statement being
> 
> ValueError: Bfloat16 is only supported on GPUs with compute capability of at least 8.0. Your Tesla P100-PCIE-16GB GPU has compute capability 6.0. You can use float16 instead by explicitly setting thedtype flag in CLI, for example: --dtype=half
> 
> 
> 
> > ## Rob MullaTopic Author
> > 
> > What model are you trying to run?
> > 
> > 
> > 
> > > ## Bhanu Prakash M
> > > 
> > > phi-3 model with its weight layers converted to llama format
> > > 
> > > [https://huggingface.co/rhysjones/Phi-3-mini-mango-1-llamafied](https://huggingface.co/rhysjones/Phi-3-mini-mango-1-llamafied)
> > > 
> > > this is the exact model
> > > 
> > > 
> > > 
> > > ## Bhanu Prakash M
> > > 
> > > [@robikscube](https://www.kaggle.com/robikscube) any update?
> > > 
> > > 
> > > 
> > > ## Rob MullaTopic Author
> > > 
> > > Got it working here: [https://www.kaggle.com/code/robikscube/phi3-intro-to-rigging-for-llm-20-questions/](https://www.kaggle.com/code/robikscube/phi3-intro-to-rigging-for-llm-20-questions/)
> > > 
> > > 
> > > 


---

> ## OminousDude
> 
> Why am I getting the error "Process did not open port 9999 within 120 seconds"? [@robikscube](https://www.kaggle.com/robikscube)
> 
> 
> 
> > ## Rob MullaTopic Author
> > 
> > Let me take a look! Thanks for the heads up.
> > 
> > 
> > 
> > > ## OminousDude
> > > 
> > > Thank you very much! I am just experimenting with rigging to speed up my code I use a model that does not fit in the time allocation and this code really helps me!
> > > 
> > > 
> > > 


---

> ## OminousDude
> 
> Hi I was testing your code but when I ran it the code failed with the exception of "AttributeError: 'coroutine' object has no attribute 'last'
> 
> ". Have you had this error?
> 
> 
> 
> > ## Rob MullaTopic Author
> > 
> > Thanks for letting me know. I'm seeing that too. We're actively developing rigging and this appears to be a change made from our latest release. I'm updating the notebook to fix the change, or I may just pin an older version of rigging that should fix the problem.
> > 
> > 
> > 
> > > ## OminousDude
> > > 
> > > ok thank you!
> > > 
> > > 
> > > 
> > > ## OminousDude
> > > 
> > > Does version 7 work?
> > > 
> > > 
> > > 


---

> ## OminousDude
> 
> I am trying this on my local machine and it is not working do you have any idea why? [@robikscube](https://www.kaggle.com/robikscube) 
> 
> 
> 


---

> ## OminousDude
> 
> Not sure if this is a bug but this code only works with the "solidrust/Meta-Llama-3-8B-Instruct-hf-AWQ". I noticed this while experimenting with your code trying to use a larger version of Llama.
> 
> 
> 


---

