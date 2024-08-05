# 要約 
このディスカッションは、KaggleでトレーニングされたLlama3モデルをダウンロードする方法についてです。Valentin Wernerは、トップスコアのパブリックノートブックで使用されているモデルをダウンロードしようとしていますが、データセットをクリックすると、約30MBのデータを含むプレースホルダーファイルしか表示されません。

Kishan Vavdaraは、これらのファイルはloraウェイトであり、Kaggleからllama-3モデルを取得し、loraウェイトを追加して、さらにトレーニング/推論を行うことができることを説明しています。Valentin Wernerは、loraウェイトをこのように使ったことがないため、説明に感謝しています。

要約すると、このディスカッションは、KaggleでトレーニングされたLlama3モデルをダウンロードする方法について、loraウェイトの使用について説明しています。


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

# Download Llama3 Models from Kaggle?

**Valentin Werner** *Mon Jun 17 2024 12:41:39 GMT+0900 (日本標準時)* (2 votes)

Is there a way for me to download the Llama3 Models that were trained by others from Kaggle? I am talking about the model that is used in all the top scoring public notebooks. When I click on the dataset, I only see a placeholder file with about 30 MB of data.



---

 # Comments from other users

> ## Kishan Vavdara
> 
> They are lora weights, you can take llama-3 model from kaggle and add lora weights for further training/inference. 
> 
> 
> 
> > ## Valentin WernerTopic Author
> > 
> > Ah, I have never used lora weights before like this. Thank you for the clarification!
> > 
> > 
> > 


---



</div>
<div class="column-right">

# 日本語訳

# KaggleからLlama3モデルをダウンロードする方法について

**Valentin Werner** *2024年6月17日 月曜日 12:41:39 日本標準時* (2票)

他の人がKaggleでトレーニングしたLlama3モデルをダウンロードする方法はあるでしょうか？ 私は、トップスコアのパブリックノートブックで使用されているモデルについて話しています。 データセットをクリックすると、約30MBのデータを含むプレースホルダーファイルしか表示されません。

---
# 他のユーザーからのコメント
> ## Kishan Vavdara
> 
> それらはloraウェイトです。Kaggleからllama-3モデルを取得し、loraウェイトを追加して、さらにトレーニング/推論を行うことができます。
> 
> 
> 
> > ## Valentin Wernerトピック作成者
> > 
> > ああ、私はこれまでloraウェイトをこのように使ったことがありません。 説明してくれてありがとうございます！
> > 
> > 
> > 
--- 



</div>