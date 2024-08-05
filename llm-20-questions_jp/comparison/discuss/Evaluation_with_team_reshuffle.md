# 要約 
### 要約

コンペティションにおけるチームの再編成に関する議論が行われており、主にモデルの評価に関する懸念が述べられています。参加者のAzat Akhtyamovは、チーム間のバランスを取るためにモデルを入れ替えて再対戦することを提案しています。これに対して、他のユーザーは、エージェントの性能を不当に左右するような不公平なペアリングの例を挙げ、全エージェントが公平に対戦する必要性を強調します。

特に、モデルBが適切に機能しない場合に、全体の勝率にランダム性が増すため、より効果的に評価を行う手段としてのシャッフルマッチングの必要性が議論されています。また、再プレイにより得られる統計的利益についても議論があり、これが評価の正確さを向上させるかどうかに対する疑念も示されています。

Neuron Engineerは、特定の悪いプレイヤーと常にペアになってしまう新しいプレイヤーの評価が不公平であることを指摘し、エージェントの能力を正確に測ることが難しいと述べています。このため、シャッフルマッチングの導入が望まれるという意見が表明されています。全体的に、公平な評価システムの必要性と実現可能性が焦点となっています。

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

# Evaluation with team reshuffle

**Azat Akhtyamov** *Thu Jul 11 2024 09:32:44 GMT+0900 (日本標準時)* (18 votes)

Hi!

Currently, A and B play against C and D. If model B, which is an answering model, is badly tuned (if tunned at all) - team AB is doomed no matter what. This introduces a lot of random, which does not allow us to evaluate the models properly. What if after the game AB-CD we run a game AD-CB (swapping the answering bots) with exactly the same keyword? This will introduce at least some symmetry and fairness to the scores. 

Dear Kaggle team, please think about this. 

