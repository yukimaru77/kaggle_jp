# 要約 
このディスカッションは、Kaggleの「LLM 20 Questions」コンペティションにおけるルールベースのアルゴリズムの使用について議論しています。

**問題点:**

* 一部の参加者は、ルールベースの質問と回答のプロトコルを利用して、LLMが回答できないような質問を生成しています。
* これらのプロトコルは、特定のキーワードや文字列の出現に基づいて回答を予測できるため、LLMの能力を回避し、コンペティションの公平性を損なう可能性があります。

**提案:**

* ディスカッションの投稿者は、リーダーボードで観察されたルールベースの質問の例をいくつか挙げ、それらにどのように答えるかを示しています。
* これらの質問は、キーワードのアルファベット順、最初の文字、特定の文字の包含など、特定のルールに基づいています。
* 投稿者は、これらの質問に答えるためのPython関数を提供し、回答パイプラインに挿入することで、LLMがこれらの質問に正しく答えることができるようにしています。

**他のユーザーからのコメント:**

* loh-maaは、投稿者の提案された解決策は、すべてのルールベースのプロトコルを処理する最善の方法ではないと指摘しています。
* loh-maaは、投稿者の正規表現が非常に厳格であり、最初の質問にも依存していることを指摘しています。

**結論:**

このディスカッションは、コンペティションの公平性を維持するために、ルールベースのアルゴリズムの使用を制限する必要があることを示しています。投稿者は、ルールベースの質問を特定し、それらに答えるための方法を提供することで、この問題に対処しようとしています。しかし、他のユーザーは、投稿者の解決策が完全ではないことを指摘しています。


---
# リーダーボードで見られるルールベースのアルゴリズムで答えられる質問のリスト

**c-number** *2024年6月30日 14:01:40 GMT+0900 (日本標準時)* (5 votes)

# (考察)

ルールベースの質問/回答プロトコルによる秘密の共謀は、コンペティションの目標に反しますが、上位エージェントのプレイバックをいくつか確認した結果、これらのプロトコルが（自発的に、意図的なものではありませんが）リーダーボードを支配するのは時間の問題のように思えます。

[@lohmaa](https://www.kaggle.com/lohmaa) が [こちら](https://www.kaggle.com/competitions/llm-20-questions/discussion/511343#2866948) で指摘したように、一部のプレイヤーだけがプロトコルを知っている場合、それは不公平です。なぜなら、彼らが一緒にペアを組む際に、彼らの勝利率を高めることになるからです。

そのため、状況をより公平にするために、リーダーボードで観察されたプロトコルのような質問をいくつかリストすることにしました。

もちろん、私はこの状況が望ましいとは思っていませんが、このアプローチは少なくとも状況をより公平にすると思います。

ランダムに割り当てられたLLM（例：Llama 3、Llama 2、Gemma）と常にチームを組むことを義務付けるルールに変更すれば、LLMをプレイに維持できるかもしれません。[ref](https://www.kaggle.com/competitions/llm-20-questions/discussion/511343#2866948)

# これは何ですか？

上位エージェントのプレイバックを観察すると、一部のエージェントはルールベースのアルゴリズムを使用して回答できる質問を利用していることに気づきます。

[こちら](https://www.kaggle.com/competitions/llm-20-questions/discussion/515751) で指摘されているように、一部のキーワードは、LLMが回答するのはほぼ不可能です（少なくとも20問以内では、どのような質問をすればLLMは「サイプレスの膝」を推測できるでしょうか？）。そのため、ルールベースの質問の方が魅力的です。

（キーワードのリストが不明な場合、ルールベースの質問をするのは最善の選択ではないかもしれませんが、少なくとも回答者にとっては、質問に正しく答えることが常に最適な戦略です。）

ここでは、リーダーボードで観察された質問をいくつか紹介し、それらにどのように答えるかを示します。

# 質問

キーワード（小文字）はアルファベット順で「レーザー」の前に来ますか？ [ref](https://www.kaggle.com/competitions/llm-20-questions/leaderboard?dialog=episodes-episode-55219628)

キーワードは「m」で始まりますか？ [ref](https://www.kaggle.com/competitions/llm-20-questions/leaderboard?dialog=episodes-episode-55203947)

キーワードは「Z」、「G」、または「V」のいずれかの文字で始まりますか？ [ref](https://www.kaggle.com/competitions/llm-20-questions/leaderboard?dialog=episodes-episode-55196291)

キーワードは次のいずれかですか？ GPS、グラフ電卓、ゴミ収集車、ゴルフカート、生ゴミ処理機、重力、手袋、ガスマスク、ゴミ袋、警備塔？ [ref](https://www.kaggle.com/competitions/llm-20-questions/leaderboard?dialog=episodes-episode-55196291)

キーワードの名前のすべての文字を考慮すると、キーワードの名前には「N」という文字が含まれていますか？ [ref](https://www.kaggle.com/competitions/llm-20-questions/leaderboard?dialog=episodes-episode-55209104)

# 回答方法

以下の関数は、質問に正しく答えることができる場合はTrue/Falseを返し、できない場合はNoneを返します。そのため、質問をLLMに渡す直前に、回答パイプラインに挿入するだけです。

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

Kaggleを楽しんで！
---

# 他のユーザーからのコメント

> ## loh-maa
> 
> はい、あなたは正しいと思います。しかし、技術的には、「アルファ」プロトコルを処理する最善の方法ではありません。テストワードが二重引用符で囲まれていて、回答者が最初の質問を確認した場合、構文はそれほど重要ではありません。他のプロトコルについてはよく知りませんが、これらの正規表現は非常に厳格に見えます。また、最初の質問にも依存していると思います。「20の質問をしていますか？」のような質問をする。
> 
> 
> 
---

