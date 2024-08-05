# 要約 
このディスカッションは、LMSYS チャットボットアリーナコンペティションのデータセットエクスプローラーについてです。Emmanuel Turlay は、このツールを無料で公開し、ユーザーがデータセットを探索して、クラスタリング、セグメント化、インスペクションを行うことができるようにしました。

このツールは、個々の行をブラウズして詳細を調べたり、セマンティッククラスタを生成したり、クラスタ、モデルペア、勝者モデルなどで会話をフィルタリングしたりできます。

ユーザーからのコメントは、このツールが非常に役立ち、データセットを理解するのに役立つことを示しています。Josh Bauer は、早口言葉のクラスタを見つけたことを共有し、Idriss Chebak は、ピカチュウとゼウスのラップバトルのプロンプトを見つけたことを共有しました。

Felipe Maia Polo は、クラスタの割り当てをダウンロードする方法を尋ね、Emmanuel Turlay は、エクスポートファイルにクラスタとトークン数を追加したことを発表しました。

Valentin Werner は、ライセンスに関する懸念を表明し、Emmanuel Turlay は、ツールがライセンス条項に準拠していることを確認しました。

全体として、このディスカッションは、LMSYS チャットボットアリーナコンペティションのデータセットエクスプローラーが、ユーザーがデータセットを理解し、分析するのに役立つ貴重なツールであることを示しています。


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

# LMSYS Dataset Explorer – Cluster, segment, inspect

**Emmanuel Turlay** *Thu May 30 2024 02:56:10 GMT+0900 (日本標準時)* (40 votes)

Hey folks – Today, we’re releasing a free dataset explorer for the LMSYS challenge.

With our tool, you can browse through individual rows and inspect their content in great detail. We generated semantic clusters, and you can filter conversations by cluster, model pairs, winner model, and so on.

The tool is free and no login is required. Be sure to let the community know what you discover.

