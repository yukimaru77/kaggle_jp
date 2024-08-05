# 要約 
このディスカッションは、KaggleコンペティションでGemma 1.1 7B instruct-enモデルをメモリ不足なく使用する方法について議論しています。

Marília Prataさんは、このモデルをKaggle Notebookで実行しようとするとメモリ不足で再起動してしまう問題に直面していました。バッチサイズやmax_lengthを減らすなどの解決策を試しましたが、7Bモデルでは効果が限定的でした。

その後、Awsafさんが作成したコードを見つけたことで、メモリ問題を解決し、モデルを正常に実行することができました。このコードは、Gemma 1.1 7BモデルをInt8形式でロードすることで、メモリ使用量を削減しています。

Marília Prataさんは、Awsafさんのコードが非常に有用であるにもかかわらず、あまり注目されていないことを指摘し、その重要性を強調しています。また、このコードのおかげで、コンペティションでホストがピン留めしていた最後のモデルを提出することができたと述べています。

Adnan Alarefさんは、Marília Prataさんの問題解決に役立ったコードを共有してくれたことに感謝の意を表しています。

このディスカッションは、Kaggleコンペティションで大型言語モデルを使用する際に発生するメモリ問題に対する解決策を提供しており、他のユーザーにとっても参考になる情報となっています。


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

# Load 7b Gemma Keras without any memory issue and FAST.

**Marília Prata** *Sun May 12 2024 07:28:29 GMT+0900 (日本標準時)* (27 votes)

# A tip  to avoid memory issues while running your 1.1 -7b_instruct_en Gemma/Keras Model:

[Gemma 1.1 7B Int8 Load](https://www.kaggle.com/code/awsaf49/gemma-1-1-7b-int8-load) By Awsaf.

On the last topic (2 days ago ), I asked "How to work with Gemma Keras 1.1- 7b instruct-en WITHOUT your Kaggle Notebook being restarted cause you've allocated more memory than is avaiable. Then we should opt to Google Cloud or dismiss our work.

Some answers that I got to that previous topic:  I read/learned  that reducing batches and max_length could help me to load the model and face the memory issue.  Not always, it's a 7b (7 billion parameters model).

But, what if we don't have max_lenght and batches written on our Kaggle Notebook script? Sometimes it happens. Therefore, it's great to have a Plan B:

Fortunately, I found Awsaf's code and published my 1st Gemma 1.1-7b-instruct-en.  

So, take a look and check Awsaf's amazing, cristal clear code:

[Gemma 1.1 7B Int8 Load](https://www.kaggle.com/code/awsaf49/gemma-1-1-7b-int8-load) By Awsaf.

For the record, there aren't many 7b Gemma Keras  Kaggle Notebooks. Though we can find plenty of 2b Models.



---

 # Comments from other users

> ## Adnan Alaref
> 
> Good news for find solution, thanks for sharing  [@mpwolke](https://www.kaggle.com/mpwolke) 
> 
> 
> 
> > ## Marília PrataTopic Author
> > 
> > Indeed Alaref,
> > 
> > I was so happy that I was able to work with Gemma/Keras 1.1-7b_instruct-en without any memory issue that I felt that I should share this topic because very few showed appreciation to Awsaf's code (till yesterday he had only 6 votes for such a remarkable and useful code and  his 2 datasets.  
> > 
> > Maybe, kagglers didn't realize the importance of that code.
> > 
> > For the record, the Notebook ran in only GPU 15 minutes!  Isn't that great?
> > 
> > Besides, I was able to deliver the last Model that the hosts had pinned on this competition.
> > 
> > Not many users are working with 1.1_7b_instruct. In fact, I didn't read any other, except Awsaf's code.
> > 
> > It was almost my "Moby Dick" of models.
> > 
> > Thank you Alaref.
> > 
> > 
> > 


---



</div>
<div class="column-right">

# 日本語訳

# 7B Gemma Keras をメモリ問題なく高速にロードする方法

**Marília Prata** *2024年5月12日日曜日 07:28:29 GMT+0900 (日本標準時)* (27票)

# メモリ問題を回避するためのヒント: Gemma/Keras モデル (1.1 - 7b_instruct_en) を実行する場合

[Gemma 1.1 7B Int8 Load](https://www.kaggle.com/code/awsaf49/gemma-1-1-7b-int8-load) Awsaf 著

前回のトピック（2日前）で、「Gemma Keras 1.1- 7b instruct-en を、Kaggle Notebook がメモリ不足で再起動することなく、どのように使用すればいいのか」という質問をしました。Google Cloud を使うか、作業を諦めるしかない状況でした。

その前のトピックに対する回答として、バッチサイズと max_length を減らすことで、モデルをロードしてメモリ問題に対処できるという情報を得ました。しかし、7B（70億パラメータ）のモデルでは、必ずしも有効ではありません。

しかし、Kaggle Notebook のスクリプトに max_length やバッチサイズが記述されていない場合もあります。そのような場合に備えて、Plan B があると便利です。

幸運なことに、Awsaf のコードを見つけ、私の最初の Gemma 1.1-7b-instruct-en を公開することができました。

Awsaf の素晴らしい、非常に分かりやすいコードをご覧ください:

[Gemma 1.1 7B Int8 Load](https://www.kaggle.com/code/awsaf49/gemma-1-1-7b-int8-load) Awsaf 著

記録として、7B Gemma Keras の Kaggle Notebook は多くありません。2B モデルはたくさん見つかりますが。

---

# 他のユーザーからのコメント

> ## Adnan Alaref
> 
> 解決策が見つかって嬉しいです。共有してくれてありがとうございます  [@mpwolke](https://www.kaggle.com/mpwolke) 
> 
> 
> 
> > ## Marília Prata トピック作成者
> > 
> > Alaref さん、その通りです。
> > 
> > メモリ問題なく Gemma/Keras 1.1-7b_instruct-en を使用できたことにとても喜び、このトピックを共有すべきだと感じました。なぜなら、Awsaf のコードに対する感謝の気持ちを表明した人はほとんどいなかったからです（昨日まで、彼の素晴らしい、役に立つコードと 2 つのデータセットに対して、わずか 6 票しかありませんでした）。
> > 
> > Kagglers は、そのコードの重要性に気づいていなかったのかもしれません。
> > 
> > 記録として、Notebook は GPU でわずか 15 分で実行されました！素晴らしいと思いませんか？
> > 
> > さらに、このコンペティションでホストがピン留めしていた最後のモデルを提出することができました。
> > 
> > 1.1_7b_instruct を使用しているユーザーは多くありません。実際、Awsaf のコード以外には、他に見たことがありません。
> > 
> > それは、私にとってほぼ「白鯨」のようなモデルでした。
> > 
> > Alaref さん、ありがとうございます。
> > 
> > 
> > 
---



</div>