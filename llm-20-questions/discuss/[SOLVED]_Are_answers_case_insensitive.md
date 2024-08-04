# [SOLVED] Are answers case insensitive?

**Araik Tamazian** *Fri Jul 05 2024 19:55:09 GMT+0900 (日本標準時)* (0 votes)

Do we count an answer to be correct if it's the same regardless of letters cases, or it needs no be exactly the same?

Like: keyword is "car" - LLM answer is "Car" - is it the correct answer or not?



---

 # Comments from other users

> ## waechter
> 
> Yes answers are case insensitive
> 
> In llm_20_questions.py you will find the function used:
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
> "THE CAR", "CAR", "Car," etc.. are correct answers for the keyword "car"
> 
> 
> 


---
