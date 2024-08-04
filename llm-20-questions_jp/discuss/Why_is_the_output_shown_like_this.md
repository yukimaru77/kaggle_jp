## Yuang Wu さんの質問に対する回答

> # Why is the output shown like this?
> **Yuang Wu** *Wed Jul 10 2024 16:50:45 GMT+0900 (日本標準時)* (0 votes)
> I am running the code posted in the "Code" district, which is [https://www.kaggle.com/code/kasafumi/gemma2-9b-it-llm20-questions](https://www.kaggle.com/code/kasafumi/gemma2-9b-it-llm20-questions), to try to learn about how LLM works. I used gemma-7b-it-3 instead. However, I found that my outputs are quite weird, just is shown like this:
> round: 7
> question: Sure, here is your next question:**Is the country located in Africa?
> answer: yes
> guess: The answer is: No country name has been revealed in the text yet,
> round: 8
> question: Okay, I have received your answer. Please give me your next question.
> answer: yes
> guess: The answer is: No country name has been provided in the text, therefore
> round: 9
> question: Sure, here is your next question:**Do most people living in the country
> answer: yes
> guess: The answer is: yes. The text does not contain any information about the
> [https://www.kaggle.com/code/yuangwu/notebookee6ff5da7b/notebook](https://www.kaggle.com/code/yuangwu/notebookee6ff5da7b/notebook) This is the notebook. I am totally new to LLM, and I cannot figure out why. I will be very thankful if anyone can answer this.
> btw: How to download gemma-2-9b? I have already had the access on hugging face, but kaggle told me that I still cannot download this into kaggle directory…

Yuang Wu さん、LLM の学習、頑張ってくださいね！出力結果が奇妙に見えるとのことですが、これはおそらく **gemma-7b-it-3 モデルが質問と回答の文脈をうまく理解できていない** ことが原因です。

**gemma-7b-it-3 モデルは、質問と回答の文脈を理解する能力がまだ十分に発達していない** ため、質問の意図を正しく解釈できず、回答も適切でない場合があります。

**解決策としては、**

1. **より大きなモデルを使用する:** gemma-2-9b や他のより大きな言語モデルを使用すると、文脈理解能力が向上する可能性があります。
2. **ファインチューニングを行う:** gemma-7b-it-3 モデルを「20の質問」ゲームのデータセットでファインチューニングすることで、ゲームのルールや文脈を理解させ、より適切な質問と回答を生成できるようになる可能性があります。
3. **プロンプトエンジニアリング:** モデルに適切なプロンプトを与えることで、文脈理解を助けることができます。例えば、質問の前に「20の質問ゲームのルールに従って質問してください」といった指示を追加するなどです。

**gemma-2-9b のダウンロードについて:**

Kaggle で gemma-2-9b をダウンロードできないとのことですが、これは Kaggle の環境設定やアクセス権限の問題かもしれません。Hugging Face でアクセス権限を取得しているにもかかわらず、Kaggle でダウンロードできない場合は、Kaggle のサポートに問い合わせてみてください。

LLM の学習は難しいですが、諦めずに頑張ってください！何か困ったことがあれば、遠慮なく質問してください。

