# 要約 
ディスカッションでは、ユーザー**OminousDude**がリーダーボードのポイントに異常を感じ、特にエージェント「hsling」がスコアを大きく獲得した理由について疑問を呈しています。彼はゲームのスコアの増加がなかったことを指摘し、何が原因でこのようなポイントが与えられたのかについてのバグの可能性を示唆しています。

それに対して、**Bovard Doerschuk-Tiberi**が回答し、最初のゲームで「mhericks」のエージェントがエラーを出したため、他のエージェントが1位となったことを説明しています。また、エージェントの評価がゲームの進行に伴って変わることや、不確実性項の影響を受けることについて詳細に述べています。最終的に、**OminousDude**はBovardの説明を理解し、エラーの存在に気づいたことを認めています。

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

# Why is this agent getting points for this?

**OminousDude** *Mon Jun 03 2024 11:13:00 GMT+0900 (日本標準時)* (0 votes)

I am activaly checking the LB and when I saw this I knew something was off. How did hsling get +27 for this? Is there another bug in the loss function or something?

[https://www.kaggle.com/competitions/llm-20-questions/leaderboard?dialog=episodes-episode-54945938](https://www.kaggle.com/competitions/llm-20-questions/leaderboard?dialog=episodes-episode-54945938)

This one didn't have a score increase (it was 0) but still what?!?!

[https://www.kaggle.com/competitions/llm-20-questions/leaderboard?dialog=episodes-episode-54945203](https://www.kaggle.com/competitions/llm-20-questions/leaderboard?dialog=episodes-episode-54945203)



---

 # Comments from other users

> ## Bovard Doerschuk-Tiberi
> 
> First game:
> 
> [1st] hsling 601 (+27)
> 
> [1st] Phạm Huỳnh Thiên Phú 599 (+7)
> 
> [Err] mhericks 578 (-74)
> 
> [1st] Toon 597 (+28)
> 
> mhericks agent errored out, so it counts as a loss for that agent and all other agents get 1st place. When they win they compare their collective rating vs mhericks rating which should give them an expected probability of winning. In this case all of the agents are relatively the same rated.
> 
> However this is also a second component of our scoring system, an uncertainty term that decays as agents play more game. In this case both Toon and hsling have a larger uncertainty term (so they get more rating from the game) than Pham team (who receives less rating)
> 
> Second game:
> 
> [1st] hsling 599 (-0)
> 
> [1st] ITASps 599 (-0)
> 
> [1st] Gauranshu Rathee 596 (+1)
> 
> [1st] Guan 600 (-0)
> 
> The game result here was a tie (everyone on 1st place) and everyone is similarly rated so the expected change in rating should be quite small. Besides the -0 here, this looks expected.
> 
> Let me know if you have any other questions!
> 
> 
> 
> > ## OminousDudeTopic Author
> > 
> > Thank you very much for this explanation didn't see the error in the first one!
> > 
> > 
> > 


---



</div>
<div class="column-right">

# 日本語訳

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


</div>