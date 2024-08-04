# エージェントログは公開すべきか？
**Khoi Nguyen** *2024年5月19日 日曜日 18:39:15 日本標準時* (11票)

これは、（執筆時点での）1位のチームRiggingと33位のPavel Pavlovの最新のゲームのログです。
チーム名は間違っていると思いますが（！？）、それはさておき、ここで起こったことは、チームRigging（たぶん）が二分探索法を使って最終的な推測を導き出したことです。彼らは最初にキーワードがカテゴリのいずれかに含まれているかどうかを尋ね、次に最初の文字がアルファベットの前半にあるかどうかを尋ね、プールが十分に小さくなると、正しい推測が得られるまで、答えがサブリストに含まれているかどうかを尋ね始めました。
これで、そのゲームで勝った質問者の戦略がわかりました。
以前のボットアリーナコンテストでは、ゲームログからボットの動作を逆コンパイルするのははるかに難しかったと思いますが、20の質問では、上記の方法が実証された戦略です。最悪の場合、上位チームからすべての質問をダウンロードして分析し、独自の質問を作成することができます。それは公平ですか？
---
# 他のユーザーからのコメント
> ## Rob Mulla
> 
> これはコンテストの設計者によって意図されていると思います。過去のエージェントベースのコンテスト（[halite](https://www.kaggle.com/competitions/halite)、[connect-x](https://www.kaggle.com/competitions/connectx)）と同様に、ゲームが進行するにつれて各チームの戦略を公開して見ることができます。質問を生成するために使用された正確なロジックとコードはわかりませんが、ソリューションが非常に単純な場合は簡単に推測できます。
> 
> ちなみに、現在のソリューションは、公開/（締め切り前）のリーダーボードで使用されているカテゴリと単語のサブセットを知っているためだけに機能します。このため、最終的に公開リーダーボードは、プライベート/締め切り後のリーダーボードでどのエージェントがうまく機能するかを示す良い指標にはならないと思います。
> 
> 上位チームは、戦略が明らかにならないように、締め切り直前まで最良のエージェントを提出しないことを選択するかもしれません。しかし、結局のところ、公開リーダーボードはほとんど役に立たないので 🤷‍♂️
> 
> 
> 
---
> ## Bovard Doerschuk-Tiberi
> 
> [@suicaokhoailang](https://www.kaggle.com/suicaokhoailang) 提出締め切り後に単語リストを変更し、スコアが安定するまで待ちます。固定された単語リストを前提とするエージェントは、かなりパフォーマンスが低下します。
> 
> 最終評価
> 
>   2024年8月13日の提出締め切り時点で、提出物はロックされます。2024年8月13日から8月27日まで、公開されていない新しい単語のセットに対してエピソードを実行し続けます。この期間中、リーダーボードの対象となるのは、アクティブな3つの提出物のみです。この期間の終了時に、リーダーボードが確定します。
> 
> 
> 
---
> ## Nicholas Broad
> 
> なぜ4つのチーム名が表示されないのですか？各チームに2つずつ、質問者と回答者の名前が表示されるべきではありませんか？
> 
> 編集：もしかしたら、他の2つのチームは一番下にいるのでしょうか？チームと役割が少しわかりにくいですね。
> 
> 
> 
> > ## Bovard Doerschuk-Tiberi
> > 
> > はい、2つのチームは一番下にいます。一番上のチーム名は視覚的なバグです。修正します。
> > 
> > 
> > 
---