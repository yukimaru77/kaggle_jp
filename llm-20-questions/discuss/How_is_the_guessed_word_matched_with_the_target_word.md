# How is the guessed word matched with the target word?

**Nicholas Broad** *Thu May 16 2024 10:59:29 GMT+0900 (日本標準時)* (5 votes)

Is there any normalization (lowercase, remove certain characters)?

Does it need to be an exact match?

If it is a word that has many similar forms (jump, jumped, jumping, etc.), do you have to get the exact word to get it right?



---

 # Comments from other users

> ## waechter
> 
> Hello,
> 
> In llm_20_questions.py I found this function that do the normalization:
> 
> ```
> def keyword_guessed(guess: str) -> bool:
>     def normalize(s: str) -> str:
>       t = str.maketrans("", "", string.punctuation)
>       return s.lower().replace("the", "").replace(" ", "").translate(t)
> 
>     if normalize(guess) == normalize(keyword):
>       return True
>     for s in alts:
>       if normalize(s) == normalize(guess):
>         return True
> 
>     return False
> 
> ```
> 
> In keywords.py we can see that some keyword have a alternative valid answer example:
> 
> ```
> {
>         "keyword": "congo",
>         "alts": ["republic of the congo", "congo brazzaville", "congo republic"]
>       }
> 
> ```
> 
> Hope this help!
> 
> 
> 


---

> ## Khoi Nguyen
> 
> You can always ask whether the word is lowercase for example  ¯\_(ツ)_/¯
> 
> 
> 


---

