# 要約 
このコンペのディスカッションでは、ユーザー **loh-maa** が進める「アルファベット検索」に基づく部分的な解決策について説明しています。投稿者は、このアプローチをシンプルかつエレガントに作成したとし、完全な解決策ではないものの、適応や改善の余地があると述べています。彼は、キーワード空間が公開されている場合は最適であり、知られていない場合でも有用性がある理由を二つ挙げています。他の制度や解決策に対する批判もあり、特に信頼性の問題に言及しています。

他のユーザーからのコメントもあり、**OminousDude** がコードを称賛し、**loh-maa** が他の参加者の意見にも関心を持っている様子がうかがえます。全体として、新しいアプローチの可能性や、それに対する賛否が議論の中心となっています。

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

# Alpha notebook, maybe the final one [LB 666+]

**loh-maa** *Thu Jul 25 2024 01:00:13 GMT+0900 (日本標準時)* (5 votes)

In the spirit of Conan the Barbarian and his majesty Mad Max the second! I hereby share the partial solution based on [alphabetical search](https://www.kaggle.com/code/lohmaa/llm20-agent-alpha). I spent time to make it so simple and elegant, that I am even delighted. It is not a complete solution, and that's actually splendid because it leaves room for adaptation and improvement, especially regarding the way to finish a failed alpha search.

I know some people dislike this whole idea though, perhaps because it's not based on LLMs, maybe for other reasons, but for me that's a bit irrational. Why?

First of all, it is not against the rules, and it is not unethical. Perhaps it was not entirely expected by the concept of this competition, but unexpected approaches are not a bad thing per se.

It is optimal when the keyword space is publicly known and the answerer can answer it.

Yet, contrary to some opinions, even if the keyword space is not known, it's not at all useless..

- for one, simply because one can still have many keywords on the list covered,

- for two, because one can combine it with LLMs.

There are many other solutions which basically do a similar thing, except less efficiently, e.g. asking questions about first letters, or whether the keyword is "on the following list". Even the ex-top solution so widely adored is based on such techniques. Surely there are some pros to those, too, I will not elaborate here.

Finally, as a matter of adoption -- we may say Alpha is not reliable because many agents accept the handshake and then answer the Alpha questions incorrectly, and that's a valid point. However, regardless of whether such behavior is intentional or unintentional, it is never in the legitimate interest of an agent to fail the team on purpose. So if anybody still doesn't like or believe that lexicographical search is effective, they can simply refuse the handshake and the team may try its luck in another way. In an interesting way it's a clash between rational vs irrational.



---

 # Comments from other users

> ## OminousDude
> 
> Very good code 👍👍👍👍👍👍👍
> 
> 
> 
> > ## loh-maaTopic Author
> > 
> > [@max1mum](https://www.kaggle.com/max1mum) Thanks, well technically it's not a model, but anyway, from downvotes it seems some people disagree with your opinion.. I'd love to hear what is it exactly that they dislike or disapprove about it. So if anybody knows, then please help me understand.
> > 
> > 
> > 


---



</div>
<div class="column-right">

# 日本語訳

# Alphaノートブック、もしかしたら最終版 [LB 666+]
**loh-maa** *2024年7月25日 01:00:13 JST* (5票)
コナン・ザ・バーバリアンとマッドマックス2の精神に則り、私はこちらの[アルファベット検索](https://www.kaggle.com/code/lohmaa/llm20-agent-alpha)に基づいた部分的な解決策を共有します。とてもシンプルでエレガントに作り上げることに時間をかけたので、自分でも嬉しく思っています。これは完全な解決策ではありませんが、それが素晴らしい理由は、特に失敗したアルファ検索を完了させる方法に関して、適応や改善の余地を残しているからです。
この考え方を嫌う人もいるかもしれませんが、それはLLMに基づいていないからか、他の理由かもしれませんが、私には少し不合理に思えます。なぜでしょうか？
まず第一に、それはルールに反していないし、不道徳でもありません。おそらくこの競技の概念からは完全に期待されていなかったかもしれませんが、予期しないアプローチが必ずしも悪いことではありません。
キーワード空間が公開されていて、回答者がそれに答えられる場合は最適です。
とはいえ、一部の意見とは逆に、キーワード空間が知られていない場合でも、全く無駄というわけではありません。
- 一つ目は、まだ多くのキーワードをリストにカバーできるからです。
- 二つ目は、それをLLMと組み合わせることができるからです。
他にも基本的に同様のことを行っているが、効率は劣るソリューションはいくつも存在します。例えば、最初の文字について質問をしたり、「以下のリストにキーワードが含まれているか」を尋ねたりするものです。かつてのトップソリューションもこのような技術に基づいて非常に称賛されています。それらにもメリットがあることは確かですが、ここでは詳しくは触れません。
最後に、受け入れの問題として、私たちはアルファが信頼性がないと述べることができます。なぜなら、多くのエージェントがハンドシェイクを受け入れ、その後アルファの質問に誤った回答をするからです。これは有効な指摘ですが、そのような行動が意図的であれ非意図的であれ、エージェントにとってチームを故意に失敗させることは決して正当な利益ではありません。だから、もしまだ辞書検索が効果的だと思わない方がいれば、ハンドシェイクを拒否すればいいのです。そうすれば、チームは別の方法で運を試すことができます。興味深い点として、これは合理的な思考と非合理的な思考の対立です。
---
 # 他のユーザーからのコメント
> ## OminousDude
> 
> 素晴らしいコードですね 👍👍👍👍👍👍👍
> 
> 
> > ## loh-maaトピック作成者
> > 
> > [@max1mum](https://www.kaggle.com/max1mum) ありがとうございます。技術的にはモデルではありませんが、それでも、ダウンボートから見ると、あなたの意見に反対している人がいるようです。彼らが具体的に何を嫌ったり、不快に思ったりしているのか、ぜひ教えてもらいたいです。もし誰かが知っているなら、理解する手助けをしてもらえればと思います。
> > 
> > 
---


</div>