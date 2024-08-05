# 要約 
### 要約

**ディスカッション内容**
- **投稿者**: Chris Deotte
- **日付**: 2024年7月16日
- **内容**: Chris Deotteは、公開リーダーボードでスコア0.750以上を達成し、現在59位にランクインしているという自身のノートブックを共有。このノートブックは、質問戦略、ライブラリのインストール、LLMモデルのダウンロード方法、エージェントコード作成の手順など、さまざまな役立つ情報を提供している。

**良い点**
- 質問を絞り込む戦略に関する有用なコードが含まれている。
- LLMの回答能力のEDA（探索的データ分析）が実施されており、アクティブに使用可能なエージェントの監視方法も示されている。

**悪い点**
- 固定キーワードの使用が見られ、プライベートLBで変更される可能性がある。
- 質問が地理的要素に偏っており、物に関連した質問が不足している。

**改善提案**
- ウィキペディアから多くの単語を選び、より広範なキーワードリストを作成。新しい特徴を持つデータフレームを用いて、質問を発展させることが提案されている。

**ユーザーからのフィードバック**
- 他のユーザーが感謝の意を表明し、特にLlama 3モデルの量子化に関する提案や質問があり、ノートブックが初心者にとって役立つと評価されている。 

このディスカッションでは、ノートブックの有用性だけでなく、それを改善するための新たなアイデアや他のユーザーとの対話も含まれている。

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

# Starter Notebook - Llama3-8B - [LB 0.750+] - [Rank 59th]

**Chris Deotte** *Tue Jul 16 2024 09:54:06 GMT+0900 (日本標準時)* (59 votes)

Hi everyone! I'm sharing my current submission which is currently achieving public LB 0.750+ and public LB rank 59th! (And before keyword update, this notebook was achieving 1st place public LB 🥇 😀 ). The notebook is [here](https://www.kaggle.com/code/cdeotte/starter-code-for-llama-8b-llm-lb-0-750). Enjoy!

## Good Stuff

This notebook has some problems (i.e. it uses some fixed keywords), but it also has a lot of helpful code to demonstrate stuff. The helpful things this notebook demonstrates are as follows:

- A strategy how to ask questions to narrow down search (and use a CSV of features behind the scenes).

- How to install pip libraries to be used during submission

- How to download and use any LLM model from Hugging Face

- How to perform EDA on your LLM's answering ability

- How to create agent code and create tarball for submission

- How to run Kaggle's API to watch your agent locally

## Bad Stuff

Some problems with this notebook are:

- uses (an old list of) fixed keywords which may change during private LB. (And have changed on public LB.)

- only asks questions about places (i.e. (1) which sub-category? (city, country, landmark), (2) which continent?, (3) which first letter? It does not ask questions about things) 

## How To Improve

Note that even if private LB keywords change, we can use this notebook's template and strategy to create a notebook which selects thousands or millions of words from Wikipedia and uses that list as a list of all potential keywords. 

Then we create new columns in that dataframe with additional features describing all the words and we create pre-determined questions asking if keyword has these additional featuers. Finally we make guesses based on the keywords in our created dataframe (with additonal column features) and the answerer's responses about features.

# Starter Code

