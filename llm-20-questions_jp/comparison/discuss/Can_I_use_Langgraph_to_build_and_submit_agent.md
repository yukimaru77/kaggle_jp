# 要約 
ディスカッションでは、ユーザーのBikash PatraがLanggraphやLangchainを使用してエージェントを作成・提出できるかどうかを尋ねています。これは、他のライブラリやフレームワークを使わずに純粋なPython実装が求められるのかを確認する意図があります。

これに対して、ユーザーのVolodymyr Bilyachatは、タイムアウトや制限、ペナルティの範囲内であれば、使用するツールやライブラリに制限はないと回答しています。具体的な条件として、質問や推測の文字数制限、ラウンドごとのタイムアウト、エージェントに関する技術仕様が示されています。

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

# Can I use Langgraph to build and submit agent

**Bikash Patra** *Mon Jun 10 2024 16:45:18 GMT+0900 (日本標準時)* (0 votes)

Dear Community,

  Can anyone , please tell me if we can use langgraph / langchain to create the agents? Or does it need to have pure python implementation without any other libraries / frameworks?



---

 # Comments from other users

> ## VolodymyrBilyachat
> 
> My understanding is you can use what ever you want as soon you are within
> 
> Timeouts, Limits and Penalties.
> 
> Questions are limited to 2000 characters
> 
> Guesses are limited to 100 characters
> 
> Timeouts
> 
> Agents are given 60 seconds per round to answer
> 
> Agents have an additional 300 overage seconds to use throughout the game
> 
> Any agent timing out will cause the game to end
> 
> Any answering agent responding with anything other than yes or no will result in the game ending and them losing the match.
> 
> Technical Specifications
> 
> 100 GB of disk space
> 
> 16 GB of RAM
> 
> 1 T4 GPU
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# Langgraphを使ってエージェントを構築・提出できますか？
**Bikash Patra** *2024年6月10日 16:45 JST* (0票)
コミュニティの皆さん、
langgraphやlangchainを使用してエージェントを作成することは可能でしょうか？それとも、他のライブラリやフレームワークを使わずに純粋なPython実装でなければならないのでしょうか？

---
 # 他のユーザーからのコメント
> ## VolodymyrBilyachat
> 
> 私の理解では、タイムアウトや制限、ペナルティの範囲内であれば、何を使っても構いません。
> 
> 質問は2000文字までに制限されています。
> 
> 推測は100文字までに制限されています。
> 
> タイムアウト
> 
> エージェントには、回答のために1ラウンドあたり60秒が与えられます。
> 
> エージェントは、ゲームを通して使用できる追加の300秒の超過時間を持っています。
> 
> いずれかのエージェントがタイムアウトした場合、ゲームは終了します。
> 
> 回答エージェントが「はい」または「いいえ」以外で回答した場合、ゲームは終了し、その試合は負けとなります。
> 
> 技術仕様
> 
> ディスク容量: 100GB
> 
> RAM: 16GB
> 
> GPU: 1 T4 GPU
> 
> 


</div>