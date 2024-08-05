# 要約 
このディスカッションは、コンペティション参加者が独自のデータセットを処理する際に、特殊トークン（`+ +` や ` , , ` など）の効率性について疑問を呈しているものです。

投稿者は、特殊トークン ` , , ` を追加してモデルを訓練したものの、結果が良くないことを報告しています。

コメント欄では、他のユーザーが埋め込みサイズを変更することや、Gemma に含まれる未使用の特殊トークンを再利用することを提案しています。投稿者はこれらの提案に感謝し、試してみることを表明しています。

このディスカッションは、特殊トークンの使用に関する重要なポイントを浮き彫りにしています。特殊トークンを追加する際には、埋め込みサイズや未使用トークンの再利用など、モデルの構成を適切に調整することが重要です。


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

# special token Efficiency

**박민욱peterminpark** *Fri Jul 19 2024 07:18:04 GMT+0900 (日本標準時)* (0 votes)

many organized their dataset into  +  +  input text form. I tried adding , ,  as special tokens and trained a model but the result was not good does anyone know why this is the case.



---

 # Comments from other users

> ## cm391
> 
> have you resized the embedding to take into account that you have added new tokens?
> 
> Gemma contains some spare special tokens in its tokenizer - you could just repurpose those!
> 
> 
> 
> > ## 박민욱peterminparkTopic Author
> > 
> > thx
> > 
> > I did resize my model.
> > 
> > recycling unused special token is a good idea. I'll try that out
> > 
> > 
> > 


---



</div>
<div class="column-right">

# 日本語訳

## 特殊トークンの効率性

**박민욱peterminpark** *2024年7月19日 金曜日 07:18:04 GMT+0900 (日本標準時)* (0票)

多くの人が自分のデータセットを `+ +` のような入力テキスト形式に整理しています。私は ` , , ` を特殊トークンとして追加してモデルを訓練してみましたが、結果は良くありませんでした。なぜでしょうか？

---

## 他のユーザーからのコメント

> ## cm391
> 
> 新しいトークンを追加したことを考慮して、埋め込みのサイズを変更しましたか？
> 
> Gemma には、いくつかの余分な特殊トークンが含まれています。それらを再利用できます！
> 
> 
> 
> > ## 박민욱peterminpark トピック作成者
> > 
> > ありがとう
> > 
> > モデルのサイズを変更しました。
> > 
> > 使用されていない特殊トークンを再利用するのは良いアイデアですね。試してみます。
> > 
> > 
> > 
--- 



</div>