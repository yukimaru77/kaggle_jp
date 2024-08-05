# 要約 
コンペのディスカッションは、ポリシーベースの強化学習（RL）を用いて「20の質問ゲーム」をプレイする手法に焦点を当てています。著者らは、質問者エージェントがユーザーとのインタラクションを通じて質問選択の最適ポリシーを学ぶ方法を提案しており、報酬ネットワークを活用して情報に富んだ報酬の推定を行います。このアプローチはノイズのある回答に対して頑健で、既存の知識ベースに依存しないため、ゲームプレイの効率を向上させます。

ディスカッションでは、ゲーム内の質問選択プロセスをマルコフ決定過程（MDP）として定式化し、質問者エージェントが全オブジェクトに対する確率分布を維持しながら信頼度を更新する様子が詳述されています。また、RewardNetを使用して、即時報酬を推定し、長期的なリターンを計算することでモデルのトレーニングを支援します。

他のユーザーは、強化学習に関する関心を示し、エージェントが質問数を管理するのに苦労している体験を共有しました。また、ディスカッションの中で、著者のアルゴリズム設計の難しさが言及され、初心者にとっての挑戦が理解されました。

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

# Q20 Game with Reinforcement Learning. Markov Decision Process (MDP).

**Marília Prata** *Thu May 16 2024 11:02:24 GMT+0900 (日本標準時)* (23 votes)

# Q20 Game with Reinforcement Learning

Playing 20 Question Game with Policy-Based Reinforcement Learning

Authors: Huang Hu1, Xianchao Wu, Bingfeng Luo, Chongyang Tao,Can Xu, Wei Wu and Zhan Chen

"In this paper,the authors proposed a novel policy-based Reinforce-ment Learning (RL) method, which enables the questioner agent to learn the optimal policy of question selection through continuous interactions with users. To facilitate training,they also proposed to use a reward network to estimate the more informative reward. Compared to previous methods, their RL method is robust to noisy answers and does not rely onthe Knowledge Base of objects. Experimental results show that our RL method clearly outperforms an entropy-based engineering system and has competitive performance in a noisy-free simulation environment."

"It is not easy to design the algorithm to construct a Q20 game system. Although the decision tree based method seems like a natural fit to the Q20 game, it typically require a well defined Knowledge Base (KB) that contains enough information about each object, which is usually not available in practice. It was used a object-question relevance table as the pivot for question and object selection, which does not depend on an existing KB (Knowledge Base). Further it was improved the relevance table with a lot of engineering tricks. Since these table-based methods greedily select questions and the model parameters are only updated by rules, their models are very sensitive to noisy answers from users, which is common in the real-world Q20 games. It was utilized a value-based Reinforcement Learning (RL) model to improve the generalization ability but still relies on the existing KB.

# Markov Decision Process (MDP)

"In this paper, the authors formulated the process of question selection in the game as a Markov Decision Process (MDP), and further propose a novel policy-based RL framework to learn the optimal policy of question selection in the Q20 game. Their questioner agent maintains a probability distribution over all objects to model the confidence of the target object, and updates the confidence based on answers from the user."

# RewardNet

"At each time-step the agent uses a policy network to take in the confidence vector and output a question distribution for selecting the next question. To solve the problem that there is no immediate reward for each selected question, the authors also proposed to employ a RewardNet to estimate the appropriate immediate reward at each time-step, which is further used to calculate the long-term return to train their RL model."

"Their RL (Reinforcement Learning) framework makes the agent robust to noisy answers since the model parameters are fully learnable and the question distribution provides us with a principled way to sample questions, which enables the agent to jump out of the local optimum caused by incorrect answers and also introduces more randomness during training to improve the model generalization ability. Furthermore, the ability to sample questions, compared to greedy selection, also improves the diversity of the questions asked by their agent, which is crucial for user experience."

