# 要約 
このディスカッションは、Kaggleの「LLM 20 Questions」コンペティションにおけるルールベースの質問に関する考察を扱っています。投稿者は、ルールベースのアルゴリズムを用いた質問が一部のエージェントに有利となり、フェアでない競争条件を生み出していることを懸念し、いくつかの具体的な質問例を示しました。これにより、ルールに則った質問がトップエージェントによって有効に活用されている現象への対策として、状況を公平にするための提案をしています。

参加者は、ルールベースの質問が魅力的になる理由として、特定のキーワードがLLMによって回答困難であることを指摘しています。また、全体的な提案として、LLMの割り当てをランダムに行うルール変更が提案されています。質問例と、それに対する回答用の関数も含まれており、これが解答プロセスにどのように組み込まれるかについて説明されています。

コメント欄では、他の参加者が提案されたアプローチの限界について指摘し、議論が展開されています。全体的に、より公平なゲームプレイを実現するための努力が垣間見えます。

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

# List of questions seen on the LB that can be answered with a rule-based algorithm.

**c-number** *Sun Jun 30 2024 14:01:40 GMT+0900 (日本標準時)* (5 votes)

# (Thoughts)

While the secret collusion of a rule-based question/answer protocol goes against the goal of the competition, after reviewing some of the replays of top agents, it seems to me that it is only a matter of time before they (spontaneously, no offense intended) come to dominate the LB.

