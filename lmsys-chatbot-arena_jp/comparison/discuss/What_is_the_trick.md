# 要約 
このディスカッションは、KaggleのLMSYS - Chatbot Arena Human Preference Predictionsコンペティションにおける、参加者の抱える課題と解決策に関するものです。

**課題:**

* コンペティションで提供されるリソースでは、モデルのファインチューニングが難しい。
* 自宅のGPUメモリでは、十分な処理能力が不足する。
* テキストクレンジング、ストップワードの削除、ステミングとレマタイゼーションなどの前処理方法について、具体的なアドバイスが欲しい。

**解決策:**

* **外部プロバイダーの利用:**
    * runpod.io: 手頃な価格でGPUを提供するサービス。
    * vast.ai: クラウドベースのGPUリソースを提供するサービス。
    * Google Cloud: Googleが提供するクラウドサービス。
    * AWS, Azure: AmazonとMicrosoftが提供するクラウドサービス。
* **前処理方法:**
    * ディスカッションでは具体的なアドバイスは提供されていません。

**要約:**

コンペティション参加者は、モデルのファインチューニングとGPUリソースの不足に苦労しています。外部プロバイダーの利用が推奨されており、runpod.io、vast.ai、Google Cloudなどが挙げられています。前処理方法については、具体的なアドバイスは提供されていません。


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

# What is the trick...

**TheStoneMX** *Sun Jun 16 2024 01:19:44 GMT+0900 (日本標準時)* (3 votes)

I find almost impossible to fine-tune with the recurses that we get from Kaggle, and at home not enough GPU memory.

What are people using?

External providers? Google, Azure, My Pods, etc.

Any suggestions?

What are people doing, on these type of competitions, Text cleaning, stop words removal, Stemming and lemmatization, etc.

Thanks for any tips guys.



---

 # Comments from other users

> ## Ravi Ramakrishnan
> 
> [@oscarrangel](https://www.kaggle.com/oscarrangel) I recommend you to try out [runpod.io](https://www.runpod.io/)
> 
> They offer excellent GPUs at moderately affordable prices and across various payment plans and options
> 
> 
> 
> > ## TheStoneMXTopic Author
> > 
> > Yes, thanks. That is what I started to use, but they have secure cloud and community cloud. I am using community one. Is that correct?
> > 
> > 
> > 


---

> ## Cody_Null
> 
> I have been in this position before myself. The best option (in my opinion) would be cloud resources. It is up to you how much you are willing to spend and what experiments are worth it and I know there are a lot of platforms to choose from and price may vary based off what you need and your area. Some popular ones are runpod, vast.ai, google cloud, and then depending on your personal situation AWS or Azure may be more accessible but those first 3 are more likely and worth researching. No doubt I have missed some, but a good starting point. 
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# どうすればいいのか...
**TheStoneMX** *2024年6月16日 日曜日 01:19:44 JST* (3票)

Kaggleで提供されるリソースではファインチューニングがほぼ不可能で、自宅ではGPUメモリが不足しています。
皆さんは何を用いていますか？
外部プロバイダー？ Google、Azure、My Podsなど。
何か提案はありますか？
このようなコンペティションでは、テキストクレンジング、ストップワードの削除、ステミングとレマタイゼーションなど、どのような処理を行っていますか？
ヒントをいただけたら幸いです。

---
# 他のユーザーからのコメント
> ## Ravi Ramakrishnan
> 
> [@oscarrangel](https://www.kaggle.com/oscarrangel)  [runpod.io](https://www.runpod.io/) を試してみることをお勧めします。
> 
> 彼らは、さまざまな支払いプランとオプションで、手頃な価格で優れたGPUを提供しています。
> 
> 
> 
> > ## TheStoneMXトピック作成者
> > 
> > はい、ありがとうございます。私も使い始めましたが、セキュアクラウドとコミュニティクラウドがあります。コミュニティクラウドを使っています。これで合っていますか？
> > 
> > 
> > 
---
> ## Cody_Null
> 
> 私も以前、同じような状況にありました。最良の選択肢（私の意見では）はクラウドリソースです。どれだけの費用をかけるか、どの実験が価値があるかはあなた次第です。そして、選択肢となるプラットフォームはたくさんあり、必要なものや地域によって価格が異なることは承知しています。runpod、vast.ai、Google Cloudなど、人気のあるものがあります。そして、あなたの状況によっては、AWSやAzureの方がアクセスしやすいですが、最初の3つはより可能性が高く、調査する価値があります。間違いなくいくつか見落としていますが、良い出発点です。
> 
> 
> 
--- 



</div>