# 要約 
ディスカッションでは、ターゲット単語と提案された単語との一致に関する疑問が提起されています。主な質問は、正規化プロセスがあるかどうか、完全一致が必要なのか、及び類似形（例: "jump", "jumped", "jumping"）に対して正確な単語が必要かどうかです。

**ウェヒター**は、正規化に関する関数をコードから引用して、この関数が提案された単語を整形し、ターゲット単語と比較する方法を示しています。最終的に、正規化された提案単語がターゲット単語と一致すれば正解となり、類似の代替語（実例として"congo"に対する異なる表現）が示されています。

**ホイ・グエン**は、単語が小文字かどうかを確認することを提案しています。

このディスカッションは、正解とされる単語の特定の要件に関する理解を深めることを目的としています。

---


<style>
.column-left{
  float: left;
  width: 47.5%;
  text-align: left;
}
.column-right{
  float: right;
  width: 47.5%;
  text-align: left;
}
.column-one{
  float: left;
  width: 100%;
  text-align: left;
}
</style>


<div class="column-left">

# original

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



</div>
<div class="column-right">

# 日本語訳

# 推測した単語はターゲット単語とどのように一致しますか？
**ニコラス・ブロード** *2024年5月16日 10:59:29 JST* (5票)
正規化はありますか（小文字にする、特定の文字を削除するなど）？
完全一致が必要ですか？
もし、その単語に多くの類似形（jump, jumped, jumping など）がある場合、正解を得るには正確な単語が必要ですか？
---
 # コメント
> ## ウェヒター
> 
> こんにちは、
> 
> llm_20_questions.py の中に、この正規化を行う関数が見つかりました：
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
> keywords.py では、一部のキーワードに異なる有効な回答の例があることがわかります：
> 
> ```
> {
>         "keyword": "congo",
>         "alts": ["republic of the congo", "congo brazzaville", "congo republic"]
>       }
> 
> ```
> 
> 参考になれば幸いです！
> 
> ---
> ## ホイ・グエン
> 
> 単語が小文字かどうかを常に尋ねることができますよ、例えば ¯\_(ツ)_/¯
> 
> ---


</div>