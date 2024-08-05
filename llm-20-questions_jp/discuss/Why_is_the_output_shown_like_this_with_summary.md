# 要約 
**Yuang Wu**は、Kaggleの「20の質問」コンペの「コード」セクションに投稿されているコードを使ってLLMの動作を学ぼうとしているが、出力が異常であることに困惑しています。具体的には、gemma-7b-it-3を使用した際の出力が、質問に対する答えが十分にテキストに含まれていないといった奇妙な内容になっていることを報告しています。彼はLLMについての経験が浅いため、問題の原因が分からず、助けを求めています。また、gemma-2-9bをどのようにダウンロードするかについても質問しており、Hugging Faceのアクセス権を持っているが、Kaggleからのダウンロードができないとのことです。

---
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
