# Does post-processing apply to this competition?

**Nicole** *Wed Jul 24 2024 08:12:23 GMT+0900 (日本標準時)* (0 votes)

I tried to use some post-processing to deal with my prediction, but the effect was not good. Did you have any improvement in post-processing?



---

 # Comments from other users

> ## Valentin Werner
> 
> I tried some post processing early in the competition, which did also not work well for me. I think the intuition is that the model is basically already caibrating itself, meaning if it says "0.4" as highest probability, it will be right around 40% of the time. And 80% will be right around 80% of the time. 
> 
> If you now say 0.4 is not really confident, and that should be 0.33 , you will increase the loss in ~6 out of 10 cases (because the loss is lower if your predict 40% and it actually the right prediction).
> 
> I prepared this little code snippet to demonstrate this: 
> 
> ```
> from sklearn.metrics import log_loss
> 
> y_true = [[1,0,0]] * 4 + [[0,1,0]] * 3 + [[0,0,1]] * 3
> y_pred = [[0.4, 0.3, 0.3]] * 10
> print("raw log_loss:", log_loss(y_true, y_pred))
> # raw log_loss: 1.0888999753452235
> 
> y_true = [[1,0,0]] * 4 + [[0,1,0]] * 3 + [[0,0,1]] * 3
> y_pred = [[0.334, 0.333, 0.333]] * 10
> print("post processed (overconfident) log_loss):", log_loss(y_true, y_pred))
> # post processed (overconfident) log_loss): 1.0984133878031905
> 
> ```
> 
> Further, overconvidence is a killer. If you set a 0.8 (probably right in 80% of cases), to a 0.9, you will have a much higher loss in those 20% of cases, where you are now overconfident. You are penalized way higher for high-confidence wrong classifications.
> 
> I prepared this little code snippet to demonstrate this: 
> 
> ```
> from sklearn.metrics import log_loss
> 
> y_true = [[1,0,0]] * 2 + [[0,1,0]] * 8
> y_pred = [[0.1, 0.8, 0.05]] * 10
> print("raw log_loss:", log_loss(y_true, y_pred))
> # raw log_loss: 0.5877385652626266
> 
> y_true = [[1,0,0]] * 2 + [[0,1,0]] * 8
> y_pred = [[0.075, 0.90, 0.025]] * 10
> print("post processed (overconfident) log_loss):", log_loss(y_true, y_pred))
> # post processed (overconfident) log_loss): 0.6023418456154264
> 
> ```
> 
> I might be missing something in my intuition, but assuming your model is well calibrated, doing correction will more likely harm than fix anything.
> 
> 
> 
> > ## NicoleTopic Author
> > 
> > Totally agree with you
> > 
> > 
> > 


---

> ## Lorry Zou
> 
> I tried log-loss clipping, got same results.
> 
> 
> 


---

