# 要約 
このKaggleのディスカッションでは、言語モデルにおける回答者の「嘘」についての問題が提起されています。参加者のVolodymyrBilyachatは、回答者が嘘をついてもゲーム内でマイナスの報酬がないため、質問者の合理的な質問に対しても回答者の嘘が影響し、ゲームの進行が困難になる可能性があると指摘しています。

Chris DeotteとNicholas Broadは、質問者と回答者が同じチームに所属し、回答者は「はい」または「いいえ」でしか返答しないことを説明しています。回答者は質問者と同じポイントを得るため、嘘をつくインセンティブはないと述べています。

さらに、Kamal Dasが提案するように、もし回答者が常に「はい」と答える場合、チームに有利になる可能性があり、この状況に対する考察も行われました。

Rob Mullaは、推測の正当性はシステムによってチェックされるべきであり、具体的なコードのスニペットを示しています。最終的に、参加者たちはゲームのルールを理解し、その中での戦略を考え直すことができたようです。

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

# What if model lie on your answer?

**VolodymyrBilyachat** *Sun May 19 2024 08:36:24 GMT+0900 (日本標準時)* (0 votes)

Going through the logs i see that there is not negative reward if answerer lie.

That way the game is a bit odd even if questioner  ask reasonable question lies from answerer can redirect you to wrong path.



---

 # Comments from other users

