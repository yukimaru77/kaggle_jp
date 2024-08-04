# 要約 
このディスカッションは、Kaggleの「LLM 20 Questions」コンペティションにおける最適な戦略について議論しています。

**Khoi Nguyen**は、可能な答えのプールが有限で、正しい答えが完全にランダムであると仮定すると、二分探索が最適な戦略であると主張しています。彼は、回答エージェントが結果を幻覚していないことを確認しながら、ほぼ完璧な分割を実現するためのルールベースのアプローチを提案しています。

**Bovard Doerschuk-Tiberi**は、可能な単語のリストが最終提出期限後に変更されるため、可能な単語のリストをハードコードする戦略は推奨しないと指摘しています。

**chris**は、質問の文字数制限により、Khoi Nguyenが提案したような二分探索は実際には実行できないと指摘しています。しかし、可能な値の固定リストを持ち、何らかの二分探索を行うのは良いアプローチであると考えています。

**Khoi Nguyen**は、プライベートセット内の単語に関する情報が何も与えられていない場合、二分探索法が完璧に機能すれば、検索空間を2^19回まで絞り込むことができると述べています。

**chris**は、英語には約90,000個の名詞があるが、コンペティションでは上位N個の最も一般的なものからだけ引き出す可能性が高いと推測しています。

**G John Rao**は、Khoi Nguyenの提案した戦略は、コンペティションの本質ではないと考えています。彼は、コンペティションでは、演繹的推論、的を絞った質問による効率的な情報収集、ペアエージェント間の連携といった、LLMの重要なスキルが評価されると指摘しています。また、彼は、回答エージェントがホストから提供されたものである場合、すべての質問者LLMにとって公平な条件になると述べています。

**Khoi Nguyen**は、回答エージェントが「特定の人、場所、または物」を考え、質問者からのはい/いいえの質問に答えるため、最初の質問を考案することで、秘密は当初ほど任意ではなくなると述べています。

**結論**

このディスカッションでは、コンペティションにおける最適な戦略について、さまざまな意見が交わされています。二分探索は、可能な答えのプールが有限で、正しい答えが完全にランダムであると仮定すると、有効な戦略ですが、質問の文字数制限や、可能な単語のリストが最終提出期限後に変更される可能性など、いくつかの課題があります。コンペティションでは、LLMの演繹的推論、的を絞った質問による効率的な情報収集、ペアエージェント間の連携といったスキルが評価されるため、参加者はこれらのスキルを最大限に活用する戦略を考案する必要があります。


---
# 最適戦略（LLMは二分探索に勝てるのか？）
**Khoi Nguyen** *2024年5月17日 金曜日 21:29:31 JST* (8 votes)

単なる思考実験です。このゲームの専門家ではありませんが、私が理解したところによると、可能な答えのプールが有限で、正しい答えが完全にランダムであると仮定すると、最適な戦略は、残りのプールを毎回半分に分割しようと試みることです。

さて、答えエージェントが結果を幻覚していないことを確認しながら、ほぼ完璧な分割を実現するには、次のようなルールベースのアプローチが最適です。

- 質問：「答えは<答えプール>に含まれていますか？」答えが「いいえ」の場合、フリースタイルモードに切り替えてLLMの神に祈ります。
答えが「はい」の場合：
- 質問：「答えは<残りの答えプールの半分>に含まれていますか？」
- 「はい」または「いいえ」の答えを得ます。これは、全員が特定の質問構文を使用し、遵守した場合、確実に正しい答えになります。
- 答えが1つになるまで、ステップ2から繰り返します。

keywords.pyファイルを見ると、プライベートテストのために、可能な国、都市、ランドマークの大規模なプールを確実にクロールできます。（ランドマークが曖昧すぎてクロールできない場合、LLMがそれを推測するのに十分な情報を持っているとは思えません）

LLMはこのアプローチに対してどのような利点があるのでしょうか？答えが既知のLLMによって選択された場合、それは私たちが利用できる事前知識ですが、完全にランダムな場合はどうでしょうか？

