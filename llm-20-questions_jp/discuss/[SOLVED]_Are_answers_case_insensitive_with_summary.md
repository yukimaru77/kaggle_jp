# 要約 
ディスカッションでは、ユーザーが「20の質問」コンペティションにおける回答の大文字と小文字に関する取り扱いについて質問しています。具体的には、例えば「car」というキーワードに対し回答が「Car」であった場合、それが正しいと見なされるかどうかを尋ねています。

他のユーザーからの回答によると、答えは大文字と小文字を区別せず、正しいと見なされるとのことです。このことは、コード内の関数によっても示されています。具体的には、入力された答えは小文字に変換され、文中の「the」やスペース、句読点が取り除かれるため、「THE CAR」、「CAR」、「Car」などはすべて「car」と同じ答えとして認識されます。

---
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