Click this link to start exploring: [https://app.airtrain.ai/dataset/bb589c26-8f45-4f42-8ba3-07ef51b73a03/null/1/0](https://app.airtrain.ai/dataset/bb589c26-8f45-4f42-8ba3-07ef51b73a03/null/1/0)



---

 # Comments from other users

> ## Lisa DunlapCompetition Host
> 
> OMG THIS IS SO COOL!!!
> 
> 
> 


---

> ## Cviko Dukanovic
> 
> Amazing product. The meta clusters and clusters are greatly produced!
> 
> 
> 


---

> ## Josh Bauer
> 
> One fun cluster I've found: plenty of variations on the "how much wood could a woodchuck chuck if a woodchuck could chuck wood" tongue twister. Ex: "If, IF, a woodchuck could chuck wood, how much wood could a woodchuck chuck before it lost its job as a project manager?" 😆
> 
> Under "Riddles and Reasoning" > "Woodchuck Tongue Twister", row 4308
> 
> 
> 
> > ## Idriss Chebak
> > 
> > one cool prompt i found was "Construct a rap battle, in the style of Epic Rap Battles of History, with rhyme and meter and personal attacks relevant to each character, between Pikachu and Zeus. Each participant gets 2 verses. There is no announcer and Zeus goes first." 😄
> > 
> > 
> > 


---

> ## Felipe Maia Polo
> 
> Thanks for the amazing work! Is there a way to download the cluster assignments? Thanks!
> 
> 
> 
> > ## Josh Bauer
> > 
> > Glad you like it! You can't export the clusters right now, but it's on our TODO list.
> > 
> > 
> > 
> > ## Emmanuel TurlayTopic Author
> > 
> > We just shipped an update that includes clusters and token counts in the exported file. Have fun!
> > 
> > 
> > 
> > > ## Felipe Maia Polo
> > > 
> > > thank you!
> > > 
> > > 
> > > 


---

> ## Valentin Werner
> 
> The tool looks amazing!
> 
> As you are the the CEO of the company behind the tool, did you check the licenses? I am not sure if you are allowed to publish data from the competition on your platform, given the cc-by-nc license. I know that there was the recommendation not to do such in previous conpetitions.
> 
> Maybe you can instead show us how to use your tool to create such a dashboard instead?
> 
> All the best for your company and product!
> 
> (Also quite the PR stunt to have your employees comment on your thread (Josh & Idriss) 😉)
> 
> 
> 
> > ## Emmanuel TurlayTopic Author
> > 
> > Hi Valentin, thanks for the compliment!
> > 
> > We did check the [license](https://creativecommons.org/licenses/by-nc/4.0/) and it says we are allowed to share, copy, and redistribute the material in any medium or format; adapt, remix, transform, and build upon the material; as long as we attribute credit and offer it under non-commercial terms.
> > 
> > The Dataset Explorer is free and requires no sign-up. The Kaggle page is linked to from the description for attribution.
> > 
> > We certainly want to remain compliant and are offering this work to support the community. Thanks for making us double-check the license 😉
> > 
> > 
> > 
> > > ## Valentin Werner
> > > 
> > > Great stuff!
> > > 
> > > 
> > > 


---

> ## YingxiZhang
> 
> The tool is amazing!👍
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# LMSYS データセットエクスプローラー – クラスタリング、セグメント化、インスペクション
**Emmanuel Turlay** *2024年5月30日木曜日 02:56:10 GMT+0900 (日本標準時)* (40票)

皆さん、こんにちは！本日、LMSYS チャレンジ用の無料データセットエクスプローラーをリリースします。

このツールを使用すると、個々の行をブラウズして、その内容を詳細に調べることができます。私たちはセマンティッククラスタを生成しました。クラスタ、モデルペア、勝者モデルなどで会話をフィルタリングできます。

このツールは無料で、ログインは不要です。発見したことをコミュニティに知らせてください。

探索を開始するには、このリンクをクリックしてください：[https://app.airtrain.ai/dataset/bb589c26-8f45-4f42-8ba3-07ef51b73a03/null/1/0](https://app.airtrain.ai/dataset/bb589c26-8f45-4f42-8ba3-07ef51b73a03/null/1/0)

---
# その他のユーザーからのコメント
> ## Lisa Dunlapコンペティションホスト
> 
> OMG、これは本当に素晴らしいです！
> 
> 
> 
---
> ## Cviko Dukanovic
> 
> 素晴らしい製品です。メタクラスタとクラスタは非常にうまく生成されています！
> 
> 
> 
---
> ## Josh Bauer
> 
> 見つけた面白いクラスタの1つ： 「もしもウッドチャックが木を投げることができたら、ウッドチャックはどれだけ多くの木を投げることができるだろうか」という早口言葉の多くのバリエーションがあります。例：「もしも、もしも、ウッドチャックが木を投げることができたら、プロジェクトマネージャーとしての仕事を失う前に、ウッドチャックはどれだけ多くの木を投げることができるだろうか？」😆
> 
> 「なぞなぞと推論」>「ウッドチャックの早口言葉」の下、4308行目
> 
> 
> 
> > ## Idriss Chebak
> > 
> > 見つけた面白いプロンプトの1つは、「歴史上のエピックラップバトルのスタイルで、韻とリズム、そして各キャラクターに関連する個人的な攻撃を交えて、ピカチュウとゼウスのラップバトルを作成してください。各参加者は2つのバースを歌います。アナウンサーはいないので、ゼウスが最初に歌います。」😄
> > 
> > 
> > 
---
> ## Felipe Maia Polo
> 
> 素晴らしい仕事をしていただきありがとうございます！クラスタの割り当てをダウンロードする方法がありますか？ありがとうございます！
> 
> 
> 
> > ## Josh Bauer
> > 
> > お気に召していただけて嬉しいです！現時点ではクラスタをエクスポートすることはできませんが、TODOリストに入っています。
> > 
> > 
> > 
> > ## Emmanuel Turlayトピック作成者
> > 
> > クラスタとトークン数をエクスポートファイルに含めたアップデートをリリースしました。楽しんでください！
> > 
> > 
> > 
> > > ## Felipe Maia Polo
> > > 
> > > ありがとうございます！
> > > 
> > > 
---
> ## Valentin Werner
> 
> このツールは素晴らしいですね！
> 
> あなたはツールの背後にある会社のCEOですが、ライセンスを確認しましたか？cc-by-nc ライセンスを考えると、コンペティションのデータをプラットフォームに公開することは許可されているかどうか分かりません。以前のコンペティションでは、そのようなことをしないように推奨されていたことを知っています。
> 
> 代わりに、このツールを使用してこのようなダッシュボードを作成する方法を教えてもらうことはできますか？
> 
> あなたの会社と製品の成功を祈っています！
> 
> （また、あなたの従業員があなたのスレッドにコメントしているのは、かなり宣伝効果がありますね（Josh と Idriss）😉）
> 
> 
> 
> > ## Emmanuel Turlayトピック作成者
> > 
> > Valentin さん、お褒めの言葉をありがとうございます！
> > 
> > 私たちは [ライセンス](https://creativecommons.org/licenses/by-nc/4.0/) を確認しました。そこには、クレジットを明記し、非営利目的で提供する限り、あらゆる媒体または形式で資料を共有、コピー、再配布し、資料を適応、リミックス、変換、および構築することが許可されていると記載されています。
> > 
> > データセットエクスプローラーは無料で、サインアップは不要です。説明から Kaggle ページへのリンクが提供されており、クレジットとして機能します。
> 
> 私たちは確実にコンプライアンスを維持したいと考えており、この作業をコミュニティを支援するために提供しています。ライセンスを再確認させてくれてありがとうございます 😉
> 
> 
> 
> > > ## Valentin Werner
> > > 
> > > 素晴らしいですね！
> > > 
> > > 
---
> ## YingxiZhang
> 
> このツールは素晴らしいです！👍
> 
> 
> 
---



</div>