The starter code is [here](https://www.kaggle.com/code/cdeotte/starter-code-for-llama-8b-llm-lb-0-750).



---

 # Comments from other users

> ## mxmm2123
> 
> great job!!!
> 
> 
> 


---

> ## Rishit Jakharia
> 
> Hey!, Thanks for sharing the notebook,
> 
> I noticed you used fp4 quantization in your implementation for the llama 3 model..
> 
> Wanted to ask whether you tried GGUF quantization, if yes what were the results compared to the current implementation
> 
> 
> 
> > ## Chris DeotteTopic Author
> > 
> > Hi. I have not tried GGUF quantization. In another project (i.e. not Kaggle's 20 question comp), I have tried AWQ quantization with Hugging Face's AutoModelForCausalLM and it was very slow compared with fp4. So when we evaluate GGUF, we must also consider its speed to.
> > 
> > 
> > 
> > > ## Rishit Jakharia
> > > 
> > > Okay, thanks !
> > > 
> > > 
> > > 


---

> ## Valentin Baltazar
> 
> This is great for beginners like me! Thank you.
> 
> 
> 


---

> ## torino
> 
> [@cdeotte](https://www.kaggle.com/cdeotte) Thank you for sharing the notebook. I was see you installed python package offline, but in my notebook I can't install new pytorch for the submit environment(It worked well on the normal notebook). Do you have any suggestion? You can see my issue [here](https://www.kaggle.com/competitions/llm-20-questions/discussion/520207)
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# スターターノートブック - Llama3-8B - [LB 0.750+] - [ランク 59位]
**Chris Deotte** *2024年7月16日 火曜日 09:54:06 GMT+0900 (日本標準時)* (59票)
こんにちは、皆さん！現在の提出物を共有します。現在、公開リーダーボードで0.750以上のスコアを達成しており、公開リーダーボードのランクは59位です！(キーワードの更新前は、このノートブックが公開リーダーボードで1位を達成しました🥇 😀)。ノートブックはこちらです：[ここをクリック](https://www.kaggle.com/code/cdeotte/starter-code-for-llama-8b-llm-lb-0-750)。楽しんでください！
## 良い点
このノートブックにはいくつかの問題（固定キーワードを使用しているなど）がありますが、多くの役立つコードも含まれており、以下の内容を示しています：
- 検索を絞り込むために質問をする戦略（裏で使用される特徴のCSVを用いた方法）。
- 提出時に使用するpipライブラリのインストール方法
- Hugging Faceから任意のLLMモデルをダウンロードして使用する方法
- LLMの回答能力に対するEDAの実施方法
- エージェントコードを作成し、提出のためのtarballを作成する方法
- KaggleのAPIを実行して、ローカルでエージェントを監視する方法
## 悪い点
このノートブックのいくつかの問題は以下の通りです：
- 古いリストの固定キーワードを使用しており、プライベートLB中に変更される可能性がある（公開LBでは既に変更されています）。
- 質問が場所に関すること（例： (1) どのサブカテゴリーか？ (都市、国、ランドマーク)、(2) どの大陸か？、(3) 最初の文字は何か？）のみとなっており、物に関する質問はしていない。
## 改良方法
プライベートLBのキーワードが変わったとしても、このノートブックのテンプレートと戦略を使用して、ウィキペディアから数千または数百万の単語を選択し、それを全ての潜在的なキーワードのリストとして使用する新しいノートブックを作成できます。
その後、そのデータフレームにすべての単語を記述する追加の特徴を説明する新しい列を作成し、これらの追加の特徴を持つキーワードかどうかを尋ねる事前定義された質問を作成します。最後に、作成したデータフレームのキーワード（追加の列特徴を持つ）と特徴に関する回答者の反応に基づいて推測を行います。
# スターターコード
スターターコードは[こちら](https://www.kaggle.com/code/cdeotte/starter-code-for-llama-8b-llm-lb-0-750)です。
---
 # その他ユーザーからのコメント
> ## mxmm2123
> 
> 素晴らしい仕事ですね！
> 
> ---
> 
> ## Rishit Jakharia
> 
> こんにちは！ノートブックを共有してくれてありがとう。
> 
> 実装においてLlama 3モデルのfp4量子化を使用していることに気づきました。
> 
> GGUF量子化を試したかどうか、もし試したなら現在の実装と比較した結果はどうだったかを知りたいです。
> 
> > ## Chris Deotte (トピック作成者)
> > 
> > こんにちは。GGUF量子化は試していません。他のプロジェクト（Kaggleの20の質問コンペではない）で、Hugging FaceのAutoModelForCausalLMを使用してAWQ量子化を試しましたが、fp4と比べて非常に遅かったです。したがって、GGUFを評価する際には、速度も考慮に入れる必要があります。
> > 
> > > ## Rishit Jakharia
> > > 
> > > なるほど、ありがとうございます！
> > > > 
> > 
---
> ## Valentin Baltazar
> 
> 初心者の私にとって非常に役立つ情報です！ありがとうございます。
> 
> ---
> ## torino
> 
> [@cdeotte](https://www.kaggle.com/cdeotte) ノートブックを共有してくれてありがとう。あなたがオフラインでPythonパッケージをインストールしたのを見ましたが、私のノートブックでは提出環境用に新しいPyTorchをインストールできません（普通のノートブックではうまくいきました）。何か提案があれば教えてください。私の問題は[こちら](https://www.kaggle.com/competitions/llm-20-questions/discussion/520207)で見ることができます。
> 
> ---


</div>