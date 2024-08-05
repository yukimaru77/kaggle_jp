# 要約 
ディスカッションでは、Microsoft Research Asiaの研究者たちが「GameEval」というLLMを用いた会話ゲームの評価手法に関する情報を紹介しています。このゲームでは、質問者と回答者が協力して進められ、質問者は回答者に対して1つの質問を行い、回答者は与えられた単語を基に誠実に応答する必要があります。ただし、回答者の応答には提供された単語やフレーズを含めてはいけません。ゲームの目的は、質問者が与えられた単語を正確に推測するためのQ&Aラウンド数をできるだけ少なくすることです。質問者は、回答者の反応をもとに絞り込む質問を行い、最終的に正しい単語を特定し、「Gameover」と応答することでゲームを終了します。論文へのリンクも提供されています。

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

# Found something similar to the competition from Microsoft Research Asia researchers. 

**AC** *Thu May 16 2024 16:38:55 GMT+0900 (日本標準時)* (7 votes)

[GameEval: Evaluating LLMs on Conversational Games](https://github.com/jordddan/GameEval)

Ask-Guess is a cooperative game involving a questioner and an answerer. At the beginning of the game, the answerer receives a word unknown to the questioner. In each round, the questioner may ask the answerer one question, and the answerer has to answer faithfully. The provided word or phrase must not be included in the answerer’s reply. Both participants should collaborate to minimize the number of Q&A rounds needed for the questioner to deduce the given word or phrase accurately. The questioner should ask targeted questions to progressively narrow down the potential scope of the given word based on the answerer’s responses. The answerer must assess whether the questioner has successfully identified the word and respond with ’Gameover’ to conclude the game [Taken from the git-hub repo].

Link to the paper : [GameEval: Evaluating LLMs on Conversational Games](https://arxiv.org/pdf/2308.10032v1)





</div>
<div class="column-right">

# 日本語訳

> Microsoft Research Asiaの研究者たちによる、コンペティションに似たものを見つけました。
**AC** *2024年5月16日 木曜日 16:38:55 JST* (7票)
[GameEval: LLMを会話ゲームで評価する](https://github.com/jordddan/GameEval)
Ask-Guessは、質問者と回答者が協力して進めるゲームです。ゲームの初めに、回答者には質問者が知らない単語が与えられます。各ラウンドで、質問者は回答者に1つの質問をすることができ、回答者は誠実に応答しなければなりません。この時、提供された単語やフレーズは、回答者の返答に含めてはいけません。両者は協力して、質問者が与えられた単語やフレーズを正確に推測するために必要なQ&Aのラウンド数を最小限に抑えることを目指します。質問者は、回答者の反応に基づいて、与えられた単語の可能性を徐々に絞り込むために的を絞った質問をする必要があります。回答者は、質問者が正しく単語を特定したかどうかを評価し、ゲームを終了するために「Gameover」と応答しなければなりません[GitHubリポジトリからの引用]。
論文へのリンク: [GameEval: LLMを会話ゲームで評価する](https://arxiv.org/pdf/2308.10032v1)


</div>