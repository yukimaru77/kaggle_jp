# Expectation for Kaggle Resources?

**Cody_Null** *Thu Aug 01 2024 08:16:38 GMT+0900 (日本標準時)* (11 votes)

Hi all, my team as well as what seems like others seem to be struggling with submission times. Even submissions that we ran in 6 hours before are now timing out? We have significantly raised our CV in the last few days but have been entirely unable to get results for it due to this compute issue. I was hoping some of the Kaggle staff could help speak to what is going on? I am familiar that close to the end of competitions in the last 2 or 3 days things run a bit slower but we are experiencing 2 times longer inference time than 4 days ago and have been ever since 7 days to go! It would be a shame to put in all this work over the last several months and not get to benefit from putting it all together. 



---

 # Comments from other users

> ## Valentin Werner
> 
> Are you 100% sure you are running exactly the same script? We have been struggling with Resources too, but not along the lines of 50%. Eventhough this wastes a submission, if you have time for it, try the old notebook and version again.
> 
> To me it does not seem reasonable that participation rates raise GPU Processing times. It is not like we are all on the same two T4s. Also all the environments are containers, so they should be clean on every run.
> 
> 
> 
> > ## Cody_NullTopic Author
> > 
> > I totally agree, it is not completely identical but it is a small change and identical in simulated run times. It’s not quite a 50% slowdown but it’s fairly close! What once took 5.5 is now 9+
> > 
> > 
> > 
> > ## Rise_Hand
> > 
> > It's not same as container actually. Some sub obviously need more computer source can finish running faster than the one which need less. So it's just a luck game to be allocated to a better machine tbh
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > Agreed, over the lifecycle of every chip performance may vary. This also goes for room temperature at servers etc. 
> > > 
> > > The point, I am making about containerization is that when you submission is over you have a clean GPU, its not like you will share compute etc. - However, you can and will get worse chips. Its impossible for the kaggle team to have all GPUs available perform exactly the same. 
> > > 
> > > 
> > > 


---

> ## yechenzhi1
> 
> Try to reduce your max-length? I've encountered a similar issue, and I suspect that the test data may be longer than what we used for training.
> 
> 
> 


---

> ## Attacker
> 
> People's participation rate rises before the competition closes, so the server becomes unstable.
> 
> 
> 
> > ## Cody_NullTopic Author
> > 
> > That is true but I don’t notice anything different from this comp than others but I have never seen a 50% slowdown of submissions before :/ Of course we can’t expect Kaggle to have it be seamless especially when they are providing these GPUs for free but I would like a little more clarity on what is going on and if we should expect it to change before the deadline.
> > 
> > 
> > 


---

> ## Korey Ma
> 
> I am afraid that my new submissions will time out🫠
> 
> 
> 
> > ## Valentin Werner
> > 
> > 
> > 
> > 
> > 


---

