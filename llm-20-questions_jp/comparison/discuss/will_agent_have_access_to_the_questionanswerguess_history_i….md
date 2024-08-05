# 要約 
このディスカッションでは、コンペティションに参加するエージェントの機能についての質問が中心となっています。参加者のHaolx0824がエージェントが各セッションの質問や回答、推測履歴にアクセスできるかどうかを尋ねています。

Chris DeotteとMatthew S Farmerが応じ、エージェントは全履歴を受け取ることができ、これはobs辞書に含まれていることを説明しています。具体的な例として、過去の質問や回答、推測の履歴が示され、エージェントがそれを利用して推測を行うことができると述べています。ただし、履歴を活用する際の難しさについても触れられており、特に不十分な回答をするエージェントとペアになる状況が課題であることが指摘されています。

さらに、Haolx0824が「keyword」がobs辞書に含まれていることについて、質問者がそれにアクセスできないような対策が取られているのかを確認すると、Bovard Doerschuk-Tiberiがそれに対し、質問者はそのキーワードを確認できないことを確認しています。

全体として、エージェントの履歴の利用とその限界、またそれに関連するルールについての確認が行われたディスカッションです。

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

# will agent have access to the question/answer/guess history in each session?

**Haolx0824** *Thu Jun 20 2024 11:00:12 GMT+0900 (日本標準時)* (1 votes)

will agent have access to the question/answer/guess history in each session?



---

 # Comments from other users

> ## Chris Deotte
> 
> Yes, our agent receives the entire history. It is contained in the obs dictionary. Here is an example of the dictionary's values for an agent that just randomly asks questions. This is the obs dictionary during somewhere around round 16:
> 
> obs = {'remainingOverageTime': 300, 'questions': ['Is it equatorial guinea?', 'Is it lyon france?', 'Is it hermosillo mexico?', 'Is it malta?', 'Is it belarus?', 'Is it porto portugal?', 'Is it istanbul turkey?', 'Is it dallas texas?', 'Is it orlando florida?', 'Is it caracas venezuela?', 'Is it libya?', 'Is it zunyi china?', 'Is it mexico city mexico?', 'Is it london england?', 'Is it osaka japan?', 'Is it enugu nigeria?'], 'guesses': ['kathmandu nepal', 'slovenia', 'dhaka bangladesh', 'switzerland', 'guwahati india', 'athens georgia', 'bahrain', 'kyrgyzstan', 'guadalajara mexico', 'madrid spain', 'antwerp belgium', 'uzbekistan', 'tirana albania', 'york england', 'essentuki russia'], 'answers': ['no', 'no', 'no', 'no', 'no', 'no', 'no', 'no', 'no', 'no', 'no', 'no', 'no', 'no', 'no'], 'role': 'answerer', 'turnType': 'answer', 'keyword': 'jabalpur india', 'category': 'city', 'step': 46}
> 
> 
> 
> > ## Matthew S Farmer
> > 
> > 
> > Yes, our agent receives the entire history. It is contained in the obs dictionary. Here is an example of the dictionary's values for an agent that just randomly asks questions. This is the obs dictionary during somewhere around round 16:
> > 
> > obs = {'remainingOverageTime': 300, 'questions': ['Is it equatorial guinea?', 'Is it lyon france?', 'Is it hermosillo mexico?', 'Is it malta?', 'Is it belarus?', 'Is it porto portugal?', 'Is it istanbul turkey?', 'Is it dallas texas?', 'Is it orlando florida?', 'Is it caracas venezuela?', 'Is it libya?', 'Is it zunyi china?', 'Is it mexico city mexico?', 'Is it london england?', 'Is it osaka japan?', 'Is it enugu nigeria?'], 'guesses': ['kathmandu nepal', 'slovenia', 'dhaka bangladesh', 'switzerland', 'guwahati india', 'athens georgia', 'bahrain', 'kyrgyzstan', 'guadalajara mexico', 'madrid spain', 'antwerp belgium', 'uzbekistan', 'tirana albania', 'york england', 'essentuki russia'], 'answers': ['no', 'no', 'no', 'no', 'no', 'no', 'no', 'no', 'no', 'no', 'no', 'no', 'no', 'no', 'no'], 'role': 'answerer', 'turnType': 'answer', 'keyword': 'jabalpur india', 'category': 'city', 'step': 46}
> > 
> > This has been an interesting topic on my mind. I have utilized history in my script but since our agents are teamed with an agent that could answer incorrectly/poorly a history may or may not be helpful to guess the keyword. For example in Chris's output, the agent could ask "Is it a place?" and the answerer agent could say "no" which would make attempting deductive logic difficult. This has been a fun and challenging competition! 
> > 
> > 
> > 
> > > ## Haolx0824Topic Author
> > > 
> > > Thanks Chris and Matthew - the fact that we can't rely on deductive logic is making this competition harder (if you are unlucky and get paired with a bad answerer, then no much you can do…)
> > > 
> > > Another basic question - since 'keyword' is in the obs dictionary, did you guys make sure that the Questioner cannot access that by any mean? Thanks!
> > > 
> > > 
> > > 
> > > ## Bovard Doerschuk-Tiberi
> > > 
> > > Correct, the Questioner cannot see the keyword. Each agent has its own observation.
> > > 
> > > 
> > > 
> > > ## Haolx0824Topic Author
> > > 
> > > Thanks for confirming.
> > > 
> > > 
> > > 
> > ## KKY
> > 
> > Very detailed explanation,  even examples,  thanks! chris.
> > 
> > 
> > 


