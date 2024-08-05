# 要約 
コンペのディスカッションでは、タイプミスを含むキーワードの処理について話し合われています。ユーザーtiod0611がいくつかのタイプミスの例を挙げ、エージェントが正しい単語を提供した場合のスコア結果についての懸念を表明しています。これに対して、他の参加者からの回答があります。

DJ Sterlingは、これらのキーワードがすでにセットから削除されたことを報告しています。RS Turleyは、間違った綴りの回答が認識されない可能性があることを指摘し、各キーワードには正解と見なされる代替文字列のリストがあるが、指摘された例には正しい代替が存在しないと説明しています。

tiod0611は意図的に間違ったキーワードで回答すべきだと考え、勝利した例も挙げています。また、大文字小文字の違いについての質問もあり、tiod0611はエージェントの試合での勝利の例をもって問題ないと述べています。全体として、タイプミスや綴りの正確さに関する懸念が多くの意見を呼んでいます。

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

# How Are Keywords with Typographical Errors Handled?

**tiod0611** *Thu Jun 27 2024 20:40:22 GMT+0900 (日本標準時)* (5 votes)

Hello,

While analyzing the keywords, I found a few words that seem to contain typographical errors. The list of these words is as follows:

isafahan iran → isfahan

nurumberg germany → nuremberg

zincantan mexico → zinacantan

mount saint lias → mount saint elias

On the left are the words from the keywords.py file, and on the right are the actual words. I am curious about the scoring results when an agent encounters these keywords and provides the correct word.

I am concerned that answering "isfahan" for "isafahan" might result in an incorrect response.



---

 # Comments from other users

> ## DJ Sterling
> 
> Sorry for the mistakes here.  These keywords have been removed from the set entirely.
> 
> 
> 
> > ## tiod0611Topic Author
> > 
> > Thank you for your action. 😎
> > 
> > 
> > 


---

> ## RS Turley
> 
> Sadly, in those cases, the correctly spelled answer would not be recognized. 
> 
> While each keyword has a list of potential alternative strings that would be marked correct, none of the examples you shared above have correctly spelled alternatives in the file.
> 
> 
> 
> > ## tiod0611Topic Author
> > 
> > Thank you for answering. I think we should intentionally answer with the incorrect keyword. For example, if the keyword is "isfahan," we should answer "isafahan" instead.
> > 
> > 
> > 
> > ## Kirill Yakunin
> > 
> > What about capitalization? Does "headphones" vs "Headphones" matter? "Mount saint elias" vs "mount saint Elias"?
> > 
> > 
> > 
> > > ## tiod0611Topic Author
> > > 
> > > I think It doesn't matter. In game my agent played, the keyword was "granola", but it answered with "Granoal". It got the win.
> > > 
> > > 
> > > 


---



</div>
<div class="column-right">

# 日本語訳

# タイプミスを含むキーワードはどのように処理されるのか？
**tiod0611** *2024年6月27日（木）20:40:22 JST* (5票)
こんにちは、  
キーワードを分析していると、いくつかの単語にタイプミスが含まれているように見えることに気付きました。これらの単語のリストは次の通りです：
isafahan iran → isfahan  
nurumberg germany → nuremberg  
zincantan mexico → zinacantan  
mount saint lias → mount saint elias  
左側はkeywords.pyファイルの単語、右側は実際の単語です。エージェントがこれらのキーワードに遭遇し、正しい単語を提供した場合のスコア結果について興味があります。  
「isafahan」に対して「isfahan」と答えることが間違った応答になるのではないかと心配しています。  
---  
 # 他のユーザーからのコメント  
> ## DJ Sterling  
>  
> 申し訳ありませんが、ここに間違いがありました。これらのキーワードはセットから完全に削除されました。  
>  
>  
> > ## tiod0611 トピック作成者  
> >  
> > ご対応ありがとうございます。😎  
> >  
> >  

---  
> ## RS Turley  
>  
> 残念ながら、その場合、正しく綴られた回答は認識されません。  
> 各キーワードには、正解と見なされる可能性のある代替文字列のリストがありますが、上記の例には正しく綴られた代替がファイルに含まれていません。  
>   
>  
> > ## tiod0611 トピック作成者  
> >  
> > ご回答ありがとうございます。私は、意図的に間違ったキーワードで答えるべきだと思います。例えば、「isfahan」というキーワードに対して「isafahan」と答えるべきです。  
> >  
> >  

>  
> > ## Kirill Yakunin  
> >  
> > では、大文字小文字はどうですか？「headphones」と「Headphones」の違いは問題になりますか？「Mount saint elias」と「mount saint Elias」の違いは？  
> >  
> >  
> > > ## tiod0611 トピック作成者  
> > >  
> > > > 問題ないと思います。私のエージェントがプレイしたゲームでは、キーワードが「granola」だったのに対して、「Granoal」と答えましたが、勝利を収めました。  
> > >  
> > >  


</div>