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

# How are we gonna predict probability with no data?

**alekh** *Sun May 12 2024 14:13:23 GMT+0900 (日本標準時)* (0 votes)

How are we gonna predict the probability when we have no training data with probabilities that makes sense. The training data is comprised of 1-hot vectors assigning 100% probability to one of the outcomes. That must clearly be wrong. I don't understand what the training set represents. Does it represent the preference of one particular human? Of a random human? If so, are there multiple rows with the same prompt and responses for different people?



---

 # Comments from other users

> ## alekhTopic Author
> 
> Guess I found the answer:
> 
> "The competition dataset consists of user interactions from the ChatBot Arena. In each user interaction a judge provides one or more prompts to two different large language models, and then indicates which of the models gave the more satisfactory response."
> 
> So i guess we have to like do a softmax on the logits to get probabilities.
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

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



</div>