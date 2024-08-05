# 要約 
このKaggleコンペティションのディスカッションは、DeBERTaモデルのトレーニングにおける不安定性について議論しています。トピック作成者のValentin Wernerは、以前はDeBERTa-3-largeモデルで良い結果を得ていましたが、最近では同じパラメータを使用してもモデルが学習に失敗するようになったと報告しています。

他のユーザーからのコメントでは、いくつかの潜在的な原因と解決策が提示されています。

* **James Day**は、学習率スケジュールの設定ミスが原因である可能性があると指摘し、自身のベースラインアプローチではDeBERTa-v3-largeモデルを使用して0.997のスコアを達成したと述べています。彼は、会話の両側それぞれについて埋め込みを生成し、それらを小さな全結合分類器に渡す方法を採用しました。
* **Takamichi Toda**は、ラベルスムージング、タスク内事前トレーニング、ドロップアウトオフ、対抗学習などのテクニックが効果的であったと共有しています。彼は、DeBERTa xsmallモデルで実験を行っており、ドロップアウトをオフにすることで精度が向上したことに驚いています。

Valentin Wernerは、AWP（対抗学習）を使用するとモデルがすぐに学習を停止してしまうという問題を報告しています。Takamichi Todaは、モデルサイズやAWP学習率が原因である可能性があると示唆しています。

ディスカッションの最後では、Valentin Wernerは、DeBERTa-3-largeモデルのトレーニング結果が実行間で大きく異なることを報告しています。James Dayは、トレーニングパイプラインに問題がある可能性があると指摘し、自身のCVとLBのスコアは非常に高い相関関係があることを強調しています。

このディスカッションは、DeBERTaモデルのトレーニングにおける不安定性という共通の問題を浮き彫りにしています。ユーザーは、学習率スケジュール、データの前処理、正則化テクニック、対抗学習などの要因が安定性に影響を与える可能性があると指摘しています。さらに、CVとLBのスコア間のギャップは、データ分割方法やモデルの過剰適合に関連している可能性があります。


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

# Unstable Deberta Training Results

**Valentin Werner** *Sat Jun 15 2024 18:19:14 GMT+0900 (日本標準時)* (29 votes)

I spent a lot of time trying the boosting approach without any tf-idf or transformer embeddings and am now moving back to training transformers. Now, early in the competition I trained a deberta-3-large model, which did not break any records, but at least learned something (like 1.039). However, all my current attempts are failing to learn yet again - even with the same parameters as the last time I trained.

Have you experienced similar results where doing rather small changes (e.g., the structure of the input string) results in the model suddenly being unable to learn at all? What are the "best practices" you learned for training deberta / llama & co during this competition (if you dont mind sharing).

Cheers!



---

 # Comments from other users

> ## James Day
> 
> I got 0.997 with deberta-v3-large by having it produce an embedding for each side of the conversation separately, then passing those embeddings to a small 2 layer fully connected classifier. That was my first baseline approach in this competition. It certainly isn't the most accurate, but worked better than what you're describing.
> 
> I haven't really had any stability problems in this competition, but most stability problems where a model fails to converge to anything better than random guessing that I've encountered in the past have stemmed from a misconfigured learning rate schedule, so you might want to try tinkering with that if you haven't already.
> 
> 
> 
> > ## Valentin WernerTopic Author
> > 
> > Welcome back to the competition, James - I remember you die some impressive training in DAIGT too. Looking forward to See you on top of the lb again!
> > 
> > Do I understand correctly that you are only using the embeddings or did you combine two deberta Models and add layers on top of it?
> > 
> > 
> > 
> > > ## James Day
> > > 
> > > My 0.997 baseline used the same deberta backbone to process each "side" of the conversation (where each side is essentially a concatenation of the initial prompt, model X's first response, the follow up prompt (if available), model X's second response… up to a 768 token max context length). The embeddings from the CLS token on each side (A & B) were then concatenated and fed to a small classification head. In other words, there was a single debeta model with a couple extra layers stacked on top. The whole thing was trainable - I did not use a frozen pretrained backbone to compute the embeddings.
> > > 
> > > The approach described above is easily beaten by scaling up to using Llama 3 8B as the foundation model.
> > > 
> > > 
> > > 


---

