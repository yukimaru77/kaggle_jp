# 要約 
ディスカッションでは、コンペティションの参加者が「keywords.py」について疑問を持ち、主に以下の点が議論されています。

1. **キーワードの使用目的**: 参加者のKhoi Nguyenが、キーワードが最初のフェーズでどのように使用されるのか、またプライベートテストで他のカテゴリーが含まれるかどうかを尋ねています。

2. **リーダーボードの透明性**: Duke SilverとChris Deotteは、公開リーダーボードがプライベートリーダーボードを正確に反映していないと指摘し、成功するモデルが異なる可能性について言及しています。また、キーワード以外の単語でモデルを訓練することの価値についても話しています。

3. **ガイダンスの提供**: Bovard Doerschuk-Tiberiが、第二フェーズのカテゴリーについてのガイダンスを提供する意向を示しています。

4. **評価の懸念**: Rob Mullaと他のユーザーは、締切後に新しいキーワードセットが使用されることにより、リーダーボードが過剰適合するリスクがあると懸念しています。

5. **キーワードのカテゴリーの限界**: 一部のユーザーは、現在提供されている3つのカテゴリー以外の選択肢がないことを確認しています。

6. **keyword.pyの利用**: alekhが「keyword.py」ファイルの環境内での利用可能性を尋ね、そのファイルがKaggle環境に含まれていることが確認されましたが、使用は推奨されていません。

全体として、キーワードの使用、リーダーボードの透明性、評価基準、及び「keyword.py」の利用方法についてのクリアな情報を求める声が多く上がっています。

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

# Scope of keywords.py

**Khoi Nguyen** *Thu May 16 2024 17:49:23 GMT+0900 (日本標準時)* (20 votes)

A few questions since there is no description (yet):

- Are the keywords there also the ones actually used for the first phase or are they just for debugging?

- Will the second phase (private test) contains categories outside of the 3 in there?



---

 # Comments from other users

> ## Duke Silver
> 
> It feels like public leaderboard doesn't really represent the private leaderboard very well.
> 
> 
> 
> > ## Chris Deotte
> > 
> > True. The solutions which are successful on public LB will be much different than successful models on private LB. (Because we have list of possible keywords for public LB but do not for private LB). None-the-less both offer learning opportunities for the other.
> > 
> > 
> > 
> > > ## Duke Silver
> > > 
> > > It seems like it could be better to train models on words outside of the keywords given as well to make the model more adaptive
> > > 
> > > 
> > > 


---

