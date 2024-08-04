# question about the quota of GPU

**Dlond Mike** *Mon Jul 29 2024 20:57:34 GMT+0900 (日本標準時)* (1 votes)

Does submission take the quota of GPU?if so,how much quota it will take?



---

 # Comments from other users

> ## CPMP
> 
> saving your notebook runs it again using your quota. Once this is done, submitting does not use your quota anymore.
> 
> 
> 


---

> ## Yi-Fu Chen
> 
> ```
> import os
> if os.getenv('KAGGLE_IS_COMPETITION_RERUN'):
>     pass
> else:
>     raise SystemExit
> 
> ```
> 
> Adding the above code at the front of the submitted notebook will quickly close the trial run notebook and retain the scored run.
> 
> 
> 


---

> ## Ravi Ramakrishnan
> 
> I usually submit to code competitions in a script. I use the below to ensure I don't use up my GPU quotas during my dummy LB submission- 
> 
> ```
> import pandas as pd
> sub_fl = pd.read_csv(.......submission.csv)
> 
> if len(sub_fl) <=10:
>     print(f"Submitting the dummy file")
>     sub_fl.to_csv("submission.csv", index = None)
> 
> else:
>     ....... (your script)
> 
> ```
> 
> [@dlondmike](https://www.kaggle.com/dlondmike) best of luck!
> 
> 
> 


---

> ## SeshuRaju 🧘‍♂️
> 
> [@dlondmike](https://www.kaggle.com/dlondmike) for scorning won't take GPU quota, but for generating the submitted notebook version ( even after submit, you can cancel the notebook, so GPU quota can be saved )
> 
> 
> 
> > ## Valentin Werner
> > 
> > From what I know (and experienes last week), the "save" notebook (not submit) also doesnt crash if it goes above quota. I think I ended last week on 32/30 hrs by accident 😃
> > 
> > 
> > 


---

> ## bao
> 
> There are two notebooks running when submitted. The scoring notebook does not use GPU quota, while the other one does.
> 
> 
> 


---

