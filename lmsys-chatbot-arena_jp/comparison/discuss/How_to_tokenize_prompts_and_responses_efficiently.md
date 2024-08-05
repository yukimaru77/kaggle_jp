# 要約 
## コンペティションディスカッション要約

このディスカッションは、LMSYS - Chatbot Arena Human Preference Predictionsコンペティションにおけるプロンプトとレスポンスの効率的なトークン化について議論しています。

**投稿者irishu**は、3つの異なるトークン化方法を試した結果、プロンプトとレスポンスAとBを結合して最大トークン数までトークン化する**方法1**が最も良い結果を出したと報告しています。

**irishu**は、方法1よりも効率的な方法があるかどうか、また最大トークン数を増やすとスコアがどのくらい向上するのかを質問しています。

**他のユーザーからのコメント**では、**irishu**は学習と推論で最大トークン数を2048に変更したところ、スコアが向上したと報告しています。また、パディングを使ってトークン長を調整すべきかどうか疑問視しています。

**要約:**

* プロンプトとレスポンスのトークン化は、コンペティションにおける重要な要素です。
* irishuは、プロンプトとレスポンスを結合して最大トークン数までトークン化する**方法1**が最も良い結果を出したと報告しています。
* 最大トークン数を増やすとスコアが向上する可能性があります。
* パディングを使ってトークン長を調整するかどうかは、さらなる検討が必要です。 


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

# How to tokenize prompts and responses efficiently

**irishu** *Sun Jul 28 2024 13:56:19 GMT+0900 (日本標準時)* (6 votes)

# Experiment

I have tried the following three methods so far, and the first has performed the best in LB.

### Methods

tokenize up to the max_tokens by joining strings like prompt + responseA + responseB
allocate one-third of the max_tokens to each sentence and tokenize up to the limit
allocate the number of tokens in the appropriate ratio(ex;1:2:2)

### Conditions

- using Gemma-2 9b 4-bit QLoRA

- max_tokens = 1024

- using only the last prompt and responses 

- 1 epoch using all train data

- referring to the excellent work [[Training] Gemma-2 9b 4-bit QLoRA fine-tuning](https://www.kaggle.com/code/emiz6413/training-gemma-2-9b-4-bit-qlora-fine-tuning)

# Question

### Don't you think there is a more efficient way than the simple method1?

Looking at the distribution of the number of tokens in the prompt and response (only the last one), it appears that around 10% of them contain more than 1024 tokens in total. That is, in some cases, response B may not contain enough information.

### How much would a larger max_tokens improve the score?

I have not been able to test this yet due to computational resources.



---

 # Comments from other users

> ## irishuTopic Author
> 
> I changed max_tokens to 2048 in learning and inference and the score improved.
> 
> Now I am wondering if I should adjust the token length with padding.
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# プロンプトとレスポンスを効率的にトークン化する

**irishu** *2024年7月28日 13:56:19 (日本標準時)* (6票)

# 実験

これまで以下の3つの方法を試してみました。その中で、最初の方法がLBで最も良い結果を出しました。

### 方法

1. プロンプト + レスポンスA + レスポンスB を結合して、最大トークン数までトークン化する。
2. 各文に最大トークン数の1/3を割り当て、その制限までトークン化する。
3. トークン数を適切な比率（例：1:2:2）で割り当てる。

### 条件

- Gemma-2 9b 4-bit QLoRAを使用
- 最大トークン数 = 1024
- 最後のプロンプトとレスポンスのみを使用
- 全ての訓練データを使用して1エポック
- 優れた作品「[Training] Gemma-2 9b 4-bit QLoRA fine-tuning」([https://www.kaggle.com/code/emiz6413/training-gemma-2-9b-4-bit-qlora-fine-tuning](https://www.kaggle.com/code/emiz6413/training-gemma-2-9b-4-bit-qlora-fine-tuning))を参照

# 質問

### シンプルな方法1よりも効率的な方法はないでしょうか？

プロンプトとレスポンス（最後のもののみ）のトークン数の分布を見ると、約10%が合計で1024トークンを超えているようです。つまり、場合によっては、レスポンスBに十分な情報が含まれていない可能性があります。

### 最大トークン数を増やすとスコアはどのくらい向上するでしょうか？

計算リソースの関係で、まだテストできていません。

---

# 他のユーザーからのコメント

> ## irishuTopic 作成者
> 
> 学習と推論で最大トークン数を2048に変更したところ、スコアが向上しました。
> 
> これで、パディングを使ってトークン長を調整すべきかどうかが疑問です。
> 
> 
> 
---



</div>