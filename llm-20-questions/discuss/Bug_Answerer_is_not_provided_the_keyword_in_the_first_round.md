# Bug: Answerer is not provided the keyword in the first round

**monoxgas** *Wed May 22 2024 10:16:36 GMT+0900 (日本標準時)* (7 votes)

This should be confirmed by the authors, but I'm fairly confident the answerer agent is not being passed the keyword in it's observation the first time it's used.

You can somewhat guess this by inspecting the replay logs, which show the answerer agents being active with empty keyword/category values on step 2. Also, agents frequently seem to "hallucinate" easy questions at the first round. This issue would be covered up by the fact that the fstring in the starter notebook simply accesses the obs.keyword prop blindly, which is an empty string.

I also added test code to our submission to raise an error if this situation ever occurs, and it does trigger the exception during validation:

```
def answer(base: rg.PendingChat, observation: Observation) -> t.Literal["yes", "no"]:
    if not observation.keyword:
        print("Keyword wasn't provided to answerer", file=sys.stderr)
        raise Exception("Keyword wasn't provided to answerer")

```

Exception Thrown

Answerer is passed the first question:

It selected 'yes' without a keyword available



---

 # Comments from other users

> ## Bovard Doerschuk-Tiberi
> 
> I'll take a look at this, thanks for reporting!
> 
> 
> 


---

