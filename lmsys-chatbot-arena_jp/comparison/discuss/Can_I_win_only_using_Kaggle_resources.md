# 要約 
このディスカッションは、KaggleのLMSYS - Chatbot Arena Human Preference Predictionsコンペティションで、Kaggleのリソースのみで優勝できるかどうかについて議論しています。

**Areej Malkawi**は、コンペティションのデータが膨大で、多くの公開ノートブックが事前学習済みモデルを使用しているため、メモリとスコアのトレードオフに直面していることを述べています。KaggleのGPU/TPUクォータ以上のものを使用する必要があるのか、外部リソースを使用せずに優勝したり、LBの上位に食い込むことは可能なのかと質問しています。

**Ebi**は、ほとんどのKaggleコンペティションでは、多くの実験サイクルを実行する必要があるため、外部リソースを使用せずに優勝したり、LBの上位に食い込むことはほとんど不可能だと答えています。Ebi自身も、CPUのみのラップトップとColabのような安価なクラウドサービスを使って参加していましたが、銀メダルを獲得できたのは、RTX 4090を購入してからだと述べています。

**Hassan Abedi**も、ほとんどのNLPコンペティションでは、VRAMが豊富な高性能なGPUがあると大きな違いが出ると同意しています。

**Valentin Werner**は、ドイツではGPUのレンタルが1時間あたり約50セントから始まると述べています。トレーニングに8時間かかるとすると、4ユーロになります。何回か反復処理を行うので、間違いなくそれ以上の費用がかかりますが、ドイツでは4090は約1800ユーロです。つまり、レンタルGPUで約450回のトレーニング（または3600時間のトレーニング！）を行うことができます。このような大きな投資をする前に何か試したい場合は、このように始めることができます。さらに、Kaggleは30GBのVRAMを提供しています（Windows PCの4090は約23GB）。そのため、投資する前にあらゆることを試すことができます。KaggleのGPUの大きな問題は、可能性ではなく速度です。

**tanaka**は、外部リソースを使わずにこれらのコンペティションで競うのはかなり難しいようだと述べています。しかし、いきなりGPUを購入するのはハードルが高いと感じます。Colabや他のGPUレンタルサーバーなど、さまざまなオプションを試してから、GPUの購入またはレンタルを決定するのが良いようです。Vast.aiは人気のある選択肢のようです。

**Ebi**は、Vast.aiを使ったことがありませんが、個人的にはjarvislabs.aiが好きだと述べています。インスタンスの作成とSSHによるアクセスが簡単で高速です。価格も非常に安いと思います。

**Andreas Bisi**は、過去のNLPコンペティションを考えると、金メダルを獲得するには外部リソースが必要になります。しかし、TF-IDFソリューション（Kaggleのハードウェアを使用）で、運が良ければ銅メダルを獲得できると思います。

**結論として、このディスカッションでは、KaggleのLMSYS - Chatbot Arena Human Preference Predictionsコンペティションで、Kaggleのリソースのみで優勝することは非常に難しいことが示されています。多くの参加者は、高性能なGPUやクラウドサービスを利用して、より良い結果を得ています。しかし、KaggleのGPU/TPUクォータでも、十分な努力と工夫を凝らせば、上位に食い込むことは可能であるという意見もあります。**


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

# Can I win only using Kaggle resources?

**Areej Malkawi** *Mon Jun 10 2024 03:35:55 GMT+0900 (日本標準時)* (5 votes)

The data of this competition are huge, I saw many public notebooks that used some pre-trained models for inference and I tried to use a pre-trained model to train the given competition data but I'm facing memory\score trade-off, am I supposed to use something more than Kaggle GPU\ TPU quota to overcome memory issues? as well as getting high LB score?

can I win or be at the top of LB without using external resources?



---

 # Comments from other users

> ## Ebi
> 
> 
> can I win or be at the top of LB without using external resources?
> 
> I think it's almost impossible. And this applies to most Kaggle competitions, because in most cases, you need to do a lot of experiment cycles.  
> 
> In fact, I've been participating for about three years using a CPU-only laptop and a cheap cloud service like Colab, but I've only managed to get a silver medal. I bought an RTX 4090 a few months ago and was able to get a gold medal right away, which gives me an advantage in this competition too.  
> 
> 
> 
> > ## Hassan Abedi
> > 
> > Yeah, for most NLP competitions, having a good GPU with lots of VRAM makes a big difference. 
> > 
> > 
> > 
> > ## Valentin Werner
> > 
> > Note that renting a GPU starts (in Germany) around 50 cent / hour - let's say a training takes 8 hours, thats 4€. You will do some iterations, so you will definetly spent more money, BUT a 4090 is about 1800€ in Germany - so you can do about 450 trainings (or 3600 hours of training!!) on a rented GPU. If you want to try something before doing such a heavy investment, you could start like that.
> > 
> > Further, since Kaggle provides you 30 GB of VRAM (vs. about 23 GB on a Windows PC with a 4090), you can try all the things before going into investment. The big blocker with kaggle GPUs is speed, not possibilities.
> > 
> > 
> > 


---