> ## Bovard Doerschuk-Tiberi
> 
> [@suicaokhoailang](https://www.kaggle.com/suicaokhoailang) We are considering a few options here on expanding the word list and giving guidance on categories for the second phase. We will make an announcement when it's decided.
> 
> 
> 


---

> ## Rob Mulla
> 
> I have similar questions. From what I gather reading the competition description and looking at the keywords used in games on the leaderboard:
> 
> - Current games look like they only use the subsection of keywords provided in keywords.py
> 
> - After the submission deadline there will be a new set of keywords used.
> 
> From the [evaluation section](www.kaggle.com/competitions/llm-20-questions/overview/evaluation): 
> 
> "At the submission deadline on August 13, 2024, submissions will be locked. From August 13, 2024 to August 27th, 2024 we will continue to run episodes against a new set of unpublished, secret words. At the conclusion of this period, the leaderboard is final."
> 
> This might mean that the "pre-deadline" leaderboard is going to be overfit to these words unfortunately.
> 
> 
> 
> > ## G John Rao
> > 
> > The keywords will be within those three categories? This is the real question that needs to be answered by the hosts
> > 
> > 
> > 
> > > ## Bovard Doerschuk-Tiberi
> > > 
> > > Stay tuned, we'll make an announcement to address this. Thank you!
> > > 
> > > 
> > > 
> > > ## Chandresh J Sutariya
> > > 
> > > any update??
> > > 
> > > 
> > > 


---

> ## alekh
> 
> Is the keyword.py file included in the environment? i.e. can i read it and feed it to my agent?
> 
> 
> 
> > ## Bovard Doerschuk-Tiberi
> > 
> > keyword.py is indeed contained in the kaggle-environment pip package. However I advise against using it, agents will not have access to the final list published after the submission deadline:
> > 
> > Final Evaluation
> > 
> >   At the submission deadline on August 13, 2024, submissions will be locked. From August 13, 2024 to August 27th, 2024 we will continue to run episodes against a new set of unpublished, secret words. At the conclusion of this period, the leaderboard is final.
> > 
> > 
> > 
> > > ## VolodymyrBilyachat
> > > 
> > > Will it be just new keywords in those categories or new categories too?
> > > 
> > > 
> > > 
> > > ## Gavin Cao
> > > 
> > > "agents will not have access to the final list published after the submission deadline."  does it mean agent could not read keyword.py after August 13? or the final list will be different from the content of  keyword.py?
> > > 
> > > 
> > > 


---

> ## Sheema Zain
> 
> Looks like there is just those 3 categories!
> 
> 
> 


---

> ## VolodymyrBilyachat
> 
> Looks like there is just those 3 categories
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# keywords.py の範囲
**Khoi Nguyen** ＊2024年5月16日 17:49:23 JST＊ (20票)  
現時点では説明がないため、いくつか質問があります：
- キーワードは、最初のフェーズで実際に使用されるものでしょうか、それともデバッグ用のものでしょうか？
- 第二のフェーズ（プライベートテスト）では、そこにある3つのカテゴリー以外のものが含まれるのでしょうか？

---
 # 他のユーザーからのコメント
> ## Duke Silver
> 
> 公開リーダーボードはプライベートリーダーボードをあまりよく表していないように感じます。

> 
> > ## Chris Deotte
> > 
> > 確かにそうですね。公開リーダーボードで成功する解決策は、プライベートリーダーボードで成功するモデルとは大きく異なるでしょう。（公開LB用の可能なキーワードのリストは知っていますが、プライベートLB用のものは知らないためです。）とはいえ、どちらも他のモデルにとって学習の機会を提供します。
> > 
> > 
> > > ## Duke Silver
> > > > それに、与えられたキーワード以外の単語でモデルを訓練する方が、モデルをより適応的にするのには良いかもしれないと思います。
> > > > 
> > > 

---
> ## Bovard Doerschuk-Tiberi
> 
> [@suicaokhoailang](https://www.kaggle.com/suicaokhoailang) いくつかのオプションについて検討中で、第二のフェーズでのカテゴリーについてのガイダンスを提供することを考えています。決定次第、発表を行います。

---
> ## Rob Mulla
> 
> 私も似たような質問があります。コンペティションの説明を読み、リーダーボード上でのゲームに用いられるキーワードを見た限り、以下のことが分かりました：
> 
> - 現在のゲームは、keywords.pyに提供されているキーワードのサブセクションのみを使用しているようです。
> 
> - 提出期限後には、新しいキーワードのセットが使われるでしょう。
> 
> [評価セクション](www.kaggle.com/competitions/llm-20-questions/overview/evaluation)には次のように書かれています：
> 「2024年8月13日の提出締め切り時点で、提出物はロックされます。2024年8月13日から8月27日まで、新しい非公開の秘密の単語のセットに対してエピソードを実施し続けます。この期間が終了すると、リーダーボードが確定します。」
> 
> これにより、「締切前」のリーダーボードがこれらの単語に対して過剰適合してしまう可能性があります。

> 
> > ## G John Rao
> > > キーワードはこれらの3つのカテゴリーに含まれるのでしょうか？ これがホストから回答が必要な本当の質問です。
> > > 
> > > 
> > > > ## Bovard Doerschuk-Tiberi
> > > > > 引き続きお待ちください。発表を行います。ありがとうございます！
> > > > 
> > > >
> > > > > ## Chandresh J Sutariya
> > > > > > アップデートはありますか？
> > > > > 
> > > 

---
> ## alekh
> 
> keyword.pyファイルは環境に含まれていますか？つまり、これを読み取ってエージェントに提供できるのでしょうか？

> 
> > ## Bovard Doerschuk-Tiberi
> > 
> > keyword.pyは確かにkaggle-environmentのpipパッケージに含まれています。ただし、使用することはお勧めしません。エージェントは提出締切後に公開される最終リストにはアクセスできないからです：
> > 
> > 最終評価
> > >
> > > 2024年8月13日の提出締め切り時点で、提出物はロックされます。2024年8月13日から8月27日まで、新しい非公開の秘密の単語のセットに対してエピソードを引き続き実施します。この期間が終了すると、リーダーボードが確定します。
> > 
> > 
> > > ## VolodymyrBilyachat
> > > > それは、これらのカテゴリーの新しいキーワードだけになりますか？それとも新しいカテゴリーも追加されるのでしょうか？
> > > > 
> > > 
> > > > ## Gavin Cao
> > > > > 「エージェントは提出締切後に公開される最終リストにはアクセスできない」とはどういう意味ですか？エージェントは8月13日以降にkeyword.pyを読み取ることができないのでしょうか？それとも最終リストがkeyword.pyの内容とは異なるのでしょうか？
> > > > 
> > > 

---
> ## Sheema Zain
> 
> どうやらその3つのカテゴリーしかないようです！

> 
> 
> ## VolodymyrBilyachat
> 
> やはりその3つのカテゴリーだけのようです。


</div>