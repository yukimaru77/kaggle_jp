# 要約 
ディスカッションでは、参加者alekhが「20の質問」ゲームにおいて、回答者が「はい」や「いいえ」以外の情報を使ってチートする可能性について提起しています。具体的には、回答者がケース（大文字小文字）を利用して最大3ビットの情報をエンコードし、質問者に暗号的なヒントを与えられるのではないかというアイデアです。

これに対して、Bovard Doerschuk-Tiberiは、そのハックは無効化されると指摘し、alekhもそれに同意します。さらに、他のユーザーからは、特定の質問の形式や回答のタイミングを利用して情報をエンコードできる可能性についてのコメントが続きますが、Kris Smithはホストがこれを考慮しているため、機能しないだろうと反論しています。全体として、ケースとタイミングを利用した情報エンコードのアイデアについての議論が展開されていますが、実際の機能性については懐疑的な意見が多いです。

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

# 3-bit cheat

**alekh** *Fri May 24 2024 08:17:25 GMT+0900 (日本標準時)* (0 votes)

Just thought of something. Since the answerer can answer in any case without it being penalized, there is an opportunity to "cheat" by sending up to 3-bits of information in addition to the yes/no information by the answerer.

Maybe someone could find a scheme to exploit this.



---

 # Comments from other users

> ## Bovard Doerschuk-Tiberi
> 
> No matter what case you send yes/no, the result in the replay is always lower case.
> 
> 
> 
> > ## alekhTopic Author
> > 
> > Okay, so the hack is effectively disabled. I guess it's good. But could have been a fun avenue to explore if possible.
> > 
> > 
> > 


---

> ## hengck23
> 
> i wonder can we ask questions like: 
> 
> "does it begin with letter B?"
> 
> "does the word has more than 10 letters?"
> 
> "if it is …, answer yes, if it is …. answer yes slowly, …"
> 
> we need to check for "cheaters" in the server
> 
> 
> 


---

> ## Nicholas Broad
> 
> Can you explain what you mean? The rules say that if the answerer responds with anything other than yes or no, they will automatically lose the match.
> 
> 
> 
> > ## alekhTopic Author
> > 
> > You can answer yes/no in any case. So you can encode information in the case of the letters of yes. I.e. yes, Yes, yEs, yeS, YEs, YeS, yES and YES.
> > 
> > You could make some kind of encoding scheme where you for instance said if the keywords first letter was in the first half of the alphabet, or the last, and so on. Narrowing down the possibilites.
> > 
> > 
> > 
> > > ## alekhTopic Author
> > > 
> > > I could be wrong about the case, and then it wont work. But I thought I've seen both "yes" and "Yes" answers in the replays.
> > > 
> > > 
> > > 
> > > ## Nicholas Broad
> > > 
> > > I don’t think that works but I don’t know for certain
> > > 
> > > 
> > > 


---

> ## Chris Deotte
> 
> We can use time to encode information. Our LLM decides the answer in the first 10 seconds. We then respond at time = 10, 20, 30, 40 seconds. This allows us to encode and pass 2 bits of information to the guesser.
> 
> For example, if the word's first letter is between A-F we respond at time=10, if first letter is between G-L we respond at time=20, if first letter is between M-R we respond at time=30, if first letter is between S-Z we respond at time=40. (And of course our response is "yes" or "no" to the question asked).
> 
> The problem with this approach is that both the questioner and answerer would need to follow this system. Perhaps this is why Kaggle chose to use teams of two instead of allowing one Kaggler to be both the questioner and answerer.
> 
> 
> 


---

