# 要約 
ディスカッションでは、「20の質問」ゲームにおける最適戦略に関する意見が交わされていますが、主要な焦点は二分探索のアプローチにあります。Khoi Nguyenは、有限かつランダムな答えのプールから最適の質問を絞り込むためには、質問を「このリストに答えはありますか？」という形で行い、場合によってはランダム性を考慮しながらフリースタイルの質問に切り替えるべきだと提案しています。

他のユーザーからは、質問の制限（2000文字）やプライベートラウンドでの単語リストの変化の可能性に言及され、一部は特定のリストをハードコーディングすることに対して懐疑的です。また、重要なポイントとして、秘密の単語が完全にランダムである必要があり、全参加者がそのランダム性を排除しようとすることが強調されます。最終的には、LLMsがこの情况においてどのような優位性を持つのか、また、対戦相手の回答者の誠実さや理解力がどのように結果に影響するかが議題として挙げられています。

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

# Optimal strategy (can LLMs beat binary search?)

**Khoi Nguyen** *Fri May 17 2024 21:29:31 GMT+0900 (日本標準時)* (8 votes)

Just a thought experiment. I'm not an expert on this game but from what I gathered, it looks like the optimal strategy when you have a finite pool of possible answers, assuming the correct answer is completely random, is to attempt to divide the remaining pool by half with each of your question.

Now in order to get a near perfect split while being sure that the answer agent did not hallucinate the result, a rule based approach like this is the best:

- Ask: Is the answer in this list <answer pool>, if answer is no, fallback to freestyle mode and pray to LLM god.

If answer is yes:

- Ask: Is the answer in this list <insert half of the remaining answer pool>

- Get a yes/no answer, this is guaranteed to be correct if everyone complies and use a specific asking syntax.

- Repeat from step 2 until there is only one answer left.

Looking at the keywords.py file, we can definitely crawl a large pool of possible countries, cities and landmarks for the private test. (if the landmark is too obscure for crawling I doubt the LLMs have enough information about it to guess anyway)

What edge do LLMs offer over this approach? I mean if the answer was chosen by a known LLM then it's prior knowledge that we can exploit, but when its completely random? 

