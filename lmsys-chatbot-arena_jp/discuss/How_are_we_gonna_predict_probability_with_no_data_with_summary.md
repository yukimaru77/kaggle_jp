# 要約 
このディスカッションは、LMSYS - Chatbot Arena 人間による好み予測チャレンジの参加者が、コンペティションデータセットの解釈について抱えていた疑問とその解決について議論しています。

**疑問点:**

* トレーニングデータは1-hotベクトルで構成されており、ある結果に100%の確率を割り当てている。
* このデータセットが何を表しているのか不明。特定の1人の人間の好みなのか、それともランダムな人間の好みなのか。
* 同じプロンプトと応答に対して、異なる人々のデータが複数行存在するのか。

**解決策:**

* データセットはChatBot Arenaからのユーザーのやり取りで構成されている。
* 各ユーザーのやり取りにおいて、審査員は2つの異なる大規模言語モデルに1つ以上のプロンプトを提供し、どちらのモデルがより満足のいく応答を与えたかを指示する。
* したがって、確率を得るためにロジットにソフトマックスを適用する必要がある。

つまり、このコンペティションでは、ユーザーの好みを予測するために、ロジスティック回帰などの分類モデルを使用し、ソフトマックス関数を用いて確率を算出することが適切であると結論付けられています。


---
# どうやって確率を予測するのか？データがないのに！
**alekh** *2024年5月12日(日) 14:13:23 JST* (0票)

確率を予測するのに、意味のある確率を持つトレーニングデータがないのはどうすればいいのでしょうか？トレーニングデータは、ある結果に100%の確率を割り当てる1-hotベクトルで構成されています。これは明らかに間違っているはずです。トレーニングセットが何を表しているのか理解できません。それは特定の1人の人間の好みを表しているのでしょうか？それともランダムな人間の好みを表しているのでしょうか？もしそうなら、同じプロンプトと応答に対して、異なる人々のデータが複数行存在するのでしょうか？
---
# 他のユーザーからのコメント
> ## alekhトピック作成者
> 
> 答えが見つかったようです。
> 
> 「コンペティションのデータセットは、ChatBot Arenaからのユーザーのやり取りで構成されています。各ユーザーのやり取りにおいて、審査員は2つの異なる大規模言語モデルに1つ以上のプロンプトを提供し、その後、どちらのモデルがより満足のいく応答を与えたかを指示します。」
> 
> つまり、確率を得るためにロジットにソフトマックスを適用する必要があるということですね。
> 
> 
> 
--- 
