# 要約 
このコンペティションのディスカッションでは、参加者のMatthew S Farmerが「はい/いいえ」ボットの改善を提案しています。彼は、他の参加者に対し、リギングチームが公開した高性能な回答者エージェントと同等以上に自分たちのエージェントを更新するよう呼びかけています。これにより、シンプルな「はい/いいえ」ボットが本来の質問/推測エージェントのパフォーマンスを妨げる問題を解決できると述べています。彼は具体的なコード例を提供し、改善のための指針を示しています。

他の参加者であるOminousDudeは、良い回答者ボット（特にLlama 3）を使用することの重要性を強調し、これにより競技者の選択肢が向上すると述べています。また、彼は自身のボットの改善が進まないことに不満を抱き、コードを公開する意向を示しています。

さらに、JK-Pieceは一部の参加者が誤った質問をするエージェントを作成しており、それが良いモデルのパフォーマンスを損なう原因になっていると指摘しています。全体として、ディスカッションはエージェントの性能を向上させるための共通の関心事と試行錯誤の場となっています。

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

# Dear Yes/No bot contributors...

**Matthew S Farmer** *Tue Jul 09 2024 00:18:52 GMT+0900 (日本標準時)* (6 votes)

Please update your answerer agent to be at least as good as the public answerer agent [published by the Rigging Team](https://www.kaggle.com/code/robikscube/phi3-intro-to-rigging-for-llm-20-questions?kernelSessionId=185594599). Simple yes/no bots are making robust question/guess agents suffer. It will help the competition tremendously. Of course, you'll need to update some of the code to make it work in your script.

```
async def answer(base: rg.ChatPipeline, observation: Observation) -> t.Literal["yes", "no"]:
    if not observation.keyword:
        print("Keyword wasn't provided to answerer", file=sys.stderr)
        return "yes" # override until keyword bug is fixed.

    last_question = observation.questions[-1]

    try:
        responses = []
        for i in range(5):
            # Loop 5 times and take the most frequent response
            chat = await (
                base.fork(
#                     f"""\
#                         20 Questions game. Answer yes/no for this keyword: [{observation.keyword}]

#                             Question: {last_question}

#                             Rules:
#                             1. Only consider [{observation.keyword}]
#                             2. Check each letter for letter questions
#                             3. Answer only yes or no

#                             Format:
#                             <answer>yes</answer>
#                             OR
#                             <answer>no</answer>

#                             Your answer:
#                         """
                    f"""
                    Keyword: [{observation.keyword}]

                    Q: {last_question}

                    Answer yes or no in Format: <answer>yes</answer> OR <answer>no</answer>
                    """
                )
                .until_parsed_as(Answer, attempt_recovery=True, max_rounds=20)
                .run()
            )
            responses.append(chat.last.parse(Answer).content.strip('*'))

        print(f'Responses are {responses}')
        return pd.Series(responses).value_counts().index[0]
    except rg.error.MessagesExhaustedMaxRoundsError:
        print('%%%%%%%%%%%% Error so answering yes %%%%%%%%%%%% ')
        return 'yes'

```



---

 # Comments from other users

> ## OminousDude
> 
> I also believe that most lower-level players in this competition should do something like this. However, in my testing, this does not help much because most bots will answer the same thing and it is unlikely to help much. More important is to use a good answerer bot and of the top model choices I believe that Llama 3 is the best answerer all around. So please if you are not consistently in the top ~100 (or even if you are) use Llama 3. It is by far the easiest to work with as it has the highest IF-Eval score.
> 
> *IF-Eval score is how well the model is at following instructions and it makes it so that your agent can have very rigorous prompt engineering.
> 
> ** [LLM Leaderboard use IF-Eval score](https://huggingface.co/spaces/open-llm-leaderboard/open_llm_leaderboard)
> 
> P.S.: I am seriously considering releasing my code because the dumb bots (no offense to you guys) are making me lose my mind
> 
> 
> 
> > ## Matthew S FarmerTopic Author
> > 
> > Agreed. Great point.
> > 
> >  I've been considering releasing some earlier code as well. 
> > 
> > 
> > 
> > > ## OminousDude
> > > 
> > > Same as my thinking. I am just so tired of seeing stuff like this
> > > 
> > > Question: "Is the keyword a thing/object or place/location" Answer: "no"
> > > 
> > > 
> > > 


---

> ## JK-Piece
> 
> Moreover, some people write their agents in a way that they as the wrong questions. This makes good models fail as well
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# 親愛なるはい/いいえボットの寄稿者の皆さんへ...
**Matthew S Farmer** *2024年7月9日火曜日 00:18:52 JST* (6票)
あなたの回答者エージェントを、リギングチームが公開した公共の回答者エージェントと同等以上に更新してください。このようなシンプルなはい/いいえボットが、堅牢な質問/推測エージェントのパフォーマンスを妨げています。これを改善することで、コンペティションに大きな助けになります。もちろん、あなたのスクリプトで動作させるためには、いくつかのコードを更新する必要があります。

```python
async def answer(base: rg.ChatPipeline, observation: Observation) -> t.Literal["yes", "no"]:
    if not observation.keyword:
        print("回答者にキーワードが提供されていません", file=sys.stderr)
        return "yes" # キーワードのバグが修正されるまでオーバーライド。
    last_question = observation.questions[-1]
    try:
        responses = []
        for i in range(5):
            # 5回ループして最も頻繁に出現する回答を取得
            chat = await (
                base.fork(
                    f"""
                    キーワード: [{observation.keyword}]
                    質問: {last_question}
                    はいまたはいいえで答えてください (フォーマット: <answer>yes</answer> OR <answer>no</answer>)
                    """
                )
                .until_parsed_as(Answer, attempt_recovery=True, max_rounds=20)
                .run()
            )
            responses.append(chat.last.parse(Answer).content.strip('*'))
        print(f'回答は {responses} です')
        return pd.Series(responses).value_counts().index[0]
    except rg.error.MessagesExhaustedMaxRoundsError:
        print('%%%%%%%%%%%% エラー発生のため、はいと回答します %%%%%%%%%%%% ')
        return 'yes'
```
---
 # 他のユーザーからのコメント
> ## OminousDude
> 
> 私も、競技の多くの下位プレイヤーがこのようなことをすべきだと思います。しかし、私のテストでは、ほとんどのボットが同じことを答えるので、あまり助けにならないことがわかりました。もっと重要なのは、良い回答者ボットを使用することで、トップモデルの選択肢の中で、Llama 3が最も優れた回答者だと考えています。ですので、もしあなたが常にトップ約100に入れない場合（あるいは入っていても）Llama 3を使用してください。最も使いやすく、最高のIF-Evalスコアを持っています。
> 
> *IF-Evalスコアは、モデルが指示に従う能力を示し、エージェントが非常に厳密なプロンプトエンジニアリングを持つことを可能にします。
> 
> ** [LLMリーダーボードはIF-Evalスコアを使用しています](https://huggingface.co/spaces/open-llm-leaderboard/open_llm_leaderboard)
> 
> P.S.: 私は真剣にコードを公開することを検討しています。おバカなボット（あえて言わせてもらいますが）に頭を悩ませられているからです。
> 
> > ## Matthew S Farmer (トピック作成者)
> > 
> > 同意します。素晴らしいポイントです。
> > 
> > 私も以前のコードを公開することを考えています。
> > 
> > > ## OminousDude
> > > 
> > > 私も同じ考えです。本当にこんなものを見続けるのに疲れています。
> > > 
> > > 質問: "キーワードは物体か場所を示していますか" タンムー: "いいえ"
> > > 
> > > 
---
> ## JK-Piece
> 
> さらに、一部の人々はエージェントを、間違った質問をするように作成しています。これが良いモデルの失敗を引き起こすこともあります。


</div>