> ## Chris Deotte
> 
> It is my understanding that the questioner and answerer are teammates. The questioner asks a yes or not question. Then Kaggle responds with yes or no (and Kaggle will not lie). Then your teammate the answerer guesses a possible word. Then Kaggle responds if your are correct or not (and Kaggle will not lie).
> 
> Your team of two bots is competing against another team of two bots to discover the word first.
> 
> UPDATE: Read Nicholas' comment below
> 
> 
> 
> > ## Nicholas Broad
> > 
> > [@cdeotte](https://www.kaggle.com/cdeotte) ,
> > 
> > I believe the questioner also is the guesser. The answerer only responds yes/no.
> > 
> > Here is how I think it goes.
> > 
> > Keyword: France
> > 
> >   Questioner turn 1: Is it a place?
> > 
> >   Answerer turn 1: Yes
> > 
> >   Questioner guess 1: USA
> > 
> >   Kaggle guess checker: Incorrect
> > 
> >   Questioner turn 2: Is it in Europe?
> > 
> >   Answerer turn 2: Yes
> > 
> >   Questioner guess 2: France
> > 
> >   Kaggle guess checker: Correct
> > 
> > 
> > 
> > > ## Chris Deotte
> > > 
> > > Yes, i think you are correct
> > > 
> > > 
> > > 


---

> ## Nicholas Broad
> 
> The answerer wants you to win because they get the same points as the questioner. There is no incentive to produce bad answers
> 
> 
> 
> > ## VolodymyrBilyachatTopic Author
> > 
> > Yes I finally got the idea. Its always 2 teams. If you lie the opponent will get confused and will not get an right answer so you both get lower scores. Thank you
> > 
> > 
> > 
> > ## Kamal Das
> > 
> > what if the reverse, the answerer lies and says OK, right answer to any guess?
> > 
> > that helps the bit pair?
> > 
> > 
> > 
> > > ## Rob Mulla
> > > 
> > > I don't think the agent is responsible for determining if a guess is right, unless I'm missing something, it looks like it's checked using this function from llm_20_questions.py, I'm assuming by the system?
> > > 
> > > ```
> > > def keyword_guessed(guess: str) -> bool:
> > >     def normalize(s: str) -> str:
> > >       t = str.maketrans("", "", string.punctuation)
> > >       return s.lower().replace("the", "").replace(" ", "").translate(t)
> > > 
> > >     if normalize(guess) == normalize(keyword):
> > >       return True
> > >     for s in alts:
> > >       if normalize(s) == normalize(guess):
> > >         return True
> > > 
> > >     return False
> > > 
> > > ```
> > > 
> > > 
> > > 
> > > ## Bovard Doerschuk-Tiberi
> > > 
> > > Yes, the engine code will check the validity of a guesses.
> > > 
> > > 
> > > 


---



</div>
<div class="column-right">

# 日本語訳

# モデルが嘘をついたらどうなるのか？
**VolodymyrBilyachat** *2024年5月19日(日) 08:36:24 GMT+0900 (日本標準時)* (0票)
ログを確認したところ、回答者が嘘をついてもマイナスの報酬が発生しないことがわかりました。そのため、質問者が合理的な質問をしていても、回答者の嘘が正しい方向への導きにくくなってしまい、ゲームが少しおかしくなります。

---
# 他のユーザーのコメント
> ## Chris Deotte
> 
> 私の理解では、質問者と回答者はチームメイトです。質問者が「はい」または「いいえ」の質問をします。その後、Kaggleが「はい」または「いいえ」で返答します（Kaggleは嘘をつきません）。次に、あなたのチームメイトである回答者が可能な単語を推測します。その後、Kaggleがそれが正しいかどうかを返答します（Kaggleは嘘をつきません）。
> 
> 2匹のボットからなるチームが、他の2匹のボットのチームと競って、最初に単語を見つけることになります。
> 
> UPDATE: Nicholasのコメントもご覧ください
> 
> > ## Nicholas Broad
> > 
> > [@cdeotte](https://www.kaggle.com/cdeotte) ,
> > 
> > 質問者も推測を行う役割だと思います。回答者は「はい」または「いいえ」でしか返答しません。
> > 
> > 私の考えは次のようになります。
> > 
> > キーワード: フランス
> > 
> >   質問者ターン1: それは場所ですか？
> > 
> >   回答者ターン1: はい
> > 
> >   質問者推測1: アメリカ
> > 
> >   Kaggle推測チェッカー: 不正解
> > 
> >   質問者ターン2: ヨーロッパにありますか？
> > 
> >   回答者ターン2: はい
> > 
> >   質問者推測2: フランス
> > 
> >   Kaggle推測チェッカー: 正解
> > 
> > > ## Chris Deotte
> > > 
> > > はい、あなたの言う通りだと思います。
> > 
> > > 
> > > 
---
> ## Nicholas Broad
> 
> 回答者はあなたに勝ってほしいと思っています。なぜなら、彼らは質問者と同じポイントを得るからです。悪い答えを出すインセンティブはありません。
> 
> > ## VolodymyrBilyachatトピック作成者
> > 
> > はい、ようやく理解できました。常に2チームがあるのですね。もし嘘をつくと相手チームが混乱し、正しい答えを得られなくなり、両方のチームが低いスコアになるわけですね。ありがとうございます。
> > 
> > > ## Kamal Das
> > > 
> > > 逆に、回答者が嘘をついて、どんな推測にも「はい」と言ったらどうなりますか？
> > >
> > > それはペアにとって助けになりますよね？
> > >
> > > > ## Rob Mulla
> > > > > 私はそのエージェントが推測が正しいかどうかを判断する責任はないと思います。私が理解している限り、これはllm_20_questions.pyのこの関数を使用してチェックされるようです。おそらく、システムによってですか？
> > > > > 
> > > > > ```python
> > > > > def keyword_guessed(guess: str) -> bool:
> > > > >     def normalize(s: str) -> str:
> > > > >       t = str.maketrans("", "", string.punctuation)
> > > > >       return s.lower().replace("the", "").replace(" ", "").translate(t)
> > > > > 
> > > > >     if normalize(guess) == normalize(keyword):
> > > > >       return True
> > > > >     for s in alts:
> > > > >       if normalize(s) == normalize(guess):
> > > > >         return True
> > > > > 
> > > > >     return False
> > > > > ```
> > > > > 
> > > > > 
> > > > > ## Bovard Doerschuk-Tiberi
> > > > > 
> > > > > はい、そのエンジンコードは推測が有効かどうかをチェックします。
> > > > > 
> > > > > 


</div>