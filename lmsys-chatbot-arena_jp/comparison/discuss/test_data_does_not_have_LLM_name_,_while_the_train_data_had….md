# 要約 
このディスカッションは、コンペティションのテストデータにLLMの名前が含まれていないことについて議論しています。トレーニングデータには「model_a」と「model_b」というカラムがあり、LLMの名前が含まれていましたが、テストデータにはそれらがありません。

ユーザーは、このことがモデル名に基づいて予測を行うことを防ぐためであると推測しています。一方、別のユーザーは、LLMの名前は予測に関係ないため、トレーニングデータにも必要ないと考えています。

このディスカッションは、コンペティションのデータセットの設計に関する疑問を提起しており、参加者はモデル名を使用せずに予測を行う方法を検討する必要があることを示唆しています。


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

# test data does not have LLM name , while the train data had (columns : 'model_a' and 'model_b'). 

**Kumar Shivansh** *Tue Jul 02 2024 08:11:13 GMT+0900 (日本標準時)* (0 votes)

test data does not have llm name , while the train data had (columns : 'model_a' and 'model_b'). 



---

 # Comments from other users

> ## Enter your display name
> 
> This is precisely to prevent people from making predictions based on the model's name.
> 
> 
> 


---

> ## Anya
> 
> I think even the train data doesnt have to have the LLM name cols, cuz they dont matter the predictions. Our task is to predict the battle results' probability between two responses.
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# テストデータにLLMの名前がありませんが、トレーニングデータにはありました（カラム：'model_a'と'model_b'）。
**Kumar Shivansh** *2024年7月2日 火曜日 08:11:13 JST* (0票)
テストデータにLLMの名前がありませんが、トレーニングデータにはありました（カラム：'model_a'と'model_b'）。 
---
# 他のユーザーからのコメント
> ## 表示名の入力
> 
> これは、モデル名に基づいて予測を行うことを防ぐためです。
> 
> 
> 
---
> ## Anya
> 
> トレーニングデータにもLLMの名前のカラムは必要ないと思います。なぜなら、それらは予測に関係ないからです。私たちの仕事は、2つの応答間のバトル結果の確率を予測することです。
> 
> 
> 
---



</div>