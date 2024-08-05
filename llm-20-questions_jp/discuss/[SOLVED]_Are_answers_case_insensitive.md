# [解決済み] 答えは大文字と小文字を区別しないのか？
**Araik Tamazian** *2024年7月5日（金）19:55:09 GMT+0900 (日本標準時)* (0票)
答えが文字の大文字小文字を無視して同じであれば正しいと見なされるのか、それとも正確に同じである必要があるのか、教えていただけませんか？
例えば、キーワードが「car」の場合、LLMの答えが「Car」であれば、それは正しい答えになるのでしょうか？

---
# 他のユーザーからのコメント
> ## waechter
> 
> はい、答えは大文字と小文字を区別しません。
> 
> llm_20_questions.py では、使用される関数が見つかります：
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
> ```
> 
> 「THE CAR」、「CAR」、「Car」などは、キーワード「car」に対して正しい答えとなります。
> 
> ---
