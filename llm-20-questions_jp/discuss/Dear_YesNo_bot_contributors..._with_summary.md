# 要約 
このディスカッションは、Kaggleの「LLM 20 Questions」コンペティションにおける回答者エージェントの質について議論しています。

**主なポイント:**

* **回答者エージェントの質:** 参加者たちは、回答者エージェントが単純なYes/Noボットではなく、より洗練されたものになる必要があると訴えています。Riggingチームが公開したパブリック回答者エージェントを参考に、より優れた回答者エージェントを作成するよう呼びかけています。
* **Llama 3の優位性:** OminousDudeは、Llama 3が回答者エージェントとして最も優れていると主張しています。IF-Evalスコアが高く、プロンプトエンジニアリングにも優れているため、トップ100位にランクインしていない参加者にはLlama 3の使用を推奨しています。
* **間違った質問:** JK-Pieceは、一部の参加者が意図的に間違った質問をするようにエージェントを記述していることを指摘し、これは優れたモデルの性能を低下させる可能性があると懸念しています。

**結論:**

このディスカッションは、回答者エージェントの質がコンペティションの成功に大きく影響することを示しています。参加者たちは、より洗練された回答者エージェントを使用し、間違った質問を避けることで、コンペティションのレベルを向上させることを目指しています。


---
# Yes/No ボットの皆さんへ

**Matthew S Farmer** *2024年7月9日 火曜日 00:18:52 日本標準時* (6票)

回答者エージェントを、少なくともRiggingチームが公開したパブリック回答者エージェント[Riggingチームが公開したパブリック回答者エージェント](https://www.kaggle.com/code/robikscube/phi3-intro-to-rigging-for-llm-20-questions?kernelSessionId=185594599)と同等かそれ以上に優れたものにしてください。単純なYes/Noボットは、堅牢な質問/推測エージェントの性能を低下させています。これはコンペティション全体に大きく役立ちます。もちろん、スクリプトで動作させるためにコードの一部を更新する必要があります。

```python
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
# 他のユーザーからのコメント

> ## OminousDude
> 
> このコンペティションの低レベルなプレイヤーのほとんどは、このようなことをする必要があると思います。しかし、私のテストでは、これはあまり役に立ちません。なぜなら、ほとんどのボットは同じように答えるので、あまり役に立たないからです。もっと重要なのは、優れた回答者ボットを使用することです。トップモデルの選択肢の中で、Llama 3は総合的に最高の回答者だと思います。ですから、トップ100位に常にランクインしていない場合（あるいはランクインしていても）、Llama 3を使用してください。IF-Evalスコアが最も高いため、間違いなく使いやすく、エージェントに非常に厳格なプロンプトエンジニアリングを行うことができます。
> 
> *IF-Evalスコアは、モデルが指示に従う能力を示すものであり、エージェントに非常に厳格なプロンプトエンジニアリングを行うことができます。
> 
> ** [LLM Leaderboard use IF-Eval score](https://huggingface.co/spaces/open-llm-leaderboard/open_llm_leaderboard)
> 
> P.S.: 私は自分のコードを公開することを真剣に検討しています。なぜなら、愚かなボット（あなたたちを傷つけるつもりはありません）のせいで、私は気が狂いそうです。
> 
> 
> 
> > ## Matthew S Farmerトピック作成者
> > 
> > 同意します。素晴らしい指摘です。
> > 
> >  私も以前のコードを公開することを検討していました。 
> > 
> > 
> > 
> > > ## OminousDude
> > > 
> > > 私の考えと同じです。私はこのようなものを見るのにうんざりしています。
> > > 
> > > 質問: "キーワードは物/物体ですか、場所/ロケーションですか？" 回答: "いいえ"
> > > 
> > > 
> > > 
---
> ## JK-Piece
> 
> さらに、一部の人は、間違った質問をするようにエージェントを記述しています。これは、優れたモデルも失敗させてしまいます。
> 
> 
> 
---

