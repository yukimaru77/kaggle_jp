# 要約 
以下は、コンペのディスカッションに関する要約です。

---

**テーマ**: keywords.py の変更と関連質問

**主な変更内容**:
- keywords.pyでは、推測対象となる単語のカテゴリが「人」「場所」「物」の3つに簡略化される。この変更は2024年6月の第一週に実施される予定で、今後も新しい単語が追加される。
- 最終提出締切後にはエージェントが使用できる単語セットが変更されるが、カテゴリは変わらず「人」「場所」「物」のままである。全ての潜在的な単語リストに依存しないようにとの注意もなされている。

**ユーザーからの質問と回答**:
- 質問者は、カテゴリにおける「人」とは特定の個人か一般的な職業かを尋ねるが、特定の人物の名前（有名人やインフルエンサー）や職業（医者、配管工など）が混在する可能性があるとされている。
- 他の質問者は、推測する単語が常に2単語以内か、ハイフンを含む可能性について疑問を呈し、システムでは大文字小文字や句読点が無視されるとの回答を得ている。
- keywords.py とプライベートリーダーボードのキーワードが、データセットのランダムなサンプルで構成されているかどうかについても質問があり、キーワードカテゴリ間の分布についての情報も求められている。
- 「物」カテゴリーにおける具体的な単語の例として犬が挙げられ、その定義が物理的なオブジェクトであることが説明されている。

この要約から、ディスカッションではキーワード変更に関する詳細や、それに関するユーザーの疑問とその解決が主な内容として浮かび上がる。

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

# Upcoming changes to keywords.py

**Bovard Doerschuk-Tiberi** *Sat Jun 01 2024 08:35:32 GMT+0900 (日本標準時)* (21 votes)

There will be a few changes to keywords.py (this is the list of possible words to guess for the game).

Categories will be simplified into person, place, or thing.
Change will happen next week (first week of June)
Half way through the competition more words will be added

As stated in the rules, after the FINAL submission deadline, the words will be swapped for a set that is NOT accessible by your agents. This word set will have the same 3 categories

IMPORTANT: Do not rely on knowing the full list of possible words ahead of time!

EDIT: This will now roll out early next week, sorry for the delay!

