# 要約 
コンペのディスカッションでは、キーワードの変更に関する質問が話題になっています。ユーザーのOminousDudeは、キーワードが6月の最初の週に変更されると聞いていたが、その実現が遅れており、具体的な変更日時や遅延の理由について尋ねています。

Bovard Doerschuk-Tiberiは、新しい単語がその日展開されるとの情報を提供しています。一方、Guillaume Gillesは、キーワードは既に変更されており、初期のカテゴリである「人」「場所」「物」から「国」「都市」「ランドマーク」に置き換えられていると説明しています。

OminousDudeは、現在のキーワードが常に「国」「都市」「ランドマーク」であったのではなく、「人」と「物」が追加される約束があったことを指摘し、Guillaume Gillesは混乱を招いたことを謝罪しました。全体として、キーワードの変更とその進行状況に関するやり取りが続いています。

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

# When are keywords going to change?

**OminousDude** *Mon Jun 17 2024 08:24:58 GMT+0900 (日本標準時)* (5 votes)

Earlier we were told that they would change first week of June, but as you can see we haven't had this. Last week we were told

EDIT: This will now roll out early next week, sorry for the delay!

But it is no the end of this week when will the changes be made? And if you can answer what is the reason for this delay?



---

 # Comments from other users

> ## Bovard Doerschuk-Tiberi
> 
> New words should roll out today
> 
> 
> 


---

> ## Guillaume Gilles
> 
> I believe keywords have been changed since the keywords.py file now includes: country, city, and landmark instead of the initial categories: person, place,  and thing.
> 
> Below, is an excerpt of the file:
> 
> ```
> """List of keywords for 20 Questions."""
> 
> KEYWORDS_JSON = """
> [
>   {
>     "category": "country",
>     "words": [
>       {
>         "keyword": "afghanistan",
>         "alts": []
>       },
> 
> ```
> 
> 
> 
> > ## OminousDudeTopic Author
> > 
> > Keywords were always country, city, and landmark and were never person, place, and thing. They were promising to add person and object soon.
> > 
> > 
> > 
> > > ## Guillaume Gilles
> > > 
> > > Forgive me for my confusion.
> > > 
> > > If I understood correctly, categories are now: place and things.
> > > 
> > > 
> > > 


---



</div>
<div class="column-right">

# 日本語訳

# キーワードの変更はいつですか？
**OminousDude** *2024年6月17日 月曜日 08:24:58 GMT+0900 (日本標準時)* (5票)
以前、キーワードは6月の最初の週に変更されると言われていましたが、見ての通り、それは実現していません。先週、私たちは
EDIT: これが来週初めに展開されるとのことです。遅延についてお詫びします！
しかし、今週末ではなく、変更はいつ行われるのでしょうか？そして、この遅延の理由は何ですか？

---
 # 他のユーザーからのコメント
> ## Bovard Doerschuk-Tiberi
> 
> 新しい単語は今日展開されるはずです。

---
> ## Guillaume Gilles
> 
> キーワードは既に変更されていると思います。なぜなら、keywords.pyファイルには、初期のカテゴリである「人」「場所」「物」の代わりに、「国」「都市」「ランドマーク」が含まれているからです。
> 
> 以下は、そのファイルの抜粋です：
> 
> ```python
> """20の質問のためのキーワード一覧。"""
> 
> KEYWORDS_JSON = """
> [
>   {
>     "category": "country",
>     "words": [
>       {
>         "keyword": "afghanistan",
>         "alts": []
>       },
> 
> ```

> > ## OminousDude トピック著者
> > 
> > キーワードは常に「国」「都市」「ランドマーク」であり、「人」「場所」「物」ではありませんでした。近々「人」と「物」を追加する約束がありました。
> > 
> > 
> > > ## Guillaume Gilles
> > > 
> > > 混乱させてしまい、お詫びします。
> > > 
> > > 正しく理解したのであれば、現在のカテゴリは「場所」と「物」ですね。
> > > 
> > > 
> > > 
---


</div>