> ## Takamichi Toda
> 
> I am sharing what has been effective in my experiments. 
> 
> Now difficulty in securing computational resources, I am conducting experiments with DeBERTa xsmall. Please note that you may not achieve the same results due to environmental differences.
> 
> ### Label Smoothing
> 
> I am using CrossEntropyLoss and setting the label_smoothing parameter to 0.2. The reason is that competition data can be labelled differently for the same data, and I thought it could be said to be a kind of noisy data.
> 
> ### Within-task Pre-training
> 
> I train the Masked Language Model using the competition data and use these weights for fine-tuning.
> 
> ### Dropout Off
> 
> I adjusted the Dropout Ratio, but 0 was the most effective. 
> 
> Although I have heard that Dropout should be off for regression problems, this is not. I do not understand why the absence of Dropout yielded better accuracy.🧐
> 
> ### Adversarial Training
> 
> I tried AWP, and it was effective. I also plan to test other methods such as FGM.
> 
> 
> 
> > ## Valentin WernerTopic Author
> > 
> > have you had stable results between XSmall and Large? for me, the smaller models are not converging, so I only trained Large. This obviously has terrible Iteration Speed for the experiments.
> > 
> > Thanks for sharing!
> > 
> > 
> > 
> > ## Valentin WernerTopic Author
> > 
> > Once I tried training with AWP the model instantly learned nothing again - its quite interesting
> > 
> > 
> > 
> > > ## Takamichi Toda
> > > 
> > > Hmm, I wonder why.
> > > 
> > > Which model are you using? I am still using DeBERTa xsmall, so it might be due to the difference in model size.
> > > 
> > > How about applying a small value to the AWP Learning Rate?
> > > 
> > > In my case, it's 1e-4. By the way, the overall learning rate is 2e-5.
> > > 
> > > 
> > > 
> > > ## Valentin WernerTopic Author
> > > 
> > > I will have to look further into AWP, I guess. I have not used it before and took an existing kaggle notebook as basis. 
> > > 
> > > I had no success with any small model and only ever got close to 1.00 with deberta-3-large. I am also using effective batch size of 8 (2 x 4) and a lr of about 8e-6 - so that is muuuuch lower than yours… Time to do some more experiments :)
> > > 
> > > 
> > > 


---

> ## Valentin WernerTopic Author
> 
> I trained a deberta-3-large model yesterday and achieved 1.005 - same training params today get me about 1.07. It seems very unreliable to me - I have yet to schiebe good scores with lora
> 
> 
> 
> > ## James Day
> > 
> > Weird. For me the random variation from run to run is < 0.01. CV & LB are very well correlated too (pearson r = 0.97).
> > 
> > It sounds to me like something is broken or misconfigured in your training pipeline. It isn't a problem inherent to the data itself.
> > 
> > 
> > 
> > > ## yechenzhi1
> > > 
> > > Hi, may I ask how do you get your CV split? I randomly split 10% from the training dataset, and the score from CV and LB are very different, my CV score is 0.889, and LB is 0.922. 
> > > 
> > > 
> > > 


---



</div>
<div class="column-right">

# 日本語訳

# DeBERTaトレーニング結果の不安定性

**Valentin Werner** *2024年6月15日土曜日 18:19:14 GMT+0900 (日本標準時)* (29票)

ブースト手法をTF-IDFやトランスフォーマー埋め込みなしで試すのに多くの時間を費やしたので、トランスフォーマーのトレーニングに戻ってきました。コンペティションの初期段階では、DeBERTa-3-largeモデルをトレーニングしましたが、記録を破ることはありませんでしたが、少なくとも何かを学習しました（1.039など）。しかし、現在の試みはすべて再び学習に失敗しています。前回のトレーニングと同じパラメータを使用してもです。

入力文字列の構造など、ごくわずかな変更を加えただけで、モデルが突然まったく学習できなくなるような経験はありますか？このコンペティションでDeBERTaやLLaMAなどのトレーニングについて学んだ「ベストプラクティス」があれば教えてください（共有して差し支えなければ）。

よろしくお願いします！
---
# 他のユーザーからのコメント