citation that Gemini gave me: [https://www.cns.nyu.edu/~reuben/blog/20-questions-info-theory/](https://www.cns.nyu.edu/~reuben/blog/20-questions-info-theory/)

Note: Even when if the answer pool is non-crawlable or quasi-infinite (all possible English words), this is still a strong approach, just ask for stuff like: Is the first character of that word in this list […] or something.



---

 # Comments from other users

> ## Bovard Doerschuk-Tiberi
> 
> The list of possible words will change after the final submission deadline (meaning you won't be able to update your agent with the new list). I would strongly advise against any strategies that hard code in the list of possible words.
> 
> Final Evaluation
> 
>   At the submission deadline on August 13, 2024, submissions will be locked. From August 13, 2024 to August 27th, 2024 we will continue to run episodes against a new set of unpublished, secret words. At the conclusion of this period, the leaderboard is final.
> 
> 
> 


---

> ## chris
> 
> I had a similar thought. You do only get 2000 characters in your question (which means you can't really ask a question like "Is the answer in this list", but it does seem like a good approach to have some fixed list of possible values and do some kind of binary search.
> 
> 2^20 = 1,048,576
> 
> So if you hit every split exactly 50% then you could go through a list of ~1M things
> 
> If you use that approach though, you'd better hope that the thing is in your list! So it might be tricky if we're not given more information about the types of words in the private set.
> 
> EDIT: oh, I guess you have to use one guess to actually guess the word, right? So in that case you only get 2^19 = 524,288 max words.
> 
> 
> 
> > ## Khoi NguyenTopic Author
> > 
> > If no information are given about the words in the private set is it even possible to guess it? If the binary search method works perfectly like you said we can only narrow the search space down 2^19 times, anything beyond that is pure luck based.
> > 
> > 
> > 
> > > ## chris
> > > 
> > > There are ~90,000 nouns in english, but presumably they wouldn't use that full list but just pull from the top N most common.
> > > 
> > > There are far more individual places and people, but again, I would presume they would only pull the top N most famous of each.
> > > 
> > > So to solve the problem this way, the trick may just be where you do a cutoff.
> > > 
> > > 
> > > 
> > > ## Khoi NguyenTopic Author
> > > 
> > > Yeah top N most popular things is a fine assumption, so it's a risk vs reward thing in the private set when you either want to guess things faster or have higher chance for a successful guess and who have the N closest to the hosts' wins?
> > > 
> > > 
> > > 


---

> ## G John Rao
> 
> "Ask: Is the answer in this list , if answer is no, fallback to freestyle mode and pray to LLM god."
> 
> I don't think this is exactly what this competition is about. 
> 
> From the overview:
> 
> This competition will evaluate LLMs on key skills like deductive reasoning, efficient information gathering through targeted questioning, and collaboration between paired agents. It also presents a constrained setting requiring creativity and strategy with a limited number of guesses. Success will demonstrate LLMs' capacity for not just answering questions, but also asking insightful questions, performing logical inference, and quickly narrowing down possibilities.
> 
> The keywords.py contains 3 categories: country, city, landmark
> 
> I don't think the categories are limited to those 3, if that's the case, the competition is no fun. 
> 
> The starter notebook has a system prompt:
> 
> system_prompt = "You are an AI assistant designed to play the 20 Questions game. In this game, the Answerer thinks of a keyword and responds to yes-or-no questions by the Questioner. The keyword is a specific person, place, or thing."
> 
> For person and place one can make a list, I don't think it's worth it to make a list for "thing". Because a "thing" can be anything really. It can be a noun, a concept, an object, an idea, a feeling, or even an abstract entity. I think that's where the fun is, and that's where the LLMs come into play. 
> 
> "What edge do LLMs offer over this approach? I mean if the answer was chosen by a known LLM then it's prior knowledge that we can exploit, but when its completely random?"
> 
> I think the secret word has to be random. And all the participants work it to eliminate the randomness with each question. 
> 
> But my only question remains is: What if the opponent answerer straight up denies and lies or in someway lacks understanding of the questioner LLM? Or starts hallucinating?
> 
> If the answerer LLM is from the hosts, it would have been equal grounds for all questioner LLMs. If not, the power is shifted a lot towards the answerer LLM. 
> 
> Maybe we will have more clarity later on
> 
> 
> 
> > ## Khoi NguyenTopic Author
> > 
> > I mean "specific person, place, or thing" may as well mean "any arbitrary thing", you will need some prior knowledge to narrow it down somehow.
> > 
> > 
> > 
> > > ## G John Rao
> > > 
> > > And we do that by crafting our first question. After we get answer to our first question, the secret won't be as arbitrary as it began with. 
> > > 
> > > 
> > > 


---



</div>
<div class="column-right">

# 日本語訳

# 最適戦略（LLMは二分探索に勝てるのか？）
**Khoi Nguyen** *2024年5月17日 21:29:31 日本標準時* (8票)
考えてみた実験です。このゲームの専門家ではありませんが、私が集めた情報から理解したことを述べます。可能な答えが有限なプールにある場合、かつ正しい答えが完全にランダムであると仮定すると、各質問で残りのプールを半分に分けることが最適な戦略のようです。
完璧な分割を達成し、回答エージェントが結果を幻想していないことを確認するためには、次のようなルールベースのアプローチが最善です：
- 質問：このリスト<答えのプール>に答えはありますか？もし「いいえ」と答えたら、フリースタイルモードに切り替えてLLMの神に祈ります。
「はい」と答えた場合：
- 質問：このリスト<残りの答えのプールの半分>に答えはありますか？
- 「はい」か「いいえ」かの答えを取得します。これは、みんなが同意して特定の質問形式を使用する場合、正しいと保証されます。
- ステップ2を繰り返し、最後に1つの答えが残るまで続けます。
キーワード.pyファイルを見てみると、プライベートテスト用の多くの国、都市、ランドマークの可能性のあるプールをクロールすることが確実に可能です（もしそのランドマークがあまりにもマイナーであれば、LLMsがそれについて十分な情報を持っていないと考えられます）。
このアプローチに対してLLMsが提供するエッジは何でしょうか？もし答えが既知のLLMによって選ばれたものであれば、それは私たちが利用できる先行知識ですが、完全にランダムな場合はどうでしょうか？
私が引用した情報は、Geminiが教えてくれたこちらです：[https://www.cns.nyu.edu/~reuben/blog/20-questions-info-theory/](https://www.cns.nyu.edu/~reuben/blog/20-questions-info-theory/)
注意：もし答えのプールがクロールできないか、準無限（すべての可能な英単語）であっても、このアプローチは依然として強力です。「その単語の最初の文字はこのリストにありますか？ […]」のように尋ねれば良いのです。

---
 # コメント
> ## Bovard Doerschuk-Tiberi
> 
> 最終提出期限後に可能な単語のリストは変更されます（そのため、新しいリストでエージェントを更新することはできません）。可能な単語のリストをハードコーディングするような戦略は強くお勧めしません。
> 
> 最終評価終了時刻は2024年8月13日です。この時点で提出物はロックされます。2024年8月13日から8月27日までの期間中、新しい未発表の秘密の単語セットに対してエピソードを実施し続けます。この期間中は、アクティブな3つの提出物のみがリーダーボードの対象となります。この期間の終わりに、リーダーボードが確定します。
> 
> ---
> 
> ## chris
> 
> 私も似たような考えを持っていました。質問に2000文字の制限があるため、「このリストに答えはありますか？」のような質問はできませんが、固定リストの可能な値を持ち、何らかの二分探索を行うのは良いアプローチのようです。
> 
> 2^20 = 1,048,576
> 
> したがって、すべての分割をちょうど50%で行ければ、約100万のものをリストを通じて進めることができます。
> 
> しかしこのアプローチを採る場合、その答えが自身のリストに入っていることを祈らないといけません！プライベートセッションでの単語の種類についてもっと情報が与えられないと厳しいかもしれません。
> 
> 編集：ああ、たしかに、単語を推測するために1回の質問は必要ですよね？その場合、最大で2^19 = 524,288の単語までが対象になります。
> 
> > ## Khoi NguyenTopic Author
> > 
> > プライベートセットの単語に関する情報が何も与えられない場合、それを推測することは可能でしょうか？あなたが言ったように、二分探索の方法が完璧に機能するなら、検索空間を2^19回だけ狭めることができます。それ以上は完全に運に頼ることになります。
> 
> > > ## chris
> > > 
> > > 英語には約90,000の名詞がありますが、おそらく彼らはそのフルリストを使用せずに、最も一般的なトップNから選ぶと思われます。
> 
> > > 各地名や人名もさらに多く存在しますが、やはり最も有名なものだけを取り上げるでしょう。
> 
> > > だからこの問題をこのように解決するためのコツは、どこでカットオフをしぼるかですね。
> > > 
> > > ---
> > > 
> > > ## Khoi NguyenTopic Author
> > > 
> > > そうですね、最も人気のあるものをトップNと仮定するのは良い考えなので、プライベートセットでは早く予測するか成功する確率を高めるかというリスクとリワードの問題になります。そして、ホストが選んだ単語と近いNを持つ人が勝つことになるでしょう。
> > > 
> > > ---
> > > 
> > > 
---
> ## G John Rao
> 
> 「質問：このリストに答えはありますか？もし答えがないならフリースタイルモードに切り替えてLLMの神に祈る」というのは、このコンペティションの意義そのものではないと思います。
> 
> 概要から見ると：
> 
> このコンペティションでは、LLMsの演繹的推論、ターゲットを絞った質問を通じた効率的情報収集、およびペアとなったエージェント間のコラボレーションといった重要なスキルが評価されます。限られた数の推測で成り立つ制約のある設定は、創造性と戦略性が求められます。成功することで、LLMsはただ質問に答えるだけでなく、洞察に満ちた質問をし、論理的な推論を行い、迅速に可能性を絞り込む能力を示すことになります。
> 
> keywords.pyには、国、都市、ランドマークの3つのカテゴリがあります。
> 
> ですが、これら3つに限定されているとは思いません。もしそうであれば、コンペティションはつまらなくなります。
> 
> スターターノートブックにはシステムプロンプトが含まれています：
> 
> system_prompt = "あなたは20の質問ゲームをプレイするために設計されたAIアシスタントです。このゲームでは、答えがキーワードを考え、質問者からのはい・いいえの質問に答えます。このキーワードは、特定の人、場所、または物です。"
> 
> 人や場所についてはリストを作ることができますが、「物」のためにリストを作るのは意味がないと思います。「物」は本当に何でもありえます。名詞、概念、物体、アイデア、感情、さらには抽象的な存在まであり得ます。ここが面白いところで、LLMsの出番です。
> 
> "LLMsがこのアプローチに対してどのような優位性を持っているのでしょうか？もしかして答えが既知のLLMによって選ばれた場合、利用できる先行知識があるけれど、完全にランダムな場合はどうなるのか？"
> 
> 私は、秘密の単語はランダムである必要があると思います。そして、すべての参加者が質問を通じてそのランダム性を排除しようとします。
> 
> しかし私の唯一の疑問は、相手の回答者が素直に否定したり、質問者のLLMを理解できなかったり、または幻覚を起こした場合はどうなるのかということです。
> 
> ホストからの回答者LLMが使用されている場合、すべての質問者LLMにとって均等な条件になります。そうでない場合、回答者LLMが非常に有利になります。
> 
> おそらく、後ほどより明確な説明が得られるでしょう。
> 
> > ## Khoi NguyenTopic Author
> > > 私は「特定の人、場所、または物」というのは「任意のもの」とも言えると思います。何かを狭めるためには、いくらかの前提知識が必要です。
> > > 
> > > > ## G John Rao
> > > > 
> > > それは、最初の質問を作成することで実現します。最初の質問の答えを得ると、秘密は最初に思ったほどランダムではなくなります。
> > > > 
> > > > 
---


</div>