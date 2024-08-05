# 要約 
このディスカッションは、KaggleのLMSYS - Chatbot Arena Human Preference Predictionsコンペティションにおける、Rich Olson氏によるTF-IDFと勾配ブースティングツリーを用いたアプローチについてです。

Rich Olson氏は、TF-IDFを使ってテキストをベクトル化し、LightGBMで学習させるというシンプルな手法を試しました。プロンプト、response_a、response_bをTF-IDFでベクトル化し、response_aとresponse_bを結合してLightGBMで学習させました。プロンプトを学習に含めることはパフォーマンス向上に繋がらなかったようです。

この手法は、CPUで約30分でベクトル化と学習が完了し、推論も高速に行えます。ngram_range=(3, 5)ではうまくいきませんでしたが、(1, 5)に変更することでパフォーマンスが大幅に向上しました。これは、単純な単語頻度が重要な役割を果たしている可能性を示唆しています。

また、XGBoostを用いたバージョンも試しましたが、トレーニングに時間がかかりました。GPUでの高速化を試みましたが、うまくいきませんでした。

Rich Olson氏は、テストデータにベクトル化器を適合させるという興味深いオプションも提案しています。

この手法は、LightGBMで検証スコア1.036、LBスコア1.038、XGBoostでLBスコア1.039を達成しました。

このディスカッションは、コンペティション参加者にとって、TF-IDFと勾配ブースティングツリーを用いたアプローチの有効性を示す良い例となっています。


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

# TF-IDF -> Boosted Trees [LB 1.038]

**Rich Olson** *Tue May 07 2024 10:44:19 GMT+0900 (日本標準時)* (1 votes)

Hey all -

Sharing my first (working) effort at this:

[https://www.kaggle.com/code/richolson/lmsys-tf-idf-boosted-trees](https://www.kaggle.com/code/richolson/lmsys-tf-idf-boosted-trees)

Simple idea is to use TF-IDF for vectorizing the texts - then see if a gradient boosted tree framework (LightGBM) can figure it out.

The TF-IDF vectorizer is fitted on prompt, response_a and response_b.

Vectorization is done on response_a and response_b separately and then combined in an hstack - and then LightGBM is trained on the whole mess.

(Using prompt for training didn't seem to obviously improve performance).

Vectorization + training takes about 30 minutes on CPU.  I don't have a time estimate on inference - but it's fast on just CPU.

I had minimal luck when vectorizing with ngram_range=(3, 5).  Performance improved a bunch when I changed that to ngram_range=(1, 5).  This approach working may be a lot about simple word frequency.

Another version of the notebook uses XGBoost - which trains much slower (about 2.5 hours).  That one is still scoring as I type this (I suspect it will have an LB score about the same).  I tried speeding up XGBoost using GPU - but for some reason it wouldn't converge.

Since I'm able to train-on-submission - one interesting option might be to try fitting the vectorizer on the test data (and then using that to vectorize the training data)…

Hope this is helpful to someone!

-Rich

Side note: I just noticed validation on LightGBM reported a log-loss score of 1.036.. - shockingly close to my LB of 1.038! I can't recall another time I've had that happen…



---

 # Comments from other users

> ## Rich OlsonTopic Author
> 
> The XGBoost version finished scoring - 1.039 on the LB.
> 
> Considering XGBoost took much, much longer to train - I'll stick with LightGBM for this notebook.
> 
> If you're curious to see the XGBoost code - just look a version 8 of this notebook.
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# TF-IDF -> ブーステッドツリー [LB 1.038]
**Rich Olson** *2024年5月7日 火曜日 10:44:19 JST* (1票)

皆さん、こんにちは！

このコンペティションに対する私の最初の（動作する）取り組みを共有します。

[https://www.kaggle.com/code/richolson/lmsys-tf-idf-boosted-trees](https://www.kaggle.com/code/richolson/lmsys-tf-idf-boosted-trees)

シンプルなアイデアは、TF-IDF を使ってテキストをベクトル化し、勾配ブースティングツリーフレームワーク（LightGBM）でそれを理解できるかどうかを確認することです。

TF-IDF ベクトル化器は、プロンプト、response_a、response_b に適合されます。

ベクトル化は、response_a と response_b で別々に実行され、その後 hstack で結合されます。その後、LightGBM は全体でトレーニングされます。

（トレーニングにプロンプトを使用しても、パフォーマンスが明らかに向上するようには見えませんでした。）

ベクトル化とトレーニングには、CPU で約 30 分かかります。推論にかかる時間はわかりませんが、CPU のみでも高速です。

ngram_range=(3, 5) でベクトル化すると、ほとんど成功しませんでした。ngram_range=(1, 5) に変更すると、パフォーマンスが大幅に向上しました。このアプローチが機能するのは、単純な単語頻度が大きく関係しているのかもしれません。

ノートブックの別のバージョンでは XGBoost を使用していますが、トレーニングに時間がかかります（約 2.5 時間）。これは、私がこれを書いている間もまだスコア付けされています（LB スコアはほぼ同じになると思います）。GPU を使って XGBoost を高速化しようとしましたが、なぜか収束しませんでした。

トレーニング時に提出できるため、興味深いオプションの 1 つは、テストデータにベクトル化器を適合させ（そしてそれをトレーニングデータのベクトル化に使用すること）を試すことです…

これが誰かの役に立てば幸いです！

-Rich

補足：LightGBM の検証で、ログ損失スコアが 1.036 と報告されました… LB の 1.038 に驚くほど近い！このようなことが起こったのは初めてだと思います…

---
# 他のユーザーからのコメント
> ## Rich Olsonトピック作成者
> 
> XGBoost バージョンがスコア付けを完了しました - LB で 1.039。
> 
> XGBoost のトレーニングに非常に時間がかかったことを考えると、このノートブックでは LightGBM を使用します。
> 
> XGBoost のコードに興味がある場合は、このノートブックのバージョン 8 を見てください。
> 
> 
> 
---



</div>