> ## Kris Smith
> 
> This won't work as the hosts have thought of this. 
> 
> The answerer output is processed to be all lower case. 
> 
> When you review the logs of games they are showing the raw LLM response before the 20 questions competition codes have processed it. This is why you see different casing.
> 
> If you read the competition code base you can see they are all converted to lower casing here:
> 
> [https://github.com/Kaggle/kaggle-environments/blob/88d915db0a5db35536447a0ba2e2ca0845ef4e25/kaggle_environments/envs/llm_20_questions/llm_20_questions.py#L120](https://github.com/Kaggle/kaggle-environments/blob/88d915db0a5db35536447a0ba2e2ca0845ef4e25/kaggle_environments/envs/llm_20_questions/llm_20_questions.py#L120)
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# 3ビットのチート
**alekh** *2024年5月24日(金) 08:17:25 GMT+0900 (日本標準時)* (0票)
何か思いついたことがあります。回答者はケースを気にせずに回答できるため、回答者は「はい」または「いいえ」の情報に加えて、最大3ビットの情報を送信することで「チート」する機会があるかもしれません。
もしかしたら、これを利用するためのスキームが見つかるかもしれません。
---
# 他のユーザーからのコメント
> ## Bovard Doerschuk-Tiberi
> 
> たとえどんなケースで「はい」や「いいえ」を送信しても、リプレイ内では常に小文字に変換されます。
> 
> > ## alekhトピック作成者
> > 
> > つまり、そのハックは事実上無効化されているということですね。良いことだと思います。しかし、実現可能であれば面白い探求の道となったかもしれません。
> > 
> > 
---
> ## hengck23
> 
> 「それはBの文字で始まるの？」のような質問をしてもいいのか気になります。
> 
> 「その言葉には10文字以上ありますか？」
> 
> 「もしそれが…なら、「はい」と答えて、もしそれが…ならゆっくり「はい」と答えて…」
> 
> サーバーで「チーター」をチェックする必要があります。
> 
> 
---
> ## Nicholas Broad
> 
> あなたの言っていることを説明してもらえますか？ルールには、回答者が「はい」や「いいえ」以外の何かを回答した場合、自動的に試合に負けると書いてあります。
> 
> > ## alekhトピック作成者
> > 
> > 「はい」や「いいえ」をどんなケースで答えても問題ありません。つまり、はいの文字のケースを使って情報をエンコードすることができます。たとえば、yes、Yes、yEs、yeS、YEs、YeS、yES、YESなど。
> > 
> > 何らかのエンコーディングスキームを作成できて、たとえばキーワードの最初の文字がアルファベットの前半か後半かを示すことができたりします。それによって可能性を絞り込むことができます。
> > 
> > 
> > > ## alekhトピック作成者
> > > 
> > > 私がケースについて間違っている可能性があるので、そうなるとそれは機能しません。しかし、私はリプレイで「はい」と「Yes」の両方の回答を見たことがあると思いました。
> > > 
> > > 
> > > > ## Nicholas Broad
> > > > 
> > > それが機能するとは思えませんが、確証はありません。
> > > 
> > > 
---
> ## Chris Deotte
> 
> 時間を使って情報をエンコードすることができます。私たちのLLMは最初の10秒で回答を決定します。その後、10秒、20秒、30秒、40秒の時点で応答します。これにより、推測者に2ビットの情報をエンコードして渡すことが可能になります。
> 
> たとえば、単語の最初の文字がA-Fの間なら10秒で応答し、G-Lの間なら20秒、M-Rの間なら30秒、S-Zの間なら40秒で応答します。（もちろん、私たちの応答は尋ねられた質問に対する「はい」または「いいえ」です）。
> 
> このアプローチには問題があります。質問者と回答者の両方がこのシステムに従う必要がある点です。これは、Kaggleが一人のKagglerが質問者と回答者の両方を担当するのではなく、2チームの形式を採用した理由かもしれません。
> 
> 
---
> ## Kris Smith
> 
> これは機能しないと思います。ホストがこのことを考慮しているからです。
> 
> 回答者の出力はすべて小文字に処理されます。
> 
> ゲームのログを確認すると、彼らはリプレイされる前の生のLLMの応答を示しています。これが、異なるケースを見ている理由です。
> 
> コンペティション用のコードベースを読むと、ここで小文字に変換されているのがわかります：
> [https://github.com/Kaggle/kaggle-environments/blob/88d915db0a5db35536447a0ba2e2ca0845ef4e25/kaggle_environments/envs/llm_20_questions/llm_20_questions.py#L120](https://github.com/Kaggle/kaggle-environments/blob/88d915db0a5db35536447a0ba2e2ca0845ef4e25/kaggle_environments/envs/llm_20_questions/llm_20_questions.py#L120)


</div>