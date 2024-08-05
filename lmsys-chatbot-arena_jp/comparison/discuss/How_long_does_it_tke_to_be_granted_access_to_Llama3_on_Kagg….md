# 要約 
このディスカッションは、Kaggle で Llama3 へのアクセスを取得するのにかかる時間に関するものです。

トピック作成者は、Meta のサイトではすぐにアクセス権を取得できたのに、Kaggle ではまだ保留中であると述べています。他のユーザーからのコメントでは、アクセス権を取得するまでに 6 日から 7 日かかったという報告があり、週末には 10 分で取得できたという報告もありました。

また、ユーザーは、Kaggle で Llama3 へのアクセスを取得する方法、アクセス権を取得できない場合の回避策、および Llama3 を使用した際に発生するエラーの解決策について議論しています。

要約すると、このディスカッションは、Kaggle で Llama3 へのアクセスを取得するのにかかる時間、アクセス権を取得できない場合の回避策、および Llama3 を使用した際に発生するエラーの解決策について議論しています。


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

# How long does it tke to be granted access to Llama3 on Kaggle? [Solved: 24 hours]

**CPMP** *Thu Jul 11 2024 19:49:54 GMT+0900 (日本標準時)* (10 votes)

I got access immediately yesterday on Meta's site, but my request is still pending here.

Edit: I got access after 24 hours, which is reasonable. It is just that I got access on Meta immediately which sets optimistic expectations.



---

 # Comments from other users