---



</div>
<div class="column-right">

# 日本語訳

# エージェントは各セッションの質問/回答/推測履歴にアクセスできますか？
**Haolx0824** *2024年6月20日(木) 11:00:12 GMT+0900 (日本標準時)* (1票)
エージェントは各セッションの質問/回答/推測履歴にアクセスできますか？
---
 # 他のユーザーからのコメント
> ## Chris Deotte
> 
> はい、私たちのエージェントは全履歴を受け取ります。これはobs辞書に含まれています。こちらは、ランダムに質問をするエージェントのための辞書の例で、ラウンド16のどこかにおけるobs辞書の値です：
> 
> obs = {'remainingOverageTime': 300, 'questions': ['それは赤道ギニアですか？', 'それはフランスのリヨンですか？', 'それはメキシコのエルモシージョですか？', 'それはマルタですか？', 'それはベラルーシですか？', 'それはポルトガルのポルトですか？', 'それはトルコのイスタンブールですか？', 'それはテキサスのダラスですか？', 'それはフロリダのオーランドですか？', 'それはベネズエラのカラカスですか？', 'それはリビアですか？', 'それは中国の遵義ですか？', 'それはメキシコシティですか？', 'それはイギリスのロンドンですか？', 'それは日本の大阪ですか？', 'それはナイジェリアのエヌグですか？'], 'guesses': ['ネパールのカトマンズ', 'スロベニア', 'バングラデシュのダッカ', 'スイス', 'インドのグワハティ', 'ジョージア州のアテネ', 'バーレーン', 'キルギスタン', 'メキシコのグアダラハラ', 'スペインのマドリード', 'ベルギーのアントワープ', 'ウズベキスタン', 'アルバニアのティラナ', 'イングランドのヨーク', 'ロシアのエセンツキ'], 'answers': ['いいえ', 'いいえ', 'いいえ', 'いいえ', 'いいえ', 'いいえ', 'いいえ', 'いいえ', 'いいえ', 'いいえ', 'いいえ', 'いいえ', 'いいえ', 'いいえ', 'いいえ'], 'role': 'answerer', 'turnType': 'answer', 'keyword': 'インドのジャバルプール', 'category': '都市', 'step': 46}
> 
> > ## Matthew S Farmer
> > 
> > はい、私たちのエージェントは全履歴を受け取ります。これはobs辞書に含まれています。こちらは、ランダムに質問をするエージェントのための辞書の例で、ラウンド16のどこかにおけるobs辞書の値です：
> > 
> > obs = {'remainingOverageTime': 300, 'questions': ['それは赤道ギニアですか？', 'それはフランスのリヨンですか？', 'それはメキシコのエルモシージョですか？', 'それはマルタですか？', 'それはベラルーシですか？', 'それはポルトガルのポルトですか？', 'それはトルコのイスタンブールですか？', 'それはテキサスのダラスですか？', 'それはフロリダのオーランドですか？', 'それはベネズエラのカラカスですか？', 'それはリビアですか？', 'それは中国の遵義ですか？', 'それはメキシコシティですか？', 'それはイギリスのロンドンですか？', 'それは日本の大阪ですか？', 'それはナイジェリアのエヌグですか？'], 'guesses': ['ネパールのカトマンズ', 'スロベニア', 'バングラデシュのダッカ', 'スイス', 'インドのグワハティ', 'ジョージア州のアテネ', 'バーレーン', 'キルギスタン', 'メキシコのグアダラハラ', 'スペインのマドリード', 'ベルギーのアントワープ', 'ウズベキスタン', 'アルバニアのティラナ', 'イングランドのヨーク', 'ロシアのエセンツキ'], 'answers': ['いいえ', 'いいえ', 'いいえ', 'いいえ', 'いいえ', 'いいえ', 'いいえ', 'いいえ', 'いいえ', 'いいえ', 'いいえ', 'いいえ', 'いいえ', 'いいえ', 'いいえ'], 'role': 'answerer', 'turnType': 'answer', 'keyword': 'インドのジャバルプール', 'category': '都市', 'step': 46}
> > 
> > このトピックは非常に興味深いです。私は自分のスクリプトで履歴を活用しましたが、私たちのエージェントは間違った/不十分な回答をするエージェントとチームを組んでいるため、履歴がキーワードを推測するのに役立つかどうかが不確かです。たとえば、Chrisの出力では、エージェントが「それは場所ですか？」と尋ねることができ、回答者エージェントが「いいえ」と答えると、演繹的論理を試みるのが難しくなります。このコンペティションは楽しく、挑戦的です！
> > 
> > > ## Haolx0824トピック作成者
> > > 
> > > Chrisさん、Matthewさん、ありがとうございます。演繹的論理に依存できない事実が、このコンペティションをより難しくしていますね（もし不運にも悪い回答者とペアになってしまったら、どうしようもない…）
> > > 
> > > もう一つ基本的な質問ですが、「keyword」がobs辞書に含まれているので、質問者がそれにアクセスできないように対策を講じていますか？ありがとうございます！
> > > 
> > > > ## Bovard Doerschuk-Tiberi
> > > 
> > > 正しいです。質問者はキーワードを見れません。各エージェントにはそれぞれ独自の観察があります。
> > > 
> > > > ## Haolx0824トピック作成者
> > > 
> > > 確認してくれてありがとうございます。
> > > 
> > > > ## KKY
> > > 
> > > 詳細な説明、例までありがとうございます！Chrisさん。
> > > 
> > > 
>


</div>