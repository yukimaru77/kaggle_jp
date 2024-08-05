# 要約 
**Yuang Wu**は、Kaggleの「20の質問」コンペの「コード」セクションに投稿されているコードを使ってLLMの動作を学ぼうとしているが、出力が異常であることに困惑しています。具体的には、gemma-7b-it-3を使用した際の出力が、質問に対する答えが十分にテキストに含まれていないといった奇妙な内容になっていることを報告しています。彼はLLMについての経験が浅いため、問題の原因が分からず、助けを求めています。また、gemma-2-9bをどのようにダウンロードするかについても質問しており、Hugging Faceのアクセス権を持っているが、Kaggleからのダウンロードができないとのことです。

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

# Why is the output shown like this?

**Yuang Wu** *Wed Jul 10 2024 16:50:45 GMT+0900 (日本標準時)* (0 votes)

I am running the code posted in the "Code" district, which is [https://www.kaggle.com/code/kasafumi/gemma2-9b-it-llm20-questions](https://www.kaggle.com/code/kasafumi/gemma2-9b-it-llm20-questions), to try to learn about how LLM works. I used gemma-7b-it-3 instead. However, I found that my outputs are quite weird, just is shown like this:

round: 7
question: Sure, here is your next question:**Is the country located in Africa?
answer: yes
guess: The answer is: No country name has been revealed in the text yet,
round: 8
question: Okay, I have received your answer. Please give me your next question.
answer: yes
guess: The answer is: No country name has been provided in the text, therefore
round: 9
question: Sure, here is your next question:**Do most people living in the country
answer: yes
guess: The answer is: yes. The text does not contain any information about the

[https://www.kaggle.com/code/yuangwu/notebookee6ff5da7b/notebook](https://www.kaggle.com/code/yuangwu/notebookee6ff5da7b/notebook) This is the notebook. I am totally new to LLM, and I cannot figure out why. I will be very thankful if anyone can answer this.

btw: How to download gemma-2-9b? I have already had the access on hugging face, but kaggle told me that I still cannot download this into kaggle directory…





</div>
<div class="column-right">

# 日本語訳

**Yuang Wu** *2024年7月10日（水）16:50:45 JST* (0票)  
「コード」セクションに投稿されているコードを実行していますが、学習したいのはLLMの動作です。こちらのコードを参照しています：[https://www.kaggle.com/code/kasafumi/gemma2-9b-it-llm20-questions](https://www.kaggle.com/code/kasafumi/gemma2-9b-it-llm20-questions)。ただし、代わりにgemma-7b-it-3を使用しました。しかし、出力がかなり奇妙なものになってしまいました。以下のように表示されるのです：

round: 7  
question: ここに次の質問があります:**その国はアフリカにありますか？**  
answer: はい  
guess: 答えは：まだテキストの中に国名が明らかにされていません、  
round: 8  
question: わかりました、あなたの答えを受け取りました。次の質問をお願いします。  
answer: はい  
guess: 答えは：テキストに提供された国名がありませんので  
round: 9  
question: 次の質問です:**その国に住んでいる人々の大多数は  
answer: はい  
guess: 答えは：はい。テキストにはその国についての情報が含まれていません。  
[https://www.kaggle.com/code/yuangwu/notebookee6ff5da7b/notebook](https://www.kaggle.com/code/yuangwu/notebookee6ff5da7b/notebook) これはノートブックです。私はLLMについて全くの初心者で、なぜこうなってしまったのか理解できません。もし解答してくれる方がいれば、非常に感謝します。  

ちなみに、gemma-2-9bをどのようにダウンロードすればよいのでしょうか？Hugging Faceのアクセス権は持っているのですが、Kaggleではダウンロードできないと言われました…。


</div>