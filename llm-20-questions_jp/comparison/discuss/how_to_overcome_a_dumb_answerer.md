# 要約 
コンペのディスカッションでは、kaoutarが回答者エージェントの不正確さに苦しんでいる様子を共有しました。彼は、誤った回答によって勝利のチャンスを逃してしまうことが多いと述べています。これに対し、Matthew S Farmerは、推測者プロンプトを工夫し、一貫性のない回答を指摘する方法を提案しました。さらに、質問者が矛盾を探し出すための異なる質問のアプローチを考えるのも有効かもしれないと助言しています。kaoutarは、その後、回答者のパフォーマンスを向上させるために質問者エージェントの温度を下げることを試みるかもしれないと応じました。また、Neuron Engineerが「Chain of Thought」という考え方を提案し、それを試してみることに興味を持っているとなど、他の参加者も交流を持ちながら解決策を模索しています。

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

# how to overcome a dumb answerer?

**kaoutar** *Sun Jul 14 2024 04:57:40 GMT+0900 (日本標準時)* (6 votes)

this is one example of so many, where the answerer has no clue and misguide the asker agent, sometimes i feel like i am so close, but with one single bad answer, i lose that chance of winning

what are your solutions?



---

 # Comments from other users

> ## Matthew S Farmer
> 
> In your guesser prompt, you may want to give it instructions to make a guess even if it has inconsistent or conflicting information. Ultimately, if the answerer isn't 'truthful' the foundation of the 20 questions falls apart. 
> 
> You could also prompt your questioner in a way that looks for conflicting answers and clarifies confusion by repeating a question in a different way. 
> 
> 
> 
> > ## kaoutarTopic Author
> > 
> > [@matthewsfarmer](https://www.kaggle.com/matthewsfarmer) yeah, i've already tried warning the asker agent about meeting a stupid answerer, it wasn't bad but i noticed that sometimes even when the answerer does fairly well, the asker keeps rephrasing questions which waist time, decreasing the temperature of the asker agent may help, but truly a bad answerer sucks
> > 
> > 
> > 


---

> ## Neuron Engineer
> 
> First of all, thanks for your public notebook! I just started to build my own based on your code and some others.
> 
> About this issue, have you tried "Chain of Thought" on the keyword? 
> 
> (Then putting the thought in the prompt before producing the final answer)
> 
> 
> 
> > ## kaoutarTopic Author
> > 
> > [@ratthachat](https://www.kaggle.com/ratthachat) i'm glad to hear this, thank you, about the Chain of Thoughts, i haven't tried it yet. certainly i will.
> > 
> > 
> > 


---



</div>
<div class="column-right">

# 日本語訳

# どうやっておかしな回答者を克服するか？
**kaoutar** *2024年7月14日 午前4:57:40 (日本標準時)* (6票)
これはたくさんある例の一つで、回答者が全く理解しておらず、質問者エージェントを誤った方向に導いてしまいます。時々、自分は勝利のチャンスにとても近いと感じるのですが、たった一つの悪い回答でそのチャンスを逃してしまいます。あなたの解決策は何ですか？
---
 # 他のユーザーからのコメント
> ## Matthew S Farmer
> 
> あなたの推測者プロンプトでは、一貫性や矛盾する情報があっても推測をするように指示を出すことを考慮してみてください。最終的には、回答者が「真実でない」場合、「20の質問」の基盤が崩れてしまいます。 
> 
> また、質問者が矛盾した回答を探し、異なる質問の仕方で混乱を明らかにするように促すこともできるかもしれません。
>
> > ## kaoutarトピック作成者
> > 
> > [@matthewsfarmer](https://www.kaggle.com/matthewsfarmer) 確かに、私はすでにおかしな回答者に出くわした場合に質問者エージェントに警告を試みました。悪くはなかったですが、時々、回答者がそこそこうまく答えても、質問者が質問を再度言い換え続けるため、時間が無駄になります。質問者エージェントの温度を下げることで改善できるかもしれませんが、本当に悪い回答者は最悪です。
> > 
> > 
---
> ## Neuron Engineer
> 
> まず最初に、あなたの公開ノートブックに感謝します！私はあなたのコードと他のものを基に自分自身のノートブックを作り始めたところです。
> 
> この問題についてですが、「Chain of Thought」をキーワードに試しましたか？
> 
> （次に、最終的な回答を出す前にその考えをプロンプトに入れる）
>
> > ## kaoutarトピック作成者
> > 
> > [@ratthachat](https://www.kaggle.com/ratthachat) このことを聞けてうれしいです。ありがとうございます。「Chain of Thought」についてはまだ試していないので、ぜひやってみます。 
> > 
> >  >


</div>