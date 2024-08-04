# [解決済み] 回答は大文字小文字を区別しますか？
**Araik Tamazian** *2024年7月5日(金) 19:55:09 日本標準時* (0票)

回答は大文字小文字を区別せずに正答とみなされますか？それとも、完全に一致する必要がありますか？
例えば、キーワードが "car" で、LLMの回答が "Car" の場合、これは正答になりますか？

---
# 他のユーザーからのコメント
> ## waechter
> 
> はい、回答は大文字小文字を区別しません。
> 
> llm_20_questions.py では、以下のような関数を使用しています。
> 
> ```python
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
> "THE CAR", "CAR", "Car," などは、キーワード "car" に対する正答です。
> 
> 
> 
--- 