[https://www.researchgate.net/publication/327199595_Playing_20_Question_Game_with_Policy-Based_Reinforcement_Learning](https://www.researchgate.net/publication/327199595_Playing_20_Question_Game_with_Policy-Based_Reinforcement_Learning)



---

 # Comments from other users

> ## JDau
> 
> Hey that's pretty interesting.  I've bookmarked this for future reference as I'm quite interested in the reinforcement aspect.  
> 
> Just for fun, I decided to give everyone's favourite LLM a go with this game.  I wanted to see if Chats (via co-pilot) could figure out my choice of John Maynard Keynes.   Chats spent a lot of questions trying to figure out a category (but economics wasn't a standard offering).  Here's an example exchange:
> 
> Copilot
> 
>   Let’s narrow it down. Is this historical figure known for their scientific discoveries, or are they more famous for their political or social impact? 🤔
> 
>   You
> 
>   There is not a clear answer to that. They were involved in all 3, particularly if you take a loose view on the phrase 'scientific discoveries'
> 
> Despite the hint (regular hints) that the famous person was involved in what some would call a social science, it never honed in on the category.  I did appreciate the emoji though…
> 
> It was also obvious that Chat's was struggling with keeping track of the question number.  (Perhaps it's human after all?)
> 
> Question 12: Did this person have a significant impact in the field of art, music, or literature? 🤔
> 
>   You
> 
>   They wrote books. But I don't think this person would be regarded as having a significant impact in the field of literature.
> 
>   Copilot
> 
>   Thank you for the additional context! It’s intriguing that this historical figure wrote books, although their impact in the field of literature may not be considered significant. Let’s continue our quest:
> 
>   Question 12: Did this person have a significant impact in the field of art, music, or literature? 🤔
> 
>   You
> 
>   You're up to question 13 now.
> 
>   Copilot
> 
>   My apologies for the oversight! Let’s continue with the next question:
> 
> 
> 
> > ## Marília PrataTopic Author
> > 
> > Very nice examples JDaustralia.  
> > 
> > There are great competitions on Kaggle with Agents and reinforcement learning, such as:
> > 
> > [Connect X](https://www.kaggle.com/competitions/connectx)
> > 
> > [Lux AI Season 2](https://www.kaggle.com/competitions/lux-ai-season-2/overview)
> > 
> > [Kore 2022](https://www.kaggle.com/competitions/kore-2022/overview) 
> > 
> > [Halite by Two Sigma](https://www.kaggle.com/competitions/halite)
> > 
> > 
> > 


---

> ## Edwin Samuel Giftson
> 
> This way of playing the 20 Questions game is really cool! They're using something called reinforcement learning to make a smart question-asking agent. It learns which questions to ask by talking with people. They also have this thing called RewardNet that helps figure out if the answers are good or not. It's a big step forward compared to how things used to be done, which often had problems with bad answers and needing a lot of info already set up
> 
> 
> 
> > ## Marília PrataTopic Author
> > 
> > The fun fact is that the authors wrote that "It's not easy to design the algorithm to construct a Q20 game system."
> > 
> > If it's not easy for them, imagine for me cause I'm a beginner : )  Thank you Giftson. 
> > 
> > 
> > 


---



</div>
<div class="column-right">

# 日本語訳

# Q20ゲームと強化学習。マルコフ決定過程（MDP）。
**マリリア・プラタ** *2024年5月16日 木曜日 11:02:24 GMT+0900 (日本標準時)* (23票)
# Q20ゲームと強化学習
ポリシーベースの強化学習を用いた「20の質問ゲーム」のプレイ
著者: 黄虎1、呉賢超、羅昇峰、陶崇陽、徐灿、伍韋、陳展
「本論文では、著者らは新しいポリシーベースの強化学習（RL）手法を提案しました。この手法により、質問者エージェントはユーザーとの継続的なインタラクションを通じて質問選択の最適ポリシーを学ぶことができます。トレーニングを容易にするために、より情報に富んだ報酬を推定するための報酬ネットワークの使用も提案されています。従来の手法と比較して、彼らのRL手法はノイズのある回答に対して頑健であり、オブジェクトの知識ベースに依存しません。実験結果は、彼らのRL手法がエントロピーに基づくエンジニアリングシステムを明確に上回り、ノイズのないシミュレーション環境では競争力のある性能を持つことを示しています。」
「Q20ゲームシステムを構築するためのアルゴリズムを設計するのは簡単ではありません。決定木ベースの方法はQ20ゲームに自然に適しているように見えますが、通常、各オブジェクトに関する十分な情報を含む明確に定義された知識ベース（KB）が必要であり、これは実際には一般的に入手できません。既存のKB（知識ベース）に依存しない質問とオブジェクトの選択のための参照として、オブジェクト-質問関連テーブルを使用しました。さらに、この関連テーブルは多くのエンジニアリングトリックで改善されました。これらのテーブルベースの手法は貪欲に質問を選択するため、モデルパラメータはルールによってのみ更新されるため、ユーザーからのノイズのある回答に非常に敏感です。これは現実のQ20ゲームでは一般的です。一般化能力を向上させるために、値ベースの強化学習（RL）モデルが利用されましたが、既存のKBにまだ依存しています。」

# マルコフ決定過程（MDP）
「本論文では著者らは、ゲームにおける質問選択のプロセスをマルコフ決定過程（MDP）として定式化し、さらにQ20ゲームにおける質問選択の最適ポリシーを学ぶための新しいポリシーベースのRLフレームワークを提案しました。彼らの質問者エージェントは、ターゲットオブジェクトの信頼度をモデル化するためにすべてのオブジェクトに対する確率分布を維持し、ユーザーからの回答に基づいてその信頼度を更新します。」

# RewardNet
「各タイムステップで、エージェントはポリシーネットワークを使用して信頼度ベクターを受け取り、次の質問を選択するための質問分布を出力します。選択した質問ごとに即時の報酬がないという問題を解決するために、著者らは各タイムステップで適切な即時報酬を推定するためにRewardNetを使用することを提案しました。この報酬は、長期的なリターンを計算するためにRLモデルのトレーニングに利用されます。」
「彼らのRL（強化学習）フレームワークは、エージェントをノイズのある回答に対して頑健にします。なぜなら、モデルパラメータは完全に学習可能であり、質問分布は質問をサンプリングするための原則的な方法を提供し、エージェントが不正確な回答によって引き起こされる局所最適から抜け出すことを可能にし、またトレーニング中により多くのランダム性を導入してモデルの一般化能力を向上させます。さらに、貪欲に選択することと比較して、質問をサンプリングする能力は、エージェントが尋ねる質問の多様性を改善し、ユーザー体験にとって非常に重要です。」
[https://www.researchgate.net/publication/327199595_Playing_20_Question_Game_with_Policy-Based_Reinforcement_Learning](https://www.researchgate.net/publication/327199595_Playing_20_Question_Game_with_Policy-Based_Reinforcement_Learning)

---
 # 他のユーザーからのコメント
> ## JDau
> 
> 面白いですね。強化学習の側面に興味があるので、今後の参考にこのリソースをブックマークしました。  
> 
> お遊びで、みんなのお気に入りのLLMを使ってこのゲームを試してみました。私の選んだジョン・メイナード・ケインズを特定できるか見たかったのです。チャットはそのカテゴリを特定するのに多くの質問を使っていましたが（経済学は標準の選択肢ではありませんでした）。以下は一例のやり取りです：
> 
> Copilot
> 
>   絞り込んでみましょう。この歴史的人物は科学的発見で知られていますか、それとも政治的または社会的な影響で有名ですか？🤔
> 
>   あなた
> 
>   明確な答えはありません。特に「科学的発見」というフレーズを広義に解釈すれば、彼らは3つすべてに関与していました。
> 
> ヒント（定期的なヒント）があったにも関わらず、有名な人物が一部の人が言うところの社会科学に関与していることがありましたが、それはカテゴリに絞り込まれることはありませんでした。絵文字は評価しましたが…
> 
> チャットは質問数を管理するのに苦労していることも明らかでした。（もしかしたら人間らしいですね？）
> 
> 質問12：この人は芸術、音楽、または文学の分野に重要な影響を及ぼしましたか？🤔
> 
>   あなた
> 
>   彼は本を書きました。しかし、この人物が文学の分野に重要な影響を及ぼしたとは思いません。
> 
>   Copilot
> 
>   追加のコンテキストをありがとうございます！この歴史的人物が本を書いたのは興味深いことですが、その文学の分野での影響は重要と見なされないかもしれません。それでは、探求を続けましょう：
> 
>   質問12：この人は芸術、音楽、または文学の分野に重要な影響を及ぼしましたか？🤔
> 
>   あなた
> 
>   あなたはもう質問13に到達しています。
> 
>   Copilot
> 
>   見落としについてお詫びします！次の質問を続けましょう：
> 
> > ## マリリア・プラタ トピック作成者
> > 
> > 素晴らしい例ですね、JDaustralia。  
> > 
> > Kaggleにはエージェントや強化学習に関する素晴らしいコンペもありますのでご紹介します：
> > 
> > [Connect X](https://www.kaggle.com/competitions/connectx)
> > 
> > [Lux AI Season 2](https://www.kaggle.com/competitions/lux-ai-season-2/overview)
> > 
> > [Kore 2022](https://www.kaggle.com/competitions/kore-2022/overview) 
> > 
> > [Halite by Two Sigma](https://www.kaggle.com/competitions/halite)
> > 
> > 
---
> ## エドウィン・サミュエル・ギフトソン
> 
> この20の質問ゲームのプレイ方法は本当にクールですね！彼らは強化学習と呼ばれるものを使って賢い質問をするエージェントを作っています。エージェントは人との対話を通じて、どの質問をするかを学びます。また、回答が良いかどうかを判断するのを助けるRewardNetというものもあります。従来の方法と比較して、大きな進展です。従来の方法は悪い回答や十分に設定された情報に依存することが多かったです。
> 
> 
> > ## マリリア・プラタ トピック作成者
> > 
> > 面白いことに、著者は「Q20ゲームシステムを構築するアルゴリズムを設計するのは簡単ではない」と書いています。
> > 
> > 彼らにとって簡単でないなら、私のような初心者にはいかに難しいか想像できます : ) ありがとう、ギフトソン！ 
> > 
> > 
---


</div>