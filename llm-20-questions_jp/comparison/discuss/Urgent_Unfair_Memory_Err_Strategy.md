# 要約 
ディスカッションでは、ユーザー「CchristoC」が、エージェントがエラーを起こすと他の3つのエージェントにポイントが与えられる不公平な戦略について警告しています。この状況は、エージェントが長いプロンプトを使用して質問することで、回答者のエージェントのメモリが不足しエラーを引き起こさせ、結果的に他のエージェントにプラスのポイントを付与することにつながります。CchristoCは、エラーが発生した場合はそのエージェントのみにマイナスのポイントを与えるべきだと提案しています。

他のユーザーからは、これに関して過去にも議論があったことや、エージェントは自身の限界を理解し責任を持つべきであるとの意見が寄せられています。また、「Coldstart Coder」が自分のエージェントが同様の問題を起こさないように対策を講じる必要があることに言及しています。全体として、エージェントのメモリ管理やルール変更の必要性が議題に上っています。

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

# Urgent: Unfair Memory Err Strategy

**CchristoC** *Tue Jul 09 2024 13:20:08 GMT+0900 (日本標準時)* (6 votes)

I found that if someone's agent gets an Err, all the other 3 Agents will get a + Point.

This can be misused by questioner prompting as much words as possible (lengthy prompts), so that if the answerer's agent has less available memory, it will result in an Err and all points will be given to the other 3 agents, while the Err agent get a - point.

Even if they all didn't guess the correct keyword.

This strategy is vulnerable to those who don't have a condition to give a backup answer when there is no output from the agent, especially for those who are using big size LLMs and lengthy answerer prompt too.

Should be fixed by not giving + points to the other 3 if an agent gets an Err. (Only - point to the Err agent.)



---

 # Comments from other users

> ## Chris Deotte
> 
> This was discussed [here](https://www.kaggle.com/competitions/llm-20-questions/discussion/508415) and other threads.
> 
> 
> 
> > ## CchristoCTopic Author
> > 
> > But it's still not fixed yet?
> > 
> > 
> > 
> > > ## RS Turley
> > > 
> > > I don't see an issue. The rules are pretty clear that a question can be up to 2000 characters. Each agent should be responsible not to run out of time or memory. 
> > > 
> > > 
> > > 
> > > ## Chris Deotte
> > > 
> > > 
> > > But it's still not fixed yet?
> > > 
> > > The non-error teams used to receive like +150 points! It is much better than it was.
> > > 
> > > 
> > > 


---

> ## Coldstart Coder
> 
> Thanks for the heads up, will need to put in safe guards for my own agents to make sure it doesn't error out like that.
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# 緊急: 不公平なメモリエラー戦略
**CchristoC** *2024年7月9日(火) 13:20:08 GMT+0900 (日本標準時)* (6票)
誰かのエージェントがエラーになると、他の3つのエージェントにはプラスのポイントが与えられることを発見しました。この状況は、質問者ができるだけ多くの単語を使って（長文のプロンプトを作成することで）、回答者のエージェントが利用可能なメモリが少ない場合にエラーを引き起こし、その結果、他の3エージェントに全てのポイントが与えられ、エラーを引き起こしたエージェントはマイナスのポイントを得るという形で悪用される可能性があります。
たとえ彼ら全員が正しいキーワードを推測できなくてもです。この戦略は、エージェントからの出力がない場合にバックアップの回答を行う条件を持たない者にとって特に脆弱です。特に、大きなサイズのLLMや長い回答プロンプトを使用している人々にとってはそうです。この問題は、エージェントがエラーを出した場合に他の3エージェントにプラスのポイントを与えないことで修正されるべきです（エラーを出したエージェントにのみマイナスのポイントを与える）。

---
 # 他のユーザーからのコメント
> ## Chris Deotte
> 
> これは[こちら](https://www.kaggle.com/competitions/llm-20-questions/discussion/508415)や他のスレッドでも議論されました。
> 
> > ## CchristoCTopic 作成者
> > 
> > でも、まだ修正されていないのですか？
> > 
> > > ## RS Turley
> > > 
> > > 問題だとは思いません。ルールは2000文字までの質問ができると明確に示しています。各エージェントは、時間やメモリが足りなくならないように責任を持つべきです。
> > > 
> > > > ## Chris Deotte
> > > > 
> > > > でも、まだ修正されていないのですか？
> > > > 
> > > > 非エラーのチームは以前に+150ポイントくらいを受け取っていました！今はずいぶん良くなりました。
> > > > 
> > > > 
---
> ## Coldstart Coder
> 
> 情報提供ありがとうございます。自分のエージェントがそのようにならないように安全策を講じる必要がありますね。


</div>