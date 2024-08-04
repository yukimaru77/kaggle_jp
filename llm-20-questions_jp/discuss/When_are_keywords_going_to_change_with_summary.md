# 要約 
このディスカッションは、Kaggleの「LLM 20 Questions」コンペティションにおけるキーワードの変更に関するものです。

当初、キーワードは6月の第一週に更新される予定でしたが、遅延が発生しました。OminousDudeは、変更の遅延理由と、いつ変更されるのかを質問しています。

Bovard Doerschuk-Tiberiは、新しいキーワードがその日にロールアウトされる予定であると回答しています。

Guillaume Gillesは、キーワードが変更されたのは、keywords.pyファイルにcountry、city、landmarkが追加されたためだと推測しています。しかし、OminousDudeは、キーワードは常にcountry、city、landmarkであり、person、place、thingではなかったと指摘しています。

最終的に、Guillaume Gillesは、カテゴリが現在placeとthingsであることを確認しています。


---
# キーワードはいつ変更されますか？
**OminousDude** *2024年6月17日(月) 08:24:58 JST* (5 votes)
以前は6月の第一週に変わる予定でしたが、ご覧のとおりまだ変更されていません。先週は
編集: 来週の初めにはロールアウトされる予定です。遅延をお詫び申し上げます！
しかし、今週の終わりまでに変更は行われないのでしょうか？もしお答えいただけるなら、この遅延の理由は何でしょうか？
---
# 他のユーザーからのコメント
> ## Bovard Doerschuk-Tiberi
> 
> 新しい単語は今日ロールアウトされる予定です。
> 
> 
> 
---
> ## Guillaume Gilles
> 
> キーワードは、keywords.pyファイルにcountry、city、landmarkが含まれるようになったため、変更されたと思います。当初のカテゴリはperson、place、thingでした。
> 
> 以下はファイルの抜粋です。
> 
> ```
> """20 Questionsのキーワードリスト"""
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
> > キーワードは常にcountry、city、landmarkであり、person、place、thingではありませんでした。彼らはすぐにpersonとobjectを追加することを約束していました。
> > 
> > 
> > 
> > > ## Guillaume Gilles
> > > 
> > > 私の混乱をお許しください。
> > > 
> > > 正しく理解していれば、カテゴリは現在placeとthingsです。
> > > 
> > > 
> > > 
---

