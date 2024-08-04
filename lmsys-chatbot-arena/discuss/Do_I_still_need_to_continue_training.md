# Do I still need to continue training?

**KeShuang Liu** *Fri Jul 26 2024 14:05:04 GMT+0900 (日本標準時)* (0 votes)

I have fine tuned many models, but the losses have remained almost unchanged. Is it necessary for me to continue training because I haven't trained enough? I find it difficult to make a decision at this point.This is my current validation set loss curve, which I verify every 2000 steps



---

 # Comments from other users

> ## S J Moudry
> 
> Are you testing on a validation set? I'd be more worried about performance there.  I'd also check my warmup steps and set them around 5-20%, having too few can cause a big drop right away but then you never really improve.
> 
> 
> 


---