> ## tanaka
> 
> Hmm I understood,  it seems quite difficult to compete in these competitions without using external resources.
> 
> However, I feel that suddenly buying a GPU is a high hurdle.
> 
> it seems best to try out various options like Colab or other GPU rental servers, and then decide whether to buy or rent a GPU.
> 
> [Vast.ai](http://vast.ai/) seems to be a popular option, doesn't it 🤔?
> 
> - [https://vast.ai/](https://vast.ai/)
> 
> - [https://cloud-gpus.com/](https://cloud-gpus.com/)
> 
> - [https://gist.github.com/devinschumacher/87dd5b87234f2d0e5dba56503bfba533](https://gist.github.com/devinschumacher/87dd5b87234f2d0e5dba56503bfba533)
> 
> - [https://getdeploying.com/reference/cloud-gpu](https://getdeploying.com/reference/cloud-gpu#paperspace)
> 
> 
> 
> > ## Ebi
> > 
> > I have never used vast.ai, but I personally like  [jarvislabs.ai](https://jarvislabs.ai/). 
> > 
> > It is easy and fast to create an instance and access it via SSH. I think the price is also very cheap. I mainly used it until I switched to a home server.
> > 
> > 
> > 


---

> ## Andreas Bisi
> 
> Considering past NLP competitions, you would need external resources to finish in the gold-medal area. However, I believe with a TF-IDF solution (on kaggle hardware) it's doable to finish in the bronze-medal area with some luck…
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# Kaggleのリソースのみで優勝できますか？
**Areej Malkawi** *2024年6月10日 月曜日 03:35:55 GMT+0900 (日本標準時)* (5 votes)
このコンペティションのデータは膨大で、多くの公開ノートブックが推論に事前学習済みモデルを使用しているのを見ました。私も事前学習済みモデルを使ってコンペティションデータのトレーニングを試みましたが、メモリとスコアのトレードオフに直面しています。メモリの問題を克服し、高いLBスコアを得るために、KaggleのGPU/TPUクォータ以上のものを使用する必要があるのでしょうか？外部リソースを使用せずに優勝したり、LBの上位に食い込むことは可能でしょうか？
---
# 他のユーザーからのコメント
> ## Ebi
> 
> 
> 外部リソースを使用せずに優勝したり、LBの上位に食い込むことは可能でしょうか？
> 
> ほとんど不可能だと思います。これはほとんどのKaggleコンペティションに当てはまります。なぜなら、ほとんどの場合、多くの実験サイクルを実行する必要があるからです。
> 
> 実は、私は約3年間、CPUのみのラップトップとColabのような安価なクラウドサービスを使って参加してきましたが、銀メダルを獲得できただけです。数か月前にRTX 4090を購入し、すぐに金メダルを獲得することができました。これは、このコンペティションでも有利に働きます。
> 
> 
> 
> > ## Hassan Abedi
> > 
> > はい、ほとんどのNLPコンペティションでは、VRAMが豊富な高性能なGPUがあると大きな違いが出ます。
> > 
> > 
> > 
> > ## Valentin Werner
> > 
> > ドイツでは、GPUのレンタルは1時間あたり約50セントから始まります。トレーニングに8時間かかるとすると、4ユーロになります。何回か反復処理を行うので、間違いなくそれ以上の費用がかかりますが、ドイツでは4090は約1800ユーロです。つまり、レンタルGPUで約450回のトレーニング（または3600時間のトレーニング！）を行うことができます。このような大きな投資をする前に何か試したい場合は、このように始めることができます。
> > 
> > さらに、Kaggleは30GBのVRAMを提供しています（Windows PCの4090は約23GB）。そのため、投資する前にあらゆることを試すことができます。KaggleのGPUの大きな問題は、可能性ではなく速度です。
> > 
> > 
> > 
---
> ## tanaka
> 
> なるほど、外部リソースを使わずにこれらのコンペティションで競うのはかなり難しいようですね。
> 
> しかし、いきなりGPUを購入するのはハードルが高いと感じます。
> 
> Colabや他のGPUレンタルサーバーなど、さまざまなオプションを試してから、GPUの購入またはレンタルを決定するのが良いようです。
> 
> [Vast.ai](http://vast.ai/)は人気のある選択肢のようですよね 🤔？
> 
> - [https://vast.ai/](https://vast.ai/)
> 
> - [https://cloud-gpus.com/](https://cloud-gpus.com/)
> 
> - [https://gist.github.com/devinschumacher/87dd5b87234f2d0e5dba56503bfba533](https://gist.github.com/devinschumacher/87dd5b87234f2d0e5dba56503bfba533)
> 
> - [https://getdeploying.com/reference/cloud-gpu](https://getdeploying.com/reference/cloud-gpu#paperspace)
> 
> 
> 
> > ## Ebi
> > 
> > 私はVast.aiを使ったことがありませんが、個人的には[jarvislabs.ai](https://jarvislabs.ai/)が好きです。
> > 
> > インスタンスの作成とSSHによるアクセスが簡単で高速です。価格も非常に安いと思います。私は主にホームサーバーに移行するまで、このサービスを利用していました。
> > 
> > 
> > 
---
> ## Andreas Bisi
> 
> 過去のNLPコンペティションを考えると、金メダルを獲得するには外部リソースが必要になります。しかし、TF-IDFソリューション（Kaggleのハードウェアを使用）で、運が良ければ銅メダルを獲得できると思います…
> 
> 
> 
---


</div>