# なぜこのエージェントはこのポイントを獲得しているのですか？
**OminousDude** *2024年6月3日月曜日 11:13:00 GMT+0900 (日本標準時)* (0 votes)
リーダーボードを積極的にチェックしていて、これを見たとき、何かおかしいと思いました。hslingはなぜこれに対して+27を獲得したのでしょうか？損失関数に別のバグがあるのでしょうか？
[https://www.kaggle.com/competitions/llm-20-questions/leaderboard?dialog=episodes-episode-54945938](https://www.kaggle.com/competitions/llm-20-questions/leaderboard?dialog=episodes-episode-54945938)
これはスコア増加がありませんでした（0でした）が、それでも何ですか？！
[https://www.kaggle.com/competitions/llm-20-questions/leaderboard?dialog=episodes-episode-54945203](https://www.kaggle.com/competitions/llm-20-questions/leaderboard?dialog=episodes-episode-54945203)
---
 # 他のユーザーからのコメント
> ## Bovard Doerschuk-Tiberi
> 
> 最初のゲーム：
> 
> [1位] hsling 601 (+27)
> 
> [1位] Phạm Huỳnh Thiên Phú 599 (+7)
> 
> [エラー] mhericks 578 (-74)
> 
> [1位] Toon 597 (+28)
> 
> mhericksのエージェントがエラーで終了したため、そのエージェントの負けとしてカウントされ、他のすべてエージェントが1位になります。彼らが勝つと、彼らの総合的な評価をmhericksの評価と比較します。これは、彼らが勝つ確率を期待値として与えるはずです。この場合、すべてエージェントは比較的同じ評価です。
> 
> しかし、これは私たちのスコアリングシステムの2番目の要素でもあります。これは、エージェントがより多くのゲームをプレイするにつれて減衰する不確実性の項です。この場合、ToonとhslingはどちらもPhamチームよりも大きな不確実性の項を持っています（そのため、ゲームからより多くの評価を受け取ります）。
> 
> 2番目のゲーム：
> 
> [1位] hsling 599 (-0)
> 
> [1位] ITASps 599 (-0)
> 
> [1位] Gauranshu Rathee 596 (+1)
> 
> [1位] Guan 600 (-0)
> 
> このゲームの結果は引き分け（全員が1位）であり、全員が同様に評価されているため、評価の期待される変化は非常に小さいはずです。この-0に加えて、これは期待どおりに見えます。
> 
> その他ご質問があればお知らせください！
> 
> 
> 
> > ## OminousDudeトピック作成者
> > 
> > この説明をいただきありがとうございます。最初のゲームのエラーに気づきませんでした！
> > 
> > 
> > 
---
