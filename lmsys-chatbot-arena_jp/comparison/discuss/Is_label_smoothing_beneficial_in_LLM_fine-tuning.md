# 要約 
このディスカッションは、ラベルスムージングがLLMのファインチューニングに役立つのかどうかについて議論しています。

トピック作成者のYichuan Gaoは、Gemma2ForSequenceClassificationモデルをLoRAを使ってファインチューニングしており、ラベルスムージングを追加するかどうか悩んでいます。スムージングを0.2に設定すると、評価損失がLBスコアよりも高くなり、モデルの自信が低下したのではないかと考えています。

Valentin Wernerは、精度が60%未満のタスクではラベルスムージングが役立つとコメントしています。これは、過度に自信のある誤った予測よりも、自信が低くても正しい分類の方が良いからです。ただし、モデルが適切に較正されている場合は、ラベルスムージングを使用しない方が良いとのことです。

yechenzhi1は、ラベルスムージングが自分の場合役に立たなかったとコメントしています。

Yichuan Gaoは、これらのコメントを受けて、今後スムージングを減らしてみることを決意しました。

このディスカッションから、ラベルスムージングはタスクやモデルによって効果が異なることがわかります。最適なスムージング値は、実験によって決定する必要があります。


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

# Is label smoothing beneficial in LLM fine-tuning?

**Yichuan Gao** *Sat Jul 13 2024 12:02:54 GMT+0900 (日本標準時)* (2 votes)

I'm using LoRA to fine-tune a Gemma2ForSequenceClassification model.

I'm wondering if add label smoothing is a good or bad thing in this process. Since if I add smoothing of 0.2 (i.e., label is [0.8, 0.1, 0.1] ), I'm getting a eval_loss higher than LB score (0.98 vs 0.96), maybe smoothing made my model less confident than it could be?

Could anyone share some experience on this topic? Would you add it, and if you do, how much is a sweet spot?



---

 # Comments from other users

> ## Valentin Werner
> 
> Normally if you are doing a task with < 60% accuracy and try to minimize loss, label smoothing should be helping, as its better to have less confident but correct classification rather than super confident wrong predictions. However, if your model is well calibrated without label smoothing, you should simply not use it. It helped a lot in my earlier experiments with DeBERTa though..
> 
> 
> 
> > ## Yichuan GaoTopic Author
> > 
> > Thanks for this information! I'll try to apply less smoothing now :)
> > 
> > 
> > 


---

> ## yechenzhi1
> 
> Same here, label smoothing is not beneficial for me.
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# ラベルスムージングはLLMファインチューニングに役立つのか？
**Yichuan Gao** *2024年7月13日（土）12:02:54 JST* (2票)

Gemma2ForSequenceClassificationモデルをLoRAを使ってファインチューニングしています。
このプロセスでラベルスムージングを追加するのが良いか悪いか悩んでいます。スムージングを0.2（つまり、ラベルが[0.8, 0.1, 0.1]）にすると、評価損失がLBスコアよりも高くなります（0.98対0.96）。これは、スムージングによってモデルの自信が低下したためでしょうか？
このトピックに関する経験を共有していただける方はいらっしゃいますか？ラベルスムージングを追加する場合は、どの程度の値が適切でしょうか？
---
# 他のユーザーからのコメント
> ## Valentin Werner
> 
> 通常、精度が60%未満のタスクで損失を最小化しようとする場合、ラベルスムージングは役立ちます。なぜなら、過度に自信のある誤った予測よりも、自信が低くても正しい分類の方が良いからです。ただし、ラベルスムージングなしでモデルが適切に較正されている場合は、使用しない方が良いでしょう。私の以前のDeBERTaを使った実験では、ラベルスムージングは非常に役立ちました。
> 
> 
> 
> > ## Yichuan Gaoトピック作成者
> > 
> > この情報ありがとうございます！今後はスムージングを減らしてみます :)
> > 
> > 
> > 
---
> ## yechenzhi1
> 
> 同感です。ラベルスムージングは私の場合、役に立ちませんでした。
> 
> 
> 
--- 



</div>