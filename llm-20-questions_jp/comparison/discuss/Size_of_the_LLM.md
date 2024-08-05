# 要約 
ディスカッションでは、参加者がモデルのサイズに関して質問をしています。具体的には、モデルのパラメータに制限があるのか（7B以下など）、それともより大きなモデルを使用できるのかという疑問が提示されました。これに対して、別のユーザーがNVIDIA T4（16GB）の制限に言及し、一般的にbitsandbyteのパッケージを利用すると、7Bパラメータのモデルが実行できる最大のサイズであることを解説しています。

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

# Size of the LLM

**G R Shanker Sai** *Thu Jun 27 2024 02:06:33 GMT+0900 (日本標準時)* (0 votes)

Hello,

I have a question on choosing the model, 

Is there any restriction on choosing a model (<=7B parameters)? or can I choose a model which is much larger?



---

 # Comments from other users

> ## Bovard Doerschuk-Tiberi
> 
> Competitors have to run their model on a NVIDIA T4 (16GB). In practice using the bitsandbyte pip package a 7B param model is about the largest anyone has been able to run. 
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# LLMのサイズについて
**G R Shanker Sai** *2024年6月27日 Thu 02:06:33 GMT+0900 (日本標準時)* (0票)
こんにちは、
モデルの選択について質問があります。
モデルには何か制限がありますか（<=7Bパラメータ）？それとも、もっと大きなモデルを選択することはできますか？
---
 # 他のユーザーからのコメント
> ## Bovard Doerschuk-Tiberi
> 
> 競技者は、NVIDIA T4（16GB）でモデルを実行しなければなりません。実際には、bitsandbyteのパッケージを使用すると、7Bパラメータのモデルが誰もが実行できる最大のサイズとなることが多いです。
> 
> ---


</div>