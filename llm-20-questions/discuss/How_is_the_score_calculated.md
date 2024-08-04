# How is the score calculated?

**OminousDude** *Mon May 27 2024 11:12:07 GMT+0900 (日本標準時)* (0 votes)

I was looking through some episodes and in some, I see massive changes in the score up to +64 and -64 but in some, I see stuff like +0 +1 +4 etc. I was wondering how this is calculated. Thank you for the help!



---

 # Comments from other users

> ## Chris Deotte
> 
> The evaluation page says:
> 
> Each submission has an estimated skill rating which is modeled by a Gaussian N(μ,σ2) where μ is the estimated skill and σ represents the uncertainty of that estimate which will decrease over time.
> 
> When you upload a submission, we first play a validation episode where that submission plays against copies of itself to make sure it works properly. If the episode fails, the submission is marked as error and you can download the agent logs to help figure out why. Otherwise, we initialize the submission with μ0=600 and it joins the pool of for ongoing evaluation.
> 
> I have noticed that a true win or loss changes score more than a tie (i.e. no team gets a correct answer).
> 
> 
> 
> > ## OminousDudeTopic Author
> > 
> > Thanks very much!
> > 
> > 
> > 


---

