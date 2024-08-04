# Can I win only using Kaggle resources?

**Areej Malkawi** *Mon Jun 10 2024 03:35:55 GMT+0900 (日本標準時)* (5 votes)

The data of this competition are huge, I saw many public notebooks that used some pre-trained models for inference and I tried to use a pre-trained model to train the given competition data but I'm facing memory\score trade-off, am I supposed to use something more than Kaggle GPU\ TPU quota to overcome memory issues? as well as getting high LB score?

can I win or be at the top of LB without using external resources?



---

 # Comments from other users

> ## Ebi
> 
> 
> can I win or be at the top of LB without using external resources?
> 
> I think it's almost impossible. And this applies to most Kaggle competitions, because in most cases, you need to do a lot of experiment cycles.  
> 
> In fact, I've been participating for about three years using a CPU-only laptop and a cheap cloud service like Colab, but I've only managed to get a silver medal. I bought an RTX 4090 a few months ago and was able to get a gold medal right away, which gives me an advantage in this competition too.  
> 
> 
> 
> > ## Hassan Abedi
> > 
> > Yeah, for most NLP competitions, having a good GPU with lots of VRAM makes a big difference. 
> > 
> > 
> > 
> > ## Valentin Werner
> > 
> > Note that renting a GPU starts (in Germany) around 50 cent / hour - let's say a training takes 8 hours, thats 4€. You will do some iterations, so you will definetly spent more money, BUT a 4090 is about 1800€ in Germany - so you can do about 450 trainings (or 3600 hours of training!!) on a rented GPU. If you want to try something before doing such a heavy investment, you could start like that.
> > 
> > Further, since Kaggle provides you 30 GB of VRAM (vs. about 23 GB on a Windows PC with a 4090), you can try all the things before going into investment. The big blocker with kaggle GPUs is speed, not possibilities.
> > 
> > 
> > 


---

> ## tanaka
> 
> Hmm I understood,  it seems quite difficult to compete in these competitions without using external resources.
> 
> However, I feel that suddenly buying a GPU is a high hurdle.
> 
> it seems best to try out various options like Colab or other GPU rental servers, and then decide whether to buy or rent a GPU.
> 
> [Vast.ai](http://vast.ai/) seems to be a popular option, doesn't it 🤔?
> 
> - [https://vast.ai/](https://vast.ai/)
> 
> - [https://cloud-gpus.com/](https://cloud-gpus.com/)
> 
> - [https://gist.github.com/devinschumacher/87dd5b87234f2d0e5dba56503bfba533](https://gist.github.com/devinschumacher/87dd5b87234f2d0e5dba56503bfba533)
> 
> - [https://getdeploying.com/reference/cloud-gpu](https://getdeploying.com/reference/cloud-gpu#paperspace)
> 
> 
> 
> > ## Ebi
> > 
> > I have never used vast.ai, but I personally like  [jarvislabs.ai](https://jarvislabs.ai/). 
> > 
> > It is easy and fast to create an instance and access it via SSH. I think the price is also very cheap. I mainly used it until I switched to a home server.
> > 
> > 
> > 


---

> ## Andreas Bisi
> 
> Considering past NLP competitions, you would need external resources to finish in the gold-medal area. However, I believe with a TF-IDF solution (on kaggle hardware) it's doable to finish in the bronze-medal area with some luck…
> 
> 
> 


---

