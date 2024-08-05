# 要約 
このディスカッションは、Kaggleコンペティションにおけるタイムアウト問題について議論しています。多くの参加者が、同じ推論ロジックを用いてもタイムアウトが発生する頻度が増加したと報告しています。

主な原因として、コンペティションの締め切りが近づくにつれて参加者数が増加し、サーバーの負荷が高まっている可能性が指摘されています。また、GPUの過熱やパフォーマンスのばらつきも原因として考えられています。

参加者たちは、タイムアウトによる提出時間の無駄や、解決策を求めています。具体的な解決策は提示されていませんが、GPUの負荷を軽減したり、提出時間を調整したりする必要があることが示唆されています。


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

# Time out always

**Rise_Hand** *Wed Jul 31 2024 18:18:40 GMT+0900 (日本標準時)* (7 votes)

why I always met timeout these day with same infer logic



---

 # Comments from other users

> ## Attacker
> 
> People's participation rate rises before the competition closes, and then the server becomes unstable.
> 
> 
> 


---

> ## Cody_Null
> 
> Yep same thing with our solutions
> 
> 
> 


---

> ## JM
> 
> GPUs running hot and slowing down in last few days probably 😅
> 
> 
> 


---

> ## Krupal Patel
> 
> i also facing same problem with LLMs notebooks.
> 
> 
> 


---

> ## justin1357
> 
> Same, a waste of submission times
> 
> 
> 
> > ## justin1357
> > 
> > Each GPU's performance is different, which cause this prob
> > 
> > 
> > 


---

> ## Roschild.Rui
> 
> Hi HAN, our team is also at a loss -> Why was it possible to submit almost identical inference weights and inference logic without any issues a few days ago, but recently there have been constant submission errors? It seems that the imbalance in Kaggle's computational resource load significantly affects the competition submissions.
> 
> 
> 


---

> ## JamshaidSohail
> 
> Guys. My 15 submissions wasted. Are you able to figure it out ? How to get out of it ?
> 
> 
> 


---

> ## hwz13
> 
> 是的，gpu运行时间太长了
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# タイムアウトが頻発する問題

**Rise_Hand** *2024年7月31日 水曜日 18:18:40 日本標準時* (7票)

最近、同じ推論ロジックでタイムアウトが発生し続けていますが、なぜでしょうか？

---
# 他のユーザーからのコメント

> ## Attacker
> 
> コンペティションの締め切りが近づくにつれて、参加者の数が急増し、サーバーが不安定になっている可能性があります。
> 
> 
> 
---
> ## Cody_Null
> 
> 同じ問題に直面しています。
> 
> 
> 
---
> ## JM
> 
> 過去数日間、GPUが過熱して速度が低下しているのかもしれません 😅
> 
> 
> 
---
> ## Krupal Patel
> 
> LLMのノートブックで同じ問題が発生しています。
> 
> 
> 
---
> ## justin1357
> 
> 同じです。提出時間が無駄になってしまいます。
> 
> 
> 
> > ## justin1357
> > 
> > GPUのパフォーマンスはそれぞれ異なるため、この問題が発生している可能性があります。
> > 
> > 
> > 
---
> ## Roschild.Rui
> 
> HANさん、私たちも困っています。-> 数日前はほぼ同一の推論ウェイトと推論ロジックで問題なく提出できていたのに、最近になって提出エラーが頻発するようになりました。Kaggleの計算リソース負荷の偏りが、コンペティションの提出に大きく影響しているようです。
> 
> 
> 
---
> ## JamshaidSohail
> 
> みんな、私の提出が15回も無駄になりました。解決策を見つけられましたか？どうすればこの問題を回避できますか？
> 
> 
> 
---
> ## hwz13
> 
> はい、GPUの実行時間が長すぎます。
> 
> 
> 
--- 



</div>