As pointed out by [@lohmaa](https://www.kaggle.com/lohmaa) [here](https://www.kaggle.com/competitions/llm-20-questions/discussion/511343#2866948), it would be unfair if only some of the players were aware of the protocol, as this would enhance their winning rate when they pair up together.

Therefore, I have decided to list some of the protocol-like questions that have been observed on the leaderboard, in order to make the situation more fair.

Of course, I do not believe this situation is desirable, but I think this approach at least makes the situation more fair.

Perhaps changing the rules to always require players to team up with a randomly assigned LLM (e.g. Llama 3, Llama 2, Gemma) would keep LLM in play? [ref](https://www.kaggle.com/competitions/llm-20-questions/discussion/511343#2866948)

# What is this?

Observing the replays of top agents, one notices that some agents utilize questions that can be answered using a rule-based algorithm.

As pointed out [here](https://www.kaggle.com/competitions/llm-20-questions/discussion/515751), some things keywords seem to be almost impossible to be answered by a LLM (at least within 20 questions, what questions could make a LLM guess "Cypress knee"?), making rule-based question more engaging.

(Asking rule-based questions might not be the best choice when the list of keywords is unknown, but at least for the answerer, answering correctly to the question is always the optimal strategy.)

Here, I will introduce some of the questions that have been observed on the leaderboard, and also demonstrate how to answer them.

# Questions

Does the keyword (in lowercase) come before "laser" in alphabetical order?" [ref](https://www.kaggle.com/competitions/llm-20-questions/leaderboard?dialog=episodes-episode-55219628)
Does the keyword begins with the letter "m"? [ref](https://www.kaggle.com/competitions/llm-20-questions/leaderboard?dialog=episodes-episode-55203947)
Does the keyword start with one of the letters 'Z', 'G' or 'V'? [ref](https://www.kaggle.com/competitions/llm-20-questions/leaderboard?dialog=episodes-episode-55196291)
Is the keyword one of the following? GPS, Graphing Calculator, Garbage Truck, Golf Cart, Garbage Disposal, Gravity, Glove, Gas Mask, Garbage bag, Guard tower? [ref](https://www.kaggle.com/competitions/llm-20-questions/leaderboard?dialog=episodes-episode-55196291)
Considering every letter in the name of the keyword, does the name of the keyword include the letter 'N'? [ref](https://www.kaggle.com/competitions/llm-20-questions/leaderboard?dialog=episodes-episode-55209104)

# How to answer

The function below returns True/False if the question can be answered correctly, and returns None if it cannot. So you can just insert it in your answering pipeline just before feeding the question to your LLM.

```
import re

def func1(keyword, question):
    keyword_pattern = r"^[a-zA-Z\s]+$"
    question_pattern = r'^Does the keyword \(in lowercase\) come before "([a-zA-Z\s]+)" in alphabetical order\?$'
    if not re.match(keyword_pattern, keyword) or not re.match(
        question_pattern, question
    ):
        return None
    match = re.match(question_pattern, question)
    compare_word = match.group(1)
    return keyword.lower() < compare_word.lower()

def func2(keyword, question):
    keyword_pattern = r"^[a-zA-Z\s]+$"
    question_pattern = r'^Does the keyword begins with the letter "([a-zA-Z])"\?$'

    if not re.match(keyword_pattern, keyword) or not re.match(
        question_pattern, question
    ):
        return None

    match = re.match(question_pattern, question)
    search_letter = match.group(1)

    return keyword.strip().lower().startswith(search_letter.lower())

def func3(keyword, question):
    keyword_pattern = r"^[a-zA-Z\s]+$"
    question_patterns = [
        r"^Does the keyword start with one of the letters \'([a-zA-Z]\'(?:, \'[a-zA-Z]\')*)(?: or \'[a-zA-Z]\')?\?$",
        r"^Does the keyword start with the letter \'([a-zA-Z])\'\?$",
    ]
    if not re.match(keyword_pattern, keyword) or not any(
        re.match(pattern, question) for pattern in question_patterns
    ):
        return None
    if re.match(question_patterns[0], question):
        letters = re.findall(r"'([a-zA-Z])'", question)
    else:
        match = re.match(question_patterns[1], question)
        letters = [match.group(1)]
    letters = [c.lower() for c in letters]
    return keyword.strip()[0].lower() in letters

def func4(keyword, question):
    keyword_pattern = r"^[a-zA-Z\s]+$"
    question_pattern = r"^Is the keyword one of the following\? ([a-zA-Z\s,]+)\?$"
    if not re.match(keyword_pattern, keyword) or not re.match(
        question_pattern, question
    ):
        return None
    match = re.match(question_pattern, question)
    options = [option.strip() for option in match.group(1).split(",")]
    return keyword.strip().lower() in [option.lower() for option in options]

def func5(keyword, question):
    keyword_pattern = r"^[a-zA-Z\s]+$"
    question_pattern = r"^Considering every letter in the name of the keyword, does the name of the keyword include the letter \'([A-Za-z])\'\?$"
    if not re.match(keyword_pattern, keyword) or not re.match(
        question_pattern, question
    ):
        return None
    match = re.match(question_pattern, question)
    search_letter = match.group(1)
    return search_letter.lower() in keyword.lower()

def func(keyword, question):
    solves = [func1, func2, func3, func4, func5]
    for f in solves:
        result = f(keyword, question)
        if result is not None:
            return result
    return None

```

Happy Kaggling



---

 # Comments from other users

> ## loh-maa
> 
> Yes, I think you got it right. However, technically it's not the best way to handle the "alpha" protocol. The syntax doesn't matter much if only the testword is in double quotes and the answerer confirmed the 1st question. I don't know much about other protocols, but I think those regexes look very strict. Also, I think they also rely on the 1st question, asking something like "Are we playing 20 questions?"
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# ルールベースのアルゴリズムで答えられる質問のリスト
**c-number** *2024年6月30日(日) 14:01:40 JST* (5票)

# (考察)
ルールベースの質問/回答プロトコルがコンペティションの目的に反することは承知していますが、トップエージェントのリプレイを見直すと、時が経つにつれ（故意ではありませんが）彼らがリーダーボードを支配するのは時間の問題だと感じています。
[@lohmaa](https://www.kaggle.com/lohmaa)が指摘したように、プロトコルを知っているのが一部のプレイヤーだけであった場合、それが彼らの勝率を高めることになり、フェアではありません。
そのため、リーダーボードで観察されたプロトコルに似た質問をいくつか挙げて、状況をより公正にすることにしました。
もちろん、この状況が望ましいとは思いませんが、このアプローチが少なくとも状況をより公平にすると思います。
おそらく、プレイヤーがランダムに割り当てられたLLM（例：Llama 3、Llama 2、Gemma）と必ずチームを組むようにルールを変更すれば、LLMが影響を受けない状況を維持できるのではないでしょうか？ [ref](https://www.kaggle.com/competitions/llm-20-questions/discussion/511343#2866948)

# これは何ですか？
トップエージェントのリプレイを観察すると、一部のエージェントがルールベースのアルゴリズムで答えることができる質問を利用していることに気付きます。
[こちら](https://www.kaggle.com/competitions/llm-20-questions/discussion/515751)で指摘されているように、特定のキーワードはLLMによって答えることがほぼ不可能であり（少なくとも20の質問の中では、LLMに「Cypress knee」を推測させるような質問は何か？）、ルールベースの質問がより魅力的になります。
キーワードが未知である場合、ルールベースの質問をすることが最善の選択ではないかもしれませんが、少なくとも回答者にとってはその質問に正しく答えることが常に最適な戦略となります。
ここでは、リーダーボードで観察された質問をいくつか紹介し、それに答える方法も示します。

# 質問
- 「キーワード（小文字）は「laser」より前にアルファベット順で来ますか？」 [ref](https://www.kaggle.com/competitions/llm-20-questions/leaderboard?dialog=episodes-episode-55219628)
- 「キーワードは「m」から始まりますか？」 [ref](https://www.kaggle.com/competitions/llm-20-questions/leaderboard?dialog=episodes-episode-55203947)
- 「キーワードは「Z」、「G」または「V」のいずれかの文字で始まりますか？」 [ref](https://www.kaggle.com/competitions/llm-20-questions/leaderboard?dialog=episodes-episode-55196291)
- 「キーワードは以下のいずれかですか？ GPS、グラフ計算機、ゴミトラック、ゴルフカート、ゴミ処理、重力、手袋、ガスマスク、ゴミ袋、警備塔？」 [ref](https://www.kaggle.com/competitions/llm-20-questions/leaderboard?dialog=episodes-episode-55196291)
- 「キーワードの名前に含まれるすべての文字を考慮した場合、その名前に「N」文字は含まれていますか？」 [ref](https://www.kaggle.com/competitions/llm-20-questions/leaderboard?dialog=episodes-episode-55209104)

# 答え方
以下の関数は、正しく答えられる場合はTrueまたはFalseを返し、そうでない場合はNoneを返します。したがって、質問をLLMに提供する前の回答パイプラインに挿入すれば良いです。

```python
import re

def func1(keyword, question):
    keyword_pattern = r"^[a-zA-Z\s]+$"
    question_pattern = r'^Does the keyword \(in lowercase\) come before "([a-zA-Z\s]+)" in alphabetical order\?$'
    if not re.match(keyword_pattern, keyword) or not re.match(question_pattern, question):
        return None
    match = re.match(question_pattern, question)
    compare_word = match.group(1)
    return keyword.lower() < compare_word.lower()

def func2(keyword, question):
    keyword_pattern = r"^[a-zA-Z\s]+$"
    question_pattern = r'^Does the keyword begins with the letter "([a-zA-Z])"\?$'
    if not re.match(keyword_pattern, keyword) or not re.match(question_pattern, question):
        return None
    match = re.match(question_pattern, question)
    search_letter = match.group(1)
    return keyword.strip().lower().startswith(search_letter.lower())

def func3(keyword, question):
    keyword_pattern = r"^[a-zA-Z\s]+$"
    question_patterns = [
        r"^Does the keyword start with one of the letters \'([a-zA-Z]\'(?:, \'[a-zA-Z]\')*)(?: or \'[a-zA-Z]\')?\?$",
        r"^Does the keyword start with the letter \'([a-zA-Z])\'\?$",
    ]
    if not re.match(keyword_pattern, keyword) or not any(re.match(pattern, question) for pattern in question_patterns):
        return None
    if re.match(question_patterns[0], question):
        letters = re.findall(r"'([a-zA-Z])'", question)
    else:
        match = re.match(question_patterns[1], question)
        letters = [match.group(1)]
    letters = [c.lower() for c in letters]
    return keyword.strip()[0].lower() in letters

def func4(keyword, question):
    keyword_pattern = r"^[a-zA-Z\s]+$"
    question_pattern = r"^Is the keyword one of the following\? ([a-zA-Z\s,]+)\?$"
    if not re.match(keyword_pattern, keyword) or not re.match(question_pattern, question):
        return None
    match = re.match(question_pattern, question)
    options = [option.strip() for option in match.group(1).split(",")]
    return keyword.strip().lower() in [option.lower() for option in options]

def func5(keyword, question):
    keyword_pattern = r"^[a-zA-Z\s]+$"
    question_pattern = r"^Considering every letter in the name of the keyword, does the name of the keyword include the letter \'([A-Za-z])\'\?$"
    if not re.match(keyword_pattern, keyword) or not re.match(question_pattern, question):
        return None
    match = re.match(question_pattern, question)
    search_letter = match.group(1)
    return search_letter.lower() in keyword.lower()

def func(keyword, question):
    solves = [func1, func2, func3, func4, func5]
    for f in solves:
        result = f(keyword, question)
        if result is not None:
            return result
    return None
```
楽しいKagglingを！

---
 # 他のユーザーからのコメント
> ## loh-maa
> 
> はい、あなたは正しいと思います。しかし、技術的には「アルファ」プロトコルを扱う最善の方法ではありません。構文はそれほど重要ではありません。テストワードが二重引用符で囲まれ、回答者が最初の質問を確認した場合、あまり意味がありません。ここでは他のプロトコルについてあまり知識はありませんが、これらの正規表現は非常に厳密だと思います。また、彼らは最初の質問にも依存していると思います。「我々は20の質問をプレイしていますか？」のような質問です。
> 
> ---


</div>