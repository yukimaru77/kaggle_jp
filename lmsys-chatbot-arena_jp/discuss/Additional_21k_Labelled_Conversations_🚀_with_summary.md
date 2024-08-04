# 要約 
このディスカッションは、KaggleのLMSYS - Chatbot Arena Human Preference Predictionsコンペティションにおける追加データセットに関するものです。

Abdullah Meda氏は、Chatbot Arenaのデータセットから取得した21,000件のラベル付き会話の追加データセットを公開しました。このデータセットは、コンペティションの元のデータセットとはフォーマットが異なるため、処理スクリプトも提供されています。

しかし、他のユーザーからのコメントでは、この追加データセットには元のデータセットとの重複が含まれていることが指摘されました。特に、元のデータセットの約3分の1が重複している可能性があり、追加データセット内にも類似したデータが存在する可能性があります。

Abdullah Meda氏は、重複を削除するためにプロンプト列を基準として使用し、データセットを更新しました。また、タイの処理に関する問題も修正しました。

Rich Olson氏は、この追加データセットをトレーニングに使用した結果、リーダーボードスコアは改善されなかったと報告しました。Ivan Vybornov氏は、追加データセットの大部分は、元のデータセットに存在しないモデルから来ており、tf-idfアプローチには適していないと指摘しました。

一方、xiaotingting氏は、追加データセットを使用することで結果が大幅に改善されたと報告しました。しかし、他のユーザーは、クロスバリデーションスコアとリーダーボードスコアの両方が改善されたのか、それとも一方のみが改善されたのかを質問しています。

eli plutchok氏は、追加データセットを使用することで、意図せずテストデータに対するモデルの予測が悪化するのではないかと懸念を表明しました。彼は、追加データセットを使用した場合の結果を報告することを約束しました。

このディスカッションは、追加データセットがコンペティションのパフォーマンスにどのような影響を与えるのか、そしてどのように使用するのが最適なのかについて、活発な議論が行われていることを示しています。


---
# 追加の21,000件のラベル付き会話 🚀
**Abdullah Meda** *2024年5月8日 水曜日 01:17:13 GMT+0900 (日本標準時)* (75票)