This has been implemented, see details here: [https://www.kaggle.com/competitions/llm-20-questions/discussion/512955](https://www.kaggle.com/competitions/llm-20-questions/discussion/512955)



---

 # Comments from other users

> ## Adam Kulik
> 
> I have a question regarding person and place category. Will it always be a specific person or place, or can it be generic, e.g. a doctor, a plumber?
> 
> 
> 
> > ## OminousDude
> > 
> > I also wanted to know this I used to think it would be specific people's names (celebrities, influencers, etc) but now I believe it will be occupations. On the other hand occupations aren't people but jobs so I am completely dumbfounded on this topic.😂
> > 
> > 
> > 


---

> ## David
> 
> Would the formatting of the keywords change after final submission deadline? Like can we always expect it to be no more than 2 words? Can we ever expect things like "Guinea-Bissau" with hyphens?
> 
> 
> 
> > ## RS Turley
> > 
> > In the code for the competition, it looks like punctuation and capitalization are ignored when comparing guesses to the keyword, so hyphens shouldn't matter. Here is the code used:
> > 
> > ```
> > def keyword_guessed(guess: str) -> bool:
> >     def normalize(s: str) -> str:
> >       t = str.maketrans("", "", string.punctuation)
> >       return s.lower().replace("the", "").replace(" ", "").translate(t)
> > 
> >     if normalize(guess) == normalize(keyword):
> >       return True
> >     for s in alts:
> >       if normalize(s) == normalize(guess):
> >         return True
> > 
> >     return False
> > 
> > ```
> > 
> > 
> > 


---

> ## mhericks
> 
> Can we assume that keywords.py and the keywords used for the evaluation of the private leaderboard are a random partition of a "large" dataset, i.e. keywords.py contains a random sample of a dataset and the remaining keywords are used for the private evaluation?
> 
> Especially, can we assume that the distribution of keywords among categories is the same between the two subsets?
> 
> 
> 


---

> ## Lucas Fernandes
> 
> Hi, what do you mean by 'thing' for example would a dog be a 'thing' or is that a word that won't be apart of the dataset.
> 
> Thank you 
> 
> 
> 
> > ## Bovard Doerschuk-Tiberi
> > 
> > Yes, a dog would count in the "thing" category.
> > 
> > I don't have a precise definition of what will count as a thing, but when you see the released word list you'll have a better idea. Generally a thing should be a physical object or being (like a rock or dog), not an abstract concept (like GDP)
> > 
> > 
> > 


---

> ## Saatvik Pradhan
> 
> Thats great
> 
> 
> 


---

> ## Rafael Yakupov
> 
> Hello, thank you very much for the information. I have a question, will the categories remain the same after changing the word set after FINAL submission deadline?
> 
> 
> 
> > ## Bovard Doerschuk-Tiberi
> > 
> > yes, the categories will always be person, place, or thing going forward
> > 
> > 
> > 
> > > ## AAElter
> > > 
> > > The 20 questions game I played when young was animal, vegetable, or mineral.  With this game, I would think "thing" (oh, Thing!) would encompass all animals except humans, vegetables and minerals, and manmade objects made out of those things.
> > > 
> > > 
> > > 


---



</div>
<div class="column-right">

# 日本語訳

# keywords.py に関する今後の変更について
**Bovard Doerschuk-Tiberi** *2024年6月1日（土）08:35:32 GMT+0900 (日本標準時)* (21票)
keywords.py（ゲームで推測される単語のリスト）にいくつかの変更が行われます。
カテゴリは「人」「場所」「物」に簡略化されます。
変更は来週（6月の第一週）に実施されます。
コンペティションの途中で、さらに多くの単語が追加されます。
ルールに記載されている通り、最終提出締切後にはあなたのエージェントがアクセスできない単語セットに入れ替えられます。この単語セットも同じ3つのカテゴリになります。
重要: 事前に全ての可能な単語リストを知っておくことに依存しないでください！
編集: 来週初めにこれを実施します。遅延についてお詫びします！
これが実施されました。詳細はこちらをご覧ください: [https://www.kaggle.com/competitions/llm-20-questions/discussion/512955](https://www.kaggle.com/competitions/llm-20-questions/discussion/512955)

---
# 他のユーザーからのコメント
> ## Adam Kulik
>
> 人と場所のカテゴリについて質問があります。それは常に特定の人や場所になりますか、それとも一般的なもの（例えば、医者や配管工など）も含まれますか？

>
> > ## OminousDude
> > 
> > 私もこれについて知りたかったです。私は以前、特定の人物の名前（有名人やインフルエンサーなど）になると思っていましたが、今は職業になるのではないかと思っています。職業は人ではなく仕事なので、この点については完全に混乱しています。😂
> > 
> > 
> > 

---
> ## David
> 
> 最終提出締切後にキーワードのフォーマットは変更されますか？例えば、常に2単語以内にまとめられるのでしょうか？それとも「ギニアビサウ」のようなハイフンを含むものが出てくる可能性はありますか？

> 
> > ## RS Turley
> > 
> > コンペティションのコードでは、キーワードに対する推測と比較する際に句読点と大文字小文字が無視されるようなので、ハイフンは問題ないと思います。以下のコードが使われています：
> > 
> > ```
> > def keyword_guessed(guess: str) -> bool:
> >     def normalize(s: str) -> str:
> >       t = str.maketrans("", "", string.punctuation)
> >       return s.lower().replace("the", "").replace(" ", "").translate(t)
> > 
> >     if normalize(guess) == normalize(keyword):
> >       return True
> >     for s in alts:
> >       if normalize(s) == normalize(guess):
> >         return True
> > 
> >     return False
> > 
> > ```
> > 
> > 

---
> ## mhericks
> 
> keywords.pyとプライベートリーダーボードの評価に使用されるキーワードは、大規模なデータセットのランダムな分割であると推測できますか？つまり、keywords.pyにはデータセットのランダムなサンプルが含まれ、残りのキーワードがプライベート評価に使用されるのでしょうか？
>
> 特に、カテゴリ間のキーワードの分布は、両方のサブセットで同じであると考えられますか？

---
> ## Lucas Fernandes
> 
> こんにちは、「物」とは何を意味しますか？例えば、犬は「物」としてカウントされるのでしょうか？それともデータセットに含まれない言葉ですか？
>
> ありがとうございます。

> > ## Bovard Doerschuk-Tiberi
> > 
> > はい、犬は「物」カテゴリに含まれます。
> > 
> > 何が「物」としてカウントされるかについての正確な定義はありませんが、公開された単語リストを見ればより良いアイデアが得られるでしょう。一般的には、「物」とは物理的なオブジェクトや存在（岩や犬など）を指し、抽象的な概念（GDPのようなもの）ではありません。
> > 
> > 

---
> ## Saatvik Pradhan
> 
> それは素晴らしいですね。

---
> ## Rafael Yakupov
> 
> こんにちは、情報をありがとうございます。質問がありますが、最終提出締切後に単語セットが変更されてもカテゴリは変わらないのですか？

> 
> > ## Bovard Doerschuk-Tiberi
> > 
> > はい、今後は常にカテゴリは「人」、「場所」、「物」となります。
> > 
> > 
> > > ## AAElter
> > > > 私が子供の頃に遊んだ20の質問ゲームでは、「動物、植物、鉱物」でした。このゲームでは、「物」（ああ、Thing!）は人間を除くすべての動物、植物、鉱物、そしてそれらのものから作られた人工物を含むと思います。
> > > > 
> > > > 


</div>