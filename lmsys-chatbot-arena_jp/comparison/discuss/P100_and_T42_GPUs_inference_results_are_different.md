# 要約 
このディスカッションは、Kaggleコンペティション「LMSYS - Chatbot Arena 人間による好み予測チャレンジ」における推論結果の差異に関するものです。

投稿者は、シングルGPUと2つのGPUを使った場合で推論結果が異なることに気づき、さらにローカルマシンとKaggleでの推論結果にもわずかな違いがあることを報告しています。具体的には、ID 1233961 のデータに対する `winner_model_a`, `winner_model_b`, `winner_tie` の確率が、GPUの数や実行環境によって異なっていることを示しています。

コメント欄では、Valentin Werner氏がトランスフォーマーのバージョンによってもスコアが異なる可能性を指摘しています。

このディスカッションは、推論結果の差異の原因を突き止め、安定した結果を得るための方法を探るためのものです。


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

# P100 and T4*2 GPUs inference results are different

**Femca7** *Tue Jul 16 2024 09:47:35 GMT+0900 (日本標準時)* (1 votes)

Recently, I found that the inference results differ when using a single GPU compared to using two GPUs. Another issue is that the inference results on my local machine and on Kaggle also have slight differences.

Does anyone know the reason for this?

Using one GPU:  

id     winner_model_a  winner_model_b  winner_tie 

1233961     0.245430    0.517676    0.236894

Using two GPUs:  

id     winner_model_a  winner_model_b  winner_tie 

1233961     0.238452    0.535787    0.225761



---

 # Comments from other users

> ## Valentin Werner
> 
> I also noticed that the scores are different across transformer versions.
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# P100 と T4*2 GPU での推論結果が異なる

**Femca7** *2024年7月16日 火曜日 09:47:35 JST* (1票)

最近、シングルGPUと2つのGPUを使った場合で推論結果が異なることに気づきました。もう1つの問題は、ローカルマシンとKaggleでの推論結果にもわずかな違いがあることです。

この理由をご存知の方はいらっしゃいますか？

シングルGPUを使用した場合:
```
id     winner_model_a  winner_model_b  winner_tie 
1233961     0.245430    0.517676    0.236894
```

2つのGPUを使用した場合:
```
id     winner_model_a  winner_model_b  winner_tie 
1233961     0.238452    0.535787    0.225761
```

---
# 他のユーザーからのコメント

> ## Valentin Werner
> 
> トランスフォーマーのバージョンによってもスコアが異なることに気づきました。
> 
> 
> 
--- 



</div>