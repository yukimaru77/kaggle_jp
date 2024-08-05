# 要約 
このディスカッションは、Kaggleコンペティション「LMSYS - Chatbot Arena 人間による好み予測チャレンジ」におけるCV（クロスバリデーション）とLB（リーダーボード）の相関関係について議論しています。

* **Stochoshi G** は、Deberta-v3-xsmallモデルとTfidfモデルのCVスコアとLBスコアがほぼ一致していることを報告しています。また、両モデルを組み合わせた場合、CVスコアは1.00に改善しますが、LBスコアは未定です。
* **Kishan Vavdara** は、自身のCVスコアとLBスコアがほぼ一致していることを報告しています。CVスコアが1.02、1.00、0.98、0.96の場合、LBスコアはそれぞれ0.996、0.971、0.955、0.959となっています。
* **Takamichi Toda** は、20%の検証率でホールドアウト1つを使用するCV戦略を採用しており、パブリックLBとよく相関していることを報告しています。
* **heartkilla** は、ランダム分割または層化分割を使用しているかについて質問し、Takamichi Todaはランダム分割を使用していると回答しています。
* **heartkilla** は、CVとLBの相関関係に関する最新情報がないか質問しています。

このディスカッションから、CVとLBの相関関係はコンペティション参加者によって異なり、一概に断言できないことがわかります。また、CV戦略やモデル選択によって、CVとLBの相関関係が変化する可能性があることも示唆されています。


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

# CV vs LB thread

**Stochoshi G** *Sat May 04 2024 12:56:33 GMT+0900 (日本標準時)* (13 votes)

Deberta-v3-xsmall: ~1.02 cv / 1.03 lb

Tfidf: ~1.02 cv / ~1.03 lb

Combined: ~1.00 cv / tbd

Siamese Deberta: [https://www.kaggle.com/code/stochoshi/deberta-starter-lmsys](https://www.kaggle.com/code/stochoshi/deberta-starter-lmsys)



---

 # Comments from other users

> ## Kishan Vavdara
> 
> My CV :
> 
>  1.02 Lb -> LB - 0.996
> 
>  0.98 Lb -> LB - 0.971
> 
>  0.96 Lb -> LB - 0.955
> 
>  0.95 Lb -> LB - 0.959
> 
> 
> 


---

> ## Takamichi Toda
> 
> My CV strategy is one hold-out, with a validation rate of 20%.
> 
> At present, it correlates well with the Public LB.
> 
> Best: Local=1.034074/Public LB1.036
> 
> 
> 
> > ## heartkilla
> > 
> > hi, you use random or stratified split?
> > 
> > 
> > 
> > > ## Takamichi Toda
> > > 
> > > random split
> > > 
> > > 
> > > 


---

> ## heartkilla
> 
> Any updates on this?
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# CV vs LB スレッド

**Stochoshi G** *2024年5月4日 土曜日 12:56:33 日本標準時* (13票)

Deberta-v3-xsmall: CV 約1.02 / LB 1.03
Tfidf: CV 約1.02 / LB 約1.03
組み合わせ: CV 約1.00 / LB 未定
Siamese Deberta: [https://www.kaggle.com/code/stochoshi/deberta-starter-lmsys](https://www.kaggle.com/code/stochoshi/deberta-starter-lmsys)
---
# 他のユーザーからのコメント

> ## Kishan Vavdara
> 
> 私のCV:
> 
>  1.02 LB -> LB - 0.996
> 
>  0.98 LB -> LB - 0.971
> 
>  0.96 LB -> LB - 0.955
> 
>  0.95 LB -> LB - 0.959
> 
> 
> 
---
> ## Takamichi Toda
> 
> 私のCV戦略は、20%の検証率でホールドアウト1つです。
> 
> 現時点では、パブリックLBとよく相関しています。
> 
> ベスト: ローカル=1.034074/パブリックLB1.036
> 
> 
> 
> > ## heartkilla
> > 
> > こんにちは、ランダム分割または層化分割を使用していますか？
> > 
> > 
> > 
> > > ## Takamichi Toda
> > > 
> > > ランダム分割です。
> > > 
> > > 
> > > 
---
> ## heartkilla
> 
> これに関する最新情報はありませんか？
> 
> 
> 
--- 



</div>