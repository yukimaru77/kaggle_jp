# なぜこのエージェントがポイントを獲得しているのか？
**OminousDude** *2024年6月3日 月曜日 11:13 (日本標準時)* (0票)  
リーダーボードをアクティブに確認しているのですが、これを見たとき、何かがおかしいと感じました。hslingはなぜ+27を獲得したのですか？損失関数に別のバグでもあるのでしょうか？  
[https://www.kaggle.com/competitions/llm-20-questions/leaderboard?dialog=episodes-episode-54945938](https://www.kaggle.com/competitions/llm-20-questions/leaderboard?dialog=episodes-episode-54945938)  
このゲームではスコアの増加はなかったのに（0でした）、それでも何ですか?!?  
[https://www.kaggle.com/competitions/llm-20-questions/leaderboard?dialog=episodes-episode-54945203](https://www.kaggle.com/competitions/llm-20-questions/leaderboard?dialog=episodes-episode-54945203)  
---  
# 他のユーザーのコメント
> ## Bovard Doerschuk-Tiberi
> 
> 最初のゲーム:
> 
> [1位] hsling 601 (+27)
> 
> [1位] Phạm Huỳnh Thiên Phú 599 (+7)
> 
> [エラー] mhericks 578 (-74)
> 
> [1位] Toon 597 (+28)
> 
> mhericksのエージェントがエラーを出したため、そのエージェントは敗北と見なされ、他のすべてのエージェントが1位となります。勝利すると、彼らの集団評価がmhericksの評価と比較され、勝利の期待確率が得られます。この場合、全てのエージェントは相対的に同じ評価です。  
> 
> ただし、これはまた、エージェントがゲームをプレイするにつれて減少する不確実性項の影響も受けます。この場合、ToonとhslingはPhamチームより不確実性項が大きいため、ゲームからより多くの評価を受けています（Phamチームは評価が少なくなります）。  
> 
> 第二のゲーム:
> 
> [1位] hsling 599 (-0)
> 
> [1位] ITASps 599 (-0)
> 
> [1位] Gauranshu Rathee 596 (+1)
> 
> [1位] Guan 600 (-0)
> 
> このゲームの結果は引き分け（全員1位）でしたが、皆同じ評価だったため、評価の変化は非常に小さいはずです。-0に関しては、これは期待通りです。  
> 
> 他に質問があれば教えてください！  
> 
> > ## OminousDude トピック作成者
> > 
> > この説明ありがとうございました。最初のものにエラーがあったとは気づきませんでした！  
> > 