> ## James Day
> 
> DeBERTa-v3-largeを使って、会話の両側それぞれについて埋め込みを生成し、それらの埋め込みを小さな2層の全結合分類器に渡すことで、0.997を達成しました。これは、このコンペティションでの最初のベースラインアプローチでした。最も正確な方法ではありませんが、あなたが説明しているものよりもうまく機能しました。
> 
> このコンペティションでは、安定性の問題に遭遇したことはありませんが、過去に遭遇したモデルがランダムな推測よりも良いものに収束しない安定性の問題のほとんどは、学習率スケジュールの設定ミスが原因でした。まだ試していない場合は、学習率スケジュールを調整してみてください。
> 
> 
> 
> > ## Valentin Wernerトピック作成者
> > 
> > James、コンペティションへようこそ。DAIGTでも素晴らしいトレーニングをしたことを覚えています。再びLBのトップであなたに会えるのを楽しみにしています！
> > 
> > 埋め込みのみを使用しているのか、それとも2つのDeBERTaモデルを結合して上にレイヤーを追加したのか、正しく理解していますか？
> > 
> > 
> > 
> > > ## James Day
> > > 
> > > 私の0.997のベースラインは、会話の各「側」（各側は、初期のプロンプト、モデルXの最初の応答、フォローアッププロンプト（存在する場合）、モデルXの2番目の応答…最大768トークンのコンテキスト長まで）を連結したもの）を処理するために、同じDeBERTaバックボーンを使用しました。各側（AとB）のCLSトークンからの埋め込みを連結し、小さな分類ヘッドに供給しました。言い換えれば、DeBERTaモデル1つに、上に追加のレイヤーがいくつか重ねられています。全体がトレーニング可能でした。埋め込みを計算するために、凍結された事前トレーニング済みバックボーンを使用しませんでした。
> > > 
> > > 上記のアプローチは、基礎モデルとしてLlama 3 8Bを使用するようにスケールアップすることで簡単に上回ることができます。
> > > 
> > > 
> > > 
---
> ## Takamichi Toda
> 
> 私の実験で効果的だったことを共有します。
> 
> 現在、計算リソースの確保が難しいので、DeBERTa xsmallで実験を行っています。環境の違いにより、同じ結果が得られない場合があることに注意してください。
> 
> ### ラベルスムージング
> 
> クロスエントロピー損失を使用し、label_smoothingパラメータを0.2に設定しています。理由は、コンペティションデータは同じデータに対して異なるラベル付けがされている可能性があり、ノイズデータの一種と言えると思ったからです。
> 
> ### タスク内事前トレーニング
> 
> コンペティションデータを使用してマスクされた言語モデルをトレーニングし、これらの重みをファインチューニングに使用しています。
> 
> ### ドロップアウトオフ
> 
> ドロップアウト率を調整しましたが、0が最も効果的でした。
> 
> ドロップアウトは回帰問題ではオフにするべきだと聞いたことがありますが、これはそうではありません。なぜドロップアウトがない方が精度が高くなるのか理解できません。🧐
> 
> ### 対抗学習
> 
> AWPを試しましたが、効果的でした。FGMなどの他の方法もテストする予定です。
> 
> 
> 
> > ## Valentin Wernerトピック作成者
> > 
> > XsmallとLargeの間で安定した結果を得られましたか？私の場合、小さいモデルは収束しないため、Largeのみをトレーニングしました。これは、実験の反復速度が非常に遅くなります。
> > 
> > 共有していただきありがとうございます！
> > 
> > 
> > 
> > ## Valentin Wernerトピック作成者
> > 
> > AWPでトレーニングを試みたところ、モデルはすぐに何も学習しなくなりました。興味深いですね。
> > 
> > 
> > 
> > > ## Takamichi Toda
> > > 
> > > うーん、なぜだろう。
> > > 
> > > どのようなモデルを使用していますか？私はまだDeBERTa xsmallを使用しているので、モデルサイズの差による可能性があります。
> > > 
> > > AWP学習率に小さな値を適用してみてはどうでしょうか？
> > > 
> > > 私の場合は、1e-4です。ちなみに、全体的な学習率は2e-5です。
> > > 
> > > 
> > > 
> > > ## Valentin Wernerトピック作成者
> > > 
> > > AWPについては、さらに調査する必要があると思います。以前は使用したことがなく、既存のKaggleノートブックをベースにしています。
> > > 
> > > 小さいモデルでは成功せず、DeBERTa-3-largeで1.00に近づいただけです。また、有効なバッチサイズは8（2 x 4）、学習率は約8e-6を使用しています。これは、あなたの学習率よりもはるかに低いです…さらに実験する時間ですね :)
> > > 
> > > 
> > > 
---
> ## Valentin Wernerトピック作成者
> 
> 昨日、DeBERTa-3-largeモデルをトレーニングし、1.005を達成しました。今日、同じトレーニングパラメータを使用しても、約1.07になります。非常に信頼性が低いように思えます。LoRAでも良いスコアを達成できていません。
> 
> 
> 
> > ## James Day
> > 
> > おかしいですね。私の場合、実行間のランダムな変動は0.01未満です。CVとLBも非常に高い相関関係があります（ピアソンのr = 0.97）。
> > 
> > 私の考えでは、トレーニングパイプラインに何かが壊れているか、設定ミスがあります。データ自体に固有の問題ではありません。
> > 
> > 
> > 
> > > ## yechenzhi1
> > > 
> > > こんにちは。CVの分割方法を教えていただけますか？トレーニングデータセットから10％をランダムに分割しましたが、CVとLBのスコアは大きく異なります。CVスコアは0.889、LBは0.922です。
> > > 
> > > 
> > > 
---



</div>