ジェミニが私に与えてくれた引用：[https://www.cns.nyu.edu/~reuben/blog/20-questions-info-theory/](https://www.cns.nyu.edu/~reuben/blog/20-questions-info-theory/)

注：答えプールがクロール不可能または準無限（すべての可能な英語の単語）であっても、これは依然として強力なアプローチです。単に「その単語の最初の文字は<リスト>に含まれていますか？」のような質問をするだけです。

---
# 他のユーザーからのコメント
> ## Bovard Doerschuk-Tiberi
> 
> 可能な単語のリストは、最終提出期限後に変更されます（つまり、エージェントを新しいリストで更新することはできません）。可能な単語のリストをハードコードする戦略は、強くお勧めしません。
> 
> 最終評価
> 
>   2024年8月13日の提出締め切り時点で、提出物はロックされます。2024年8月13日から8月27日までは、公開されていない新しい単語のセットに対してエピソードを実行し続けます。この期間中、リーダーボードの対象となるのは、アクティブな3つの提出物のみです。この期間の終了時に、リーダーボードが確定します。
> 
> 
> 
---
> ## chris
> 
> 私も似たようなことを考えていました。質問には2000文字しか使用できません（つまり、「答えはリストに含まれていますか？」のような質問は実際にはできません）。しかし、可能な値の固定リストを持ち、何らかの二分探索を行うのは良いアプローチのように思えます。
> 
> 2^20 = 1,048,576
> 
> したがって、すべての分割を正確に50％でヒットした場合、約100万個のものを処理できます。
> 
> ただし、このアプローチを使用する場合は、そのものがリストに含まれていることを願う必要があります！そのため、プライベートセット内の単語の種類に関する情報がもっとなければ、難しいかもしれません。
> 
> 編集：ああ、単語を実際に推測するには、1つの推測を使用する必要があると思いますよね？その場合、最大で2^19 = 524,288個の単語しかありません。
> 
> 
> 
> > ## Khoi Nguyenトピック作成者
> > 
> > プライベートセット内の単語に関する情報が何も与えられていない場合、それを推測することは可能でしょうか？二分探索法があなたが言ったように完璧に機能する場合、検索空間を2^19回まで絞り込むことができます。それ以降は、純粋な運任せです。
> > 
> > 
> > 
> > > ## chris
> > > 
> > > 英語には約90,000個の名詞がありますが、おそらく彼らはその完全なリストを使用するのではなく、上位N個の最も一般的なものからだけ引き出すでしょう。
> > > 
> > > 個々の場所や人々ははるかに多いですが、繰り返しますが、彼らはそれぞれの最も有名な上位N個だけを引き出すと推測します。
> > > 
> > > したがって、この方法で問題を解決するには、カットオフを行う場所が重要です。
> > > 
> > > 
> > > 
> > > ## Khoi Nguyenトピック作成者
> > > 
> > > はい、上位N個の最も人気のあるものは妥当な仮定です。そのため、プライベートセットでは、より早く推測するか、成功する確率を高めるか、どちらかを選択するリスクとリワードの問題になります。そして、ホストに最も近いNを持っているのは誰でしょうか？
> > > 
> > > 
> > > 
---
> ## G John Rao
> 
> 「質問：「答えは<リスト>に含まれていますか？」答えが「いいえ」の場合、フリースタイルモードに切り替えてLLMの神に祈ります。」
> 
> これは、このコンペティションの本質ではないと思います。
> 
> 概要から：
> 
> このコンペティションでは、演繹的推論、的を絞った質問による効率的な情報収集、ペアエージェント間の連携といった、LLMの重要なスキルが評価されます。また、限られた質問回数で創造性と戦略を駆使する必要がある、制約された環境も特徴です。成功すれば、LLMは単に質問に答えるだけでなく、洞察に満ちた質問をし、論理的な推論を行い、可能性を迅速に絞り込む能力を実証することになります。
> 
> keywords.pyには、国、都市、ランドマークの3つのカテゴリが含まれています。
> 
> カテゴリがこれらの3つに限定されているとは思えません。もしそうなら、コンペティションは面白くありません。
> 
> スターターノートブックには、システムプロンプトがあります。
> 
> system_prompt = "あなたは20の質問ゲームをプレイするように設計されたAIアシスタントです。このゲームでは、回答者はキーワードを考え、質問者からのはい/いいえの質問に答えます。キーワードは、特定の人、場所、または物です。"
> 
> 人と場所についてはリストを作成できますが、「物」についてはリストを作成する価値はないと思います。「物」は実際には何でもありえます。名詞、概念、オブジェクト、アイデア、感情、さらには抽象的なエンティティでもありえます。そこが面白いところであり、LLMが活躍するところです。
> 
> 「LLMはこのアプローチに対してどのような利点があるのでしょうか？答えが既知のLLMによって選択された場合、それは私たちが利用できる事前知識ですが、完全にランダムな場合はどうでしょうか？」
> 
> シークレットワードはランダムである必要があると思います。そして、すべての参加者は、それぞれの質問でランダム性を排除するために努力します。
> 
> しかし、私の唯一の疑問は、相手側の回答者が真っ向から否定したり、嘘をついたり、質問者LLMを理解していない場合、または幻覚を始めたらどうなるかということです。
> 
> 回答者LLMがホストから提供されたものである場合、すべての質問者LLMにとって公平な条件になります。そうでない場合、回答者LLMに大きな力が集中します。
> 
> 後でさらに明確になるかもしれません。
> 
> 
> 
> > ## Khoi Nguyenトピック作成者
> > 
> > 「特定の人、場所、または物」は、「任意の物」と同じ意味かもしれません。それを絞り込むには、何らかの事前知識が必要です。
> > 
> > 
> > 
> > > ## G John Rao
> > > 
> > > そして、私たちは最初の質問を考案することでそれを行います。最初の質問に対する答えを得ると、秘密は当初ほど任意ではなくなります。
> > > 
> > > 
> > > 
---

