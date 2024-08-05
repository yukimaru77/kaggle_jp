# 要約 
ディスカッションでは、「戦略的な質問応答」というコンセプトについての意見が交わされています。ユーザーのmarketneutralが、要約にあるように「はい」か「いいえ」で回答することに関して疑問を呈し、「戦略的に回答する」とはどういう意味かを尋ねています。

いくつかのコメントでは、戦略的な質問と回答がバイナリサーチアルゴリズムに似ているとの意見が示されています。G John Raoはこの点を強調し、Nicholas Broadはモデルが不適切に回答するとスコアに悪影響を及ぼす可能性があると指摘しました。また、Rakiは、質問者が情報を正確に把握することの重要性を述べ、特にあいまいさを考慮した回答が求められる場面について言及しています。彼は、状況に応じて「はい」または「いいえ」と回答する必要がある場合があると説明し、特定の単語（例: スマウグ）に関する解釈の難しさに触れています。

全体として、このディスカッションでは、戦略的な質問とその応答がゲームにおけるパフォーマンスにどのように影響するか、またその実践的なアプローチについての見解が共有されています。

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

# What is "strategic question answering"?

**marketneutral** *Thu May 16 2024 08:06:58 GMT+0900 (日本標準時)* (5 votes)

From the Overview

```
Each team will consist of one guesser LLM, responsible for asking questions and making guesses, and one answerer LLM, responsible for responding with "yes" or "no" answers. Through strategic questioning and answering, the goal is for the guesser to correctly identify the secret word in as few rounds as possible.

```

The response can only be "yes" or "no", correct? What does it mean to answer strategically in this context?



---

 # Comments from other users

> ## G John Rao
> 
> The phrase is, "Through strategic questioning and answering" - Think of it as a binary search algorithm. 
> 
> 
> 


---

> ## Nicholas Broad
> 
> If your model is bad at answering the questions it will ultimately hurt your own score. Maybe there are different techniques to make sure you answer correctly
> 
> 
> 
> > ## VolodymyrBilyachat
> > 
> > Could be a end game step, where questioner gets all questions and answers and make sure they are right
> > 
> > 
> > 


---

> ## Raki
> 
> I think "correct" is the most obvious and important part for the question answerer and it might help to have a knowledge base here, not just the knowledge embedded in the model weights. 
> 
> The "strategic" can also mean sensible handling of ambiguous cases. 
> 
> EG if the keyword was "Smaug" (dragon from The Hobbit), the "is reptile" property might be ambiguous and it could depend on the situation if you should answer yes/no. 
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# 「戦略的な質問応答」とは何ですか？
**marketneutral** *2024年5月16日 08:06:58 GMT+0900 (日本標準時)* (5票)
概要の中に次のようにあります。
```
各チームは、質問をし推測を行う「予想者LLM」と、「はい」または「いいえ」で回答する「回答者LLM」の1つずつで構成されます。戦略的な質問と回答を通じて、予想者ができるだけ少ないラウンドで秘密の単語を特定することを目指します。
```
回答は「はい」または「いいえ」のみで正しいですよね？この文脈で「戦略的に回答する」とはどういう意味なのでしょうか？
---
# 他のユーザーからのコメント
> ## G John Rao
> 
> 「戦略的な質問と回答を通じて」というフレーズを考えてみてください。これはバイナリサーチアルゴリズムのようなものです。  
> 
---
> ## Nicholas Broad
> 
> モデルが質問にうまく回答できない場合、最終的には自分のスコアを損なうことになります。正しく回答するためのさまざまな手法があるかもしれません。  
> 
> > ## VolodymyrBilyachat
> > > 終盤のステップである可能性があります。質問者がすべての質問と回答を把握し、正確であることを確認する段階です。  
> > >   
> > >   
> ---
> 
> ## Raki
> 
> 私は、「正確」であることが質問の回答者にとって最も明白で重要な部分であり、単にモデルの重みに組み込まれた知識だけでなく、知識ベースがあると助けになると思います。  
> 
> 「戦略的」というのは、あいまいなケースの賢明な扱いを意味することもできます。  
> 例えば、キーワードが「スマウグ」（『ホビットの冒険』のドラゴン）であった場合、「爬虫類であるか」の特性はあいまいであり、状況によっては「はい」または「いいえ」と回答すべきかが依存する可能性があります。  
> 


</div>