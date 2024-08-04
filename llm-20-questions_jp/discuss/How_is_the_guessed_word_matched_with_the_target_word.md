# 推測された単語はどのようにターゲット単語と照合されるのですか？
**Nicholas Broad** *2024年5月16日木曜日 10:59:29 日本標準時* (5 votes)
正規化（小文字化、特定の文字の削除）はありますか？
完全一致である必要がありますか？
多くの類似の形態を持つ単語（jump、jumped、jumpingなど）の場合、正しく推測するには正確な単語を当てなければならないのですか？
---
# 他のユーザーからのコメント
> ## waechter
> 
> こんにちは、
> 
> llm_20_questions.py で、正規化を行うこの関数を見つけました。
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
> keywords.py では、いくつかのキーワードに代替の有効な回答があることがわかります。例：
> 
> ```
> {
>         "keyword": "congo",
>         "alts": ["republic of the congo", "congo brazzaville", "congo republic"]
>       }
> 
> ```
> 
> お役に立てれば幸いです！
> 
> 
> 
---
> ## Khoi Nguyen
> 
> 例えば、単語が小文字かどうかを尋ねることができます ¯\_(ツ)_/¯
> 
> 
> 
--- 

