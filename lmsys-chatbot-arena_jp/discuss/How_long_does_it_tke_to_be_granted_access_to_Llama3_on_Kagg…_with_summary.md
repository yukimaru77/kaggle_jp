# 要約 
このディスカッションは、Kaggle で Llama3 へのアクセスを取得するのにかかる時間に関するものです。

トピック作成者は、Meta のサイトではすぐにアクセス権を取得できたのに、Kaggle ではまだ保留中であると述べています。他のユーザーからのコメントでは、アクセス権を取得するまでに 6 日から 7 日かかったという報告があり、週末には 10 分で取得できたという報告もありました。

また、ユーザーは、Kaggle で Llama3 へのアクセスを取得する方法、アクセス権を取得できない場合の回避策、および Llama3 を使用した際に発生するエラーの解決策について議論しています。

要約すると、このディスカッションは、Kaggle で Llama3 へのアクセスを取得するのにかかる時間、アクセス権を取得できない場合の回避策、および Llama3 を使用した際に発生するエラーの解決策について議論しています。


---
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

