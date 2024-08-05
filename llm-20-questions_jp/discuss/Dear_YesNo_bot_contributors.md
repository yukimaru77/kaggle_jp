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