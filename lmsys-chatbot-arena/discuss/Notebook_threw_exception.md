# Notebook threw exception

**Kaizhao Liang** *Thu May 16 2024 05:57:49 GMT+0900 (日本標準時)* (3 votes)

locally on the sample test csv, it runs fine. But submission throws exception without any useful feedback on the error log. shouldn't have been OOM since it's running BS = 1.



---

 # Comments from other users

> ## Valentin Werner
> 
> I had a similar error - for me this was what fixed it: 
> 
> ```
>  row.prompt.replace("null", "'null'")
>  row.response_a.replace("null", "'null'")
>  row.response_b.replace("null", "'null'")
> 
> ```
> 
> 
> 
> > ## Kaizhao LiangTopic Author
> > 
> > ah that could be the edge case it was discussing the other threads, let me give it a try thanks!
> > 
> > 
> > 
> > > ## RickPack
> > > 
> > > Please let us know if that worked.
> > > 
> > > 
> > > 


---

> ## jiangli59
> 
> I also met the same problem. Any update?
> 
> 
> 
> > ## jiangli59
> > 
> > If you use Llama-8b, I think it may raise this error due to out-of-memory. Sad! So, this error could be the source of oom?
> > 
> > 
> > 


---

> ## RickPack
> 
> i experienced similar today with an R notebook. Wondering if the submission needs to be rounded to two decimal places. What a does BS mean?
> 
> 
> 
> > ## Kaizhao LiangTopic Author
> > 
> > batch size = 1
> > 
> > 
> > 
> > ## Kaizhao LiangTopic Author
> > 
> > It also runs two hours before hitting that error, so clearly some edge cases that have not been exposed. Could be something due to parsing. But the error itself is not helpful for debugging at all.
> > 
> > 
> > 
> > > ## Alex Golubev
> > > 
> > > You can try to take a sample (e.g. 10k) from train and run your script on it. Probably you have a chance to hit the same error. Btw, what is the error message?
> > > 
> > > 
> > > 


---

