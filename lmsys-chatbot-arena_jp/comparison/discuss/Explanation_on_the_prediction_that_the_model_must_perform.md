# 要約 
このディスカッションは、コンペティション参加者がモデルの予測を行う際に、応答の構造のみを考慮すべきか、それとも正確性も考慮すべきかについて疑問を呈しています。

具体的には、単語埋め込みモデルが、文法的に正しいが内容的に誤った応答を、正しい応答と同じように評価してしまう可能性について懸念されています。

例えば、フランスの首都を尋ねるプロンプトに対して、モデル A は「フランスの首都はパリです。」、モデル B は「フランスの首都はローマです。」と回答した場合、単語埋め込みモデルは、両方の応答が文法的に正しいという理由で引き分けを予測する可能性があります。しかし、実際にはモデル A の回答が正しいので、モデル A が勝利するべきです。

そのため、ディスカッションの投稿者は、単語埋め込みモデルに加えて、Bert などのモデルを利用することで、応答の正確性をチェックし、より正確な予測を行うことができるのではないかと提案しています。


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

# Explanation on the prediction that the model must perform

**GregReds** *Thu Jul 11 2024 05:15:59 GMT+0900 (日本標準時)* (1 votes)

Hello everyone!

I am a master's degree student and I am using this competition for an exam; for educational purposes, I must primarily rely on the use of word embedding. My question and my doubt is: to make predictions and to determine whether to award the win to model a or model b, should the model only check the structure of the responses, or also their correctness?

Let me give an example to be more explicit:

If the prompt were: What is the capital of France?

response_a: The capital of France is Paris.

response_b: The capital of France is Rome.

Typically, a model like word2vec, if not too well-trained, might base its evaluation on the structure rather than the correctness, focusing on the fact that the sentences are structured similarly and this predicting a tie. However, model A should win because the actual capital is indeed Paris, not Rome.

Therefore, it might be useful to utilize word embedding models like Bert that theoretically also check the correctness of the response.

I hope I have made myself clear! Thanks everyone.

[Screenshot 2024-07-10 alle 22.14.58.png](https://storage.googleapis.com/kaggle-forum-message-attachments/2916192/20917/Screenshot 2024-07-10 alle 22.14.58.png)



</div>
<div class="column-right">

# 日本語訳

# モデルが実行する必要がある予測に関する説明

**GregReds** *木曜日 7月 11日 2024 05:15:59 GMT+0900 (日本標準時)* (1 票)
皆さん、こんにちは！

私は修士課程の学生で、このコンペティションを試験のために利用しています。教育目的のため、私は主に単語埋め込みの使用に頼らなければなりません。私の質問と疑問は、予測を行い、モデル a またはモデル b に勝利を与えるかどうかを判断するために、モデルは応答の構造のみをチェックする必要がありますか、それともその正確性もチェックする必要がありますか？

より明確にするために例を挙げます。

プロンプトが次の場合: フランスの首都は何ですか？
response_a: フランスの首都はパリです。
response_b: フランスの首都はローマです。

通常、word2vec のようなモデルは、十分に訓練されていない場合、正確性ではなく構造に基づいて評価を行う可能性があり、文が同様に構造化されているという事実にも焦点を当て、引き分けを予測します。しかし、モデル A は、実際の首都が実際にはパリであり、ローマではないため、勝利する必要があります。

したがって、応答の正確性も理論的にチェックする Bert のような単語埋め込みモデルを利用することが役立つ可能性があります。

私の説明が理解できたことを願っています！皆さん、ありがとうございます。
[Screenshot 2024-07-10 alle 22.14.58.png](https://storage.googleapis.com/kaggle-forum-message-attachments/2916192/20917/Screenshot 2024-07-10 alle 22.14.58.png)



</div>