このデータセットは、[https://huggingface.co/datasets/lmsys/chatbot_arena_conversations](https://huggingface.co/datasets/lmsys/chatbot_arena_conversations) の著者自身から提供されたものです。
フォーマットは、このコンペティションで使用されているものとはかなり異なっていました。私はそれを類似のフォーマットになるように処理しました。以下に示します。
- データセット: [kaggle.com/datasets/abdullahmeda/lmsys-additional-33k-labelled-conversations](https://www.kaggle.com/datasets/abdullahmeda/lmsys-additional-33k-labelled-conversations)
- 処理スクリプト: [kaggle.com/code/abdullahmeda/33k-lmsys-chatbot-arena-conversations/](https://www.kaggle.com/code/abdullahmeda/33k-lmsys-chatbot-arena-conversations/)
[データセット](https://www.kaggle.com/datasets/abdullahmeda/lmsys-additional-33k-labelled-conversations) に対する賛成票をいただけると幸いです。ありがとうございました！🙏
明日時間があれば、データセット間に重複がないか確認します。楽しいコーディングを！
**更新:** プロンプト列を重複排除基準として使用すると、サンプル数は約21,000件になります。データセットとスクリプトが更新されました。
---
# 他のユーザーからのコメント
> ## eli plutchok
> 
> [@abdullahmeda](https://www.kaggle.com/abdullahmeda) さん、このトレーニングデータを追加してテストしてみたのですが、なぜか提出スコアが大幅に悪化してしまいました。
> 
> 
> 
---
> ## eli plutchok
> 
> ああ、メインのデータセットにすでに多くの行が含まれていることに気づきました。重複をすべて削除した、新しいクリーンなバージョンを作成できるかもしれません。割合はわかりません。
> 
> 
> 
> > ## eli plutchok
> > 
> > メインのトレーニングセットから約3分の1が重複していると思いますが、データセット内にも多くの重複があり、正確な重複ではないものの非常に類似したものが追加で存在すると思います。
> > 
> > 
> > 
> > > ## Abdullah Medaトピック作成者
> > > 
> > > [@eliplutchok](https://www.kaggle.com/eliplutchok) おっしゃる通りかもしれません。今のところ、類似したプロンプトを持つ行はすべて削除しました。複数の列をサブセットとして使用して行を削除することもできますが、複数の列を使用すると削除される行が少なくなることに気づきました。プロンプトのみを重複排除基準として使用すると、数はわずか21,000件の新しいサンプルにまで減少します。スクリプトとデータセットを更新して反映しました。投稿を少し修正します。
> > > 
> > > ```
> > > superset = pd.concat([external_data, train]).reset_index(drop=True)
> > > external_data_deduplicated = superset.drop_duplicates(subset=['prompt'], keep='last')
> > > external_data_deduplicated = external_data_deduplicated[external_data_deduplicated.index.isin(external_data.index)]
> > > 
> > > len(external_data_deduplicated)
> > > >>> 21187
> > > 
> > > ```
> > > 
> > > 
> > > 
> > > ## eli plutchok
> > > 
> > > ちなみに、別のことに気づきました。 "tie (both bad)" が勝者だった行は、空白のままになっていますが、これらはすべてタイとしてカウントされるべきです。そうしないと、メインのデータセットではタイが30%であるのに対し、タイが10%しか残らなくなってしまいます。
> > > 
> > > 
> > > 
> > > ## Abdullah Medaトピック作成者
> > > 
> > > [@eliplutchok](https://www.kaggle.com/eliplutchok) ご指摘ありがとうございます。修正しました！
> > > 
> > > ```
> > > >>> external_data[['winner_model_a', 'winner_model_b', 'winner_tie']].sum(axis=1).all()
> > > True
> > > 
> > > ```
> > > 
> > > 
> > > 
---
> ## Rich Olson
> 
> 私は、重複削除されたバージョンをトレーニングに追加した、私の1.011 LBノートブックのバージョンを提出しました。
> 
> [https://www.kaggle.com/code/richolson/deberta-tf-idf-word2vec-length](https://www.kaggle.com/code/richolson/deberta-tf-idf-word2vec-length)
> 
> 結果を投稿します。
> 
> 
> 
> > ## Rich Olson
> > 
> > LBで同じ1.011を取得しました（上記のノートブックのバージョン6を参照）。
> > 
> > "[ultrafeedback](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/499756)" データセットから50,000件のアイテムを使用しても同じ結果でした。
> > 
> > これは、データがおそらく良い（少なくとも悪いわけではない）ことを示唆していると思います。私のノートブックは、追加のデータから恩恵を受けることができないだけです。
> > 
> > 
> > 
> > ## Ivan Vybornov
> > 
> > データの大部分は、実際のトレーニングセットに存在しないモデルから来ています。これは、tf-idfアプローチを補完するとは思えません。
> > 
> > 
> > 
---
> ## xiaotingting
> 
> このデータセットを追加した後、結果は大幅に改善されました。追加のデータセットの使用は確かに役立ちます。
> 
> 
> 
> > ## Erik
> > 
> > こんにちは、CVとLBの両方が同時に改善されましたか？
> > 
> > 
> > 
> > > ## KeShuang Liu
> > > 
> > > データセットを使用した後、なぜCVではパフォーマンスが向上したが、LBではパフォーマンスが低下したのでしょうか？
> > > 
> > > 
> > > 
---
> ## eli plutchok
> 
> 提出で試してみましたか？外部データを使用すると、意図せずテストデータに対するモデルの予測が悪化するのではないかと心配しています。
> 
> 
> 
> > ## Sparsh Tewatia
> > 
> > もし試したら、結果をここに更新してください。
> > 
> > 
> > 
> > > ## eli plutchok
> > > 
> > > 分かりました。明日（私にとってはニューヨークです）試して、お知らせします。
> > > 
> > > 
> > > 
> > > ## go
> > > 
> > > データを追加する前は、CVは1.01でした。
> > > 
> > > データを追加した後は、CVは1.03…
> > > 
> > > しかし、このバージョンは提出していません。
> > > 
> > > 
> > > 
---