CC [@bovard](https://www.kaggle.com/bovard) [@addisonhoward](https://www.kaggle.com/addisonhoward) [@mylesoneill](https://www.kaggle.com/mylesoneill)



---

 # Comments from other users

> ## loh-maa
> 
> What if model B is also poor at asking questions? Then perhaps A should also play with D against B and C, and C against B and D, and then against E and F, and to make things even more fair, every agent should play against every agent, and this is actually going to happen in the end, except randomly.
> 
> 
> 
> > ## Azat AkhtyamovTopic Author
> > 
> > While I agree that it would be even better, we are constrained with limited amount of gpu…
> > 
> > 
> > 
> > > ## loh-maa
> > > 
> > > Hi [@azakhtyamov](https://www.kaggle.com/azakhtyamov), I think the same constraint applies to reshuffling. It doubles the cost of evaluation. And actually it's not just a matter of changing a single parameter -- the format is established, including the ranking algorithm and visualization. Implementing such team reshuffling would complicate things, introducing unclarity, possibly new bugs and likely inviting a new bunch of requests from players. I think people supporting this idea don't take this into account at all.
> > > 
> > > The key question though is: does reshuffled evaluation provide significantly more overall "convergence gain" than two independent games? I doubt, and I would be seriously impressed If you could demontrate that actually it does.. ,)
> > > 
> > > 
> > > 
> > > ## Robert Hatch
> > > 
> > > Just guessing, but there's probably a ton of statistical benefit from the simple swap and replay. 
> > > 
> > > I'm not certain on the statistics in terms of theoretical proof, but I really think it should be trivial to show that as you increase the relative randomness of "pairing luck" and decrease the relative randomness of models AB beating models CD, then of course it will converge faster if swapping pairings. 
> > > 
> > > At that point, though, there's additional benefit if building a scoring system from scratch. Assuming no ties, every pairing will have a single winner and a single loser, which will either be the questioner models winning/losing, or the answerer models winning/losing. There might be ways to use that in bot ratings to quickly relegate the bad answerer models, or punish those losses higher, or whatever. 
> > > 
> > > Not invested in the competition, and I actually agree they shouldn't change it for this one at this point. But it seems very likely that the suggestion of match pairs (or quad battles) would indeed help (a lot) vs continuous random, statistically. 
> > > 
> > > 
> > > 


---

> ## Neuron Engineer
> 
> I also want to question about the evaluation system on similar issue:
> 
> Is the following result reasonable?
> 
> NewPlayer605 paired with BadPlayer533 who always be a wrong syntax guesser.
> 
>  vs. BetterPlayer732 & BetterPlayer652
> 
> NewPlayer605 unavoidably lost and get the most penalized of the four. (-128 points), and so continue to be paired with other BadPlayers.
> 
> Is this pairing and scoring intentional ?
> 
> Because if yes, in order to measure the real ability of NewPlayer605, we have to continuously resubmit the agent  and hope to not pair with the SyntaxErrorPlayers . And so it looks totally difficult to evaluate the NewPlayer capability.
> 
> The shuffle matching mentioned in the OP seems to help this issue to be fairer in my opinion.
> 
> [@bovard](https://www.kaggle.com/bovard) [@addisonhoward](https://www.kaggle.com/addisonhoward) [@mylesoneill](https://www.kaggle.com/mylesoneill)
> 
> 
> 
> > ## Neuron Engineer
> > 
> > Illustration of the BadSyntaxErrorPlayer
> > 
> > 
> > 


---



</div>
<div class="column-right">

# 日本語訳

# チームの再編成による評価
**Azat Akhtyamov** *2024年7月11日 09:32:44 JST* (18票)
こんにちは！
現在、チームAとBがチームCとDに対戦しています。もしモデルB（応答モデル）がうまく調整されていない場合（まったく調整されていない場合も含む）、チームABはどんな結果でも勝てないでしょう。これは多くのランダム性を引き入れ、モデルを適切に評価することを妨げます。ゲームAB-CDの後に、同じキーワードでゲームAD-CB（応答ボットを入れ替える）を実行したらどうでしょうか？これにより、少なくとも得点に対していくつかの対称性と公平性が生まれるでしょう。
Kaggleチームの皆さん、これについて考えていただけますか？ 
CC [@bovard](https://www.kaggle.com/bovard) [@addisonhoward](https://www.kaggle.com/addisonhoward) [@mylesoneill](https://www.kaggle.com/mylesoneill)
---
# 他のユーザーからのコメント
> ## loh-maa
>
> モデルBが質問をうまく尋ねられない場合はどうなるでしょうか？それなら、AがDと組んでBとCに対抗し、CがBとDに対抗し、その後EとFにも対抗させる必要があります。さらに公平にするためには、すべてのエージェントがすべてのエージェントに対してプレイする必要があり、最終的にはそれが実際に起こるでしょうが、ランダムに。
>
> > ## Azat Akhtyamov トピック作成者
> > 
> > 確かに、それはさらに良いと思いますが、GPUの量が限られていることに制約されているのです…
> > 
> > > ## loh-maa
> > > 
> > > こんにちは[@azakhtyamov](https://www.kaggle.com/azakhtyamov)、私は同じ制約が再編成にも適用されると思います。それは評価のコストを倍増させます。そして実際、これは単一のパラメーターを変更する問題ではなく、ランキングアルゴリズムやビジュアル化を含むフォーマットが確立されています。このようなチームの再編成を実装することは、混乱を引き起こし、さらなるバグを招く可能性があり、プレイヤーから新たなリクエストが来る可能性があります。このアイデアを支持する人々は、これをまったく考慮していないと思います。
> > > 
> > > 重要な質問は、再編成された評価が二つの独立したゲームよりも全体的に「収束の獲得」を大幅に向上させるかどうかです。私は疑わしいですし、それが実際にそうであることを示せば非常に感心します…。
> > > 
> > > > ## Robert Hatch
> > > > 
> > > > 仮定ですが、単純な入れ替えと再プレイからは多くの統計的利益が得られると思います。
> > > >
> > > > 理論的な証明の観点からは確信が持てませんが、「ペアの運」の相対的なランダム性を増やし、モデルABがモデルCDに勝つ相対的なランダム性を減少させると、もちろんペアリングを入れ替えれば早く収束することが明らかになります。
> > > >
> > > > その時点では、スコアリングシステムをゼロから構築する追加の利益があります。引き分けがないと仮定すれば、すべてのペアは単一の勝者と単一の敗者を持ち、質問者モデルが勝つ/負けるか、応答者モデルが勝つ/負けるかのいずれかです。これをボットの評価に利用して、悪い応答者モデルを迅速に排除したり、そうした敗北に対する罰を強化したりする方法があるかもしれません。
> > > >
> > > > 私はこのコンペに投資していませんし、実際、今すぐにこれを変更すべきではないに同意します。しかし、マッチペア（またはクアッドバトル）の提案が、連続したランダムな対戦に比べて統計的に非常に役立ちそうだと思われます。
> > > > 
> > >
---
> ## Neuron Engineer
>
> 同様の問題に関する評価システムについて質問したいと思います：
> 
> 次の結果は合理的ですか？
>
> 新しいプレイヤー605は、常に文法の誤りをする悪いプレイヤー533とペアになっています。
>
> それに対して、より良いプレイヤー732とより良いプレイヤー652と対戦します。
>
> 新しいプレイヤー605は避けられない形で敗北し、四人の中で最も厳しいペナルティ（-128ポイント）を受け、引き続き他の悪いプレイヤーとペアになっています。
>
> このペアリングとスコアリングは意図されたものですか？
> 
> もしそうなら、新しいプレイヤー605の本当の能力を測るためには、エージェントを継続的に再提出し、文法エラーのプレイヤーとペアにならないことを望まなければなりません。このため、本当に新しいプレイヤーの能力を評価することは非常に難しい印象を受けます。
>
> OPで述べたシャッフルマッチングは、私の意見ではこの問題をより公平にするでしょう。
>
> [@bovard](https://www.kaggle.com/bovard) [@addisonhoward](https://www.kaggle.com/addisonhoward) [@mylesoneill](https://www.kaggle.com/mylesoneill)
>
> > ## Neuron Engineer
> > 
> > 文法エラーの悪いプレイヤーの例を示します
> > 
> > 
---


</div>