> ## samson
> 
> Six days left for me. Access is not granted still. Thats why I got weights on HF
> 
> 
> 
> > ## CPMPTopic Author
> > 
> > Did you get access from Meta's site before asking for access here?
> > 
> > 
> > 
> > > ## samson
> > > 
> > > Yes, I did. BTW, I finally go it. It took them 7 days to give me an access
> > > 
> > > 
> > > 
> > > ## william.wu
> > > 
> > > OMG, I just requested the access yesterday… Is there any public llama3.1 models on Kaggle?
> > > 
> > > 
> > > 
> > > ## william.wu
> > > 
> > > Okay, I found one [https://www.kaggle.com/datasets/gmhost/llama31instruct](https://www.kaggle.com/datasets/gmhost/llama31instruct)
> > > 
> > > 
> > > 


---

> ## Allie K.
> 
> Good question. 
> 
> I have been waiting since last Friday morning, constantly updating the number of days of waiting (now it's 6) and repeating my questions to Kaggle team.
> 
> Perhaps you, with your authority, will be able to push things forward.🙂 
> 
> 
> 
> > ## CPMPTopic Author
> > 
> > I don't think I have more weight than anyone here.
> > 
> > 
> > 
> > > ## Allie K.
> > > 
> > > Apparently you do have!😀
> > > 
> > > As a magic, the access is here, after "only" 6 days.
> > > 
> > > 
> > > 
> > > ## CPMPTopic Author
> > > 
> > > Did you post? If yes then I will agree with you.
> > > 
> > > 
> > > 


---

> ## Psi
> 
> you can get it on HF, no need to apply here on kaggle
> 
> 
> 
> > ## CPMPTopic Author
> > 
> > I have access on HF and on Meta. I am asking why it is long here.
> > 
> > 
> > 


---

> ## RB
> 
> Hello , similar post here - [https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/518813](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/518813) 
> 
> and a workaround  [https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/518813#2913166](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/518813#2913166)
> 
> 
> 
> > ## CPMPTopic Author
> > 
> > I downloaded the model, no worries. I am asking a specific question.
> > 
> > 
> > 


---

> ## Valentin Werner
> 
> Welcome to the competition!
> 
> I already posted this before, but took 10 minutes for me a weekend.. 
> 
> 
> 


---

> ## Shelton
> 
> Nice work!
> 
> 
> 


---

> ## Nguyễn Anh Tú
> 
> Why i always get the error "Incorrect path_or_model_id: '/kaggle/input/llama-3/transformers/8b-hf/1'. Please provide either the path to a local folder or the repo_id of a model on the Hub" when using "tokenizer = AutoTokenizer.from_pretrained("/kaggle/input/llama-3/transformers/8b-hf/1")" ? Please helps me. Thanks.
> 
> 
> 
> > ## Valentin Werner
> > 
> > You have not been granted access for llama3 on Kaggle yet. Make sure to apply for access on meta and kaggle.
> > 
> > 
> > 
> > > ## Nguyễn Anh Tú
> > > 
> > > To solve that problem, I use another pretrain model from my another notebook. But I got the error "Submission Scoring Error" when I submitted my notebook, I thought that I set the wrong format for my submission.csv. Then, I read the sample_submission.csv and change the the value of ['winner_model_a', 'winner_model_b', 'winner_tie'] columns with my y_predict. The worst thing is my notebook ran successful but when I submitted again I got the error "Notebook Threw Exception", please help me!
> > > 
> > > 
> > > 
> > > ## XXX
> > > 
> > > Submission Scoring Error: Your notebook generated a submission file with incorrect format. Some examples causing this are: wrong number of rows or columns, empty values, an incorrect data type for a value, or invalid submission values from what is expected.
> > > 
> > > above is from kaggle debugging tips.
> > > 
> > > I think may be you can check the value of your submission🤔
> > > 
> > > 
> > > 


---

> ## Feisx Song
> 
> helpful tips!
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# Kaggle で Llama3 へのアクセスを取得するのにどのくらい時間がかかりますか？ [解決済み: 24 時間]
**CPMP** *2024年7月11日木曜日 19:49:54 GMT+0900 (日本標準時)* (10票)
昨日、Meta のサイトですぐにアクセス権を取得しましたが、こちらのリクエストはまだ保留中です。
編集: 24 時間後にアクセス権を取得しました。これは妥当な時間です。Meta ですぐにアクセス権を取得できたため、楽観的な期待を抱いていました。
---
# 他のユーザーからのコメント
> ## samson
> 
> 私はまだアクセス権を取得していません。6 日間残っています。そのため、HF で重みを手に入れました。
> 
> 
> 
> > ## CPMPトピック作成者
> > 
> > ここでアクセスを要求する前に、Meta のサイトからアクセス権を取得しましたか？
> > 
> > 
> > 
> > > ## samson
> > > 
> > > はい、取得しました。ちなみに、ついにアクセス権を取得しました。アクセス権を取得するまでに 7 日かかりました。
> > > 
> > > 
> > > 
> > > ## william.wu
> > > 
> > > OMG、昨日アクセスを要求したばかりです… Kaggle に公開されている llama3.1 モデルはありますか？
> > > 
> > > 
> > > 
> > > ## william.wu
> > > 
> > > いいえ、[https://www.kaggle.com/datasets/gmhost/llama31instruct](https://www.kaggle.com/datasets/gmhost/llama31instruct) を見つけました。
> > > 
> > > 
> > > 
---
> ## Allie K.
> 
> いい質問ですね。
> 
> 私は先週の金曜日の朝から待っていて、待ち時間の経過日数を常に更新しています（今は 6 日目です）。そして、Kaggle チームに質問を繰り返しています。
> 
> あなたは権限を持っているため、事態を進めることができるかもしれません。🙂 
> 
> 
> 
> > ## CPMPトピック作成者
> > 
> > 私はここで誰よりも権限を持っているとは思っていません。
> > 
> > 
> > 
> > > ## Allie K.
> > > 
> > > どうやらあなたは権限を持っているようです！😀
> > > 
> > > 魔法のように、アクセス権が「わずか」6 日後に届きました。
> > > 
> > > 
> > > 
> > > ## CPMPトピック作成者
> > > 
> > > 投稿しましたか？もしそうなら、あなたの意見に同意します。
> > > 
> > > 
> > > 
---
> ## Psi
> 
> HF で入手できます。Kaggle で申請する必要はありません。
> 
> 
> 
> > ## CPMPトピック作成者
> > 
> > HF と Meta でアクセス権を持っています。なぜここで時間がかかるのかを尋ねています。
> > 
> > 
> > 
---
> ## RB
> 
> こんにちは、ここにも同様の投稿があります - [https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/518813](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/518813) 
> 
> そして、回避策があります - [https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/518813#2913166](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/518813#2913166)
> 
> 
> 
> > ## CPMPトピック作成者
> > 
> > モデルをダウンロードしました。心配しないでください。私は具体的な質問をしています。
> > 
> > 
> > 
---
> ## Valentin Werner
> 
> このコンペティションへようこそ！
> 
> 以前にも投稿しましたが、週末は 10 分かかりました。
> 
> 
> 
---
> ## Shelton
> 
> 素晴らしいですね！
> 
> 
> 
---
> ## Nguyễn Anh Tú
> 
> 「tokenizer = AutoTokenizer.from_pretrained("/kaggle/input/llama-3/transformers/8b-hf/1")」を使用すると、なぜ常に「Incorrect path_or_model_id: '/kaggle/input/llama-3/transformers/8b-hf/1'. Please provide either the path to a local folder or the repo_id of a model on the Hub」というエラーが発生するのでしょうか？助けてください。ありがとうございます。
> 
> 
> 
> > ## Valentin Werner
> > 
> > まだ Kaggle で llama3 へのアクセス権を取得していません。Meta と Kaggle でアクセスを申請してください。
> > 
> > 
> > 
> > > ## Nguyễn Anh Tú
> > > 
> > > その問題を解決するために、別のノートブックから別の事前トレーニング済みモデルを使用しました。しかし、ノートブックを提出すると「Submission Scoring Error」というエラーが発生しました。提出ファイルのフォーマットが間違っているのではないかと考えました。そこで、sample_submission.csv を読み込み、['winner_model_a', 'winner_model_b', 'winner_tie'] 列の値を y_predict で変更しました。最悪なことに、ノートブックは正常に実行されましたが、再度提出すると「Notebook Threw Exception」というエラーが発生しました。助けてください！
> > > 
> > > 
> > > 
> > > ## XXX
> > > 
> > > Submission Scoring Error: Your notebook generated a submission file with incorrect format. Some examples causing this are: wrong number of rows or columns, empty values, an incorrect data type for a value, or invalid submission values from what is expected.
> > > 
> > > 上記は Kaggle のデバッグヒントからのものです。
> > > 
> > > 提出物の値を確認してみてください🤔
> > > 
> > > 
> > > 
---
> ## Feisx Song
> 
> 役立つヒントですね！
> 
> 
> 
---



</div>