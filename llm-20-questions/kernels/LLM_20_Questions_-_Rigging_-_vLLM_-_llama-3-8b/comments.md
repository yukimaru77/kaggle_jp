# Comments 

> ## OminousDude
> 
> Hi I was testing your code but when I ran it the code failed with the exception of "AttributeError: 'coroutine' object has no attribute 'last'
> 
> ". Have you had this error before?
> 
> 
> 
> > ## Rob Mulla
> > 
> > [@max1mum](https://www.kaggle.com/max1mum) - this is due to a new release of rigging that has some breaking changes with previous versions.
> > 
> > Try using pinned versions of the packages. Just change the install cell to this and it should work.
> > 
> > ```
> > # Dependencies (uv for speed)
> > !pip install uv==0.1.45
> > 
> > !uv pip install -U \
> >     --python $(which python) \
> >     --target /kaggle/tmp/lib \
> >     rigging==1.1.1 \
> >     kaggle
> > 
> > !uv pip install -U \
> >     --python $(which python) \
> >     --target /kaggle/tmp/srvlib \
> >     vllm==0.4.2
> > 
> > ```
> > 
> > 
> > 
> > > ## OminousDude
> > > 
> > > Thank you very much!!!
> > > 
> > > 
> > > 


---

