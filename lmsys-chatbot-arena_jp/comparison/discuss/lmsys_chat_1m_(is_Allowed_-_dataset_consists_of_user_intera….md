# 要約 
このディスカッションは、Kaggle の LMSYS チャットボット アリーナの人間による好み予測チャレンジで使用できる、LMSYS チャット 1M データセットについて議論しています。

**データセットの概要:**

* LMSYS チャット 1M は、25 の最先端の LLM から 100 万回の会話を含む、大規模な現実世界の LLM 会話データセットです。
* データは、2023 年 4 月から 8 月にかけて、ChatBot Arena ウェブサイトから収集されました。
* データセットには、150 以上の言語で 210,000 人のユーザーによる会話が含まれています。
* データセットには、ヒューマン・プレファレンス・アノテーションはありません。

**ディスカッションの主なポイント:**

* SeshuRaju は、LMSYS チャット 1M データセットが Kaggle コンペティションで使用できるかどうかを尋ねています。
* データセットのキーバリューと論文へのリンクを提供しています。
* データセットの潜在的なバイアスと欠陥について言及しています。
* Kaggle データセットと LMSYS チャット 1M データセットを比較するための質問を提起しています。
* Lisa Dunlap（コンペティションの主催者）は、データセットが使用可能であることを確認しています。
* Gaurav Rawat は、Hugging Face の LMSYS データセットについて同様の質問をしたことを共有しています。

**結論:**

このディスカッションは、LMSYS チャット 1M データセットが Kaggle コンペティションで使用可能であることを確認しています。ただし、データセットの潜在的なバイアスと欠陥について注意する必要があります。参加者は、データセットを適切に理解し、その制限を考慮してモデルを構築する必要があります。


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

# lmsys chat 1m (is Allowed? - dataset consists of user interactions from the ChatBot Arena) [Solved - Allowed]

**SeshuRaju 🧘‍♂️** *Fri May 03 2024 14:00:35 GMT+0900 (日本標準時)* (24 votes)

## [IMSYS Chat 1M](https://huggingface.co/datasets/lmsys/lmsys-chat-1m)

## KeyValue

| Metric | Value |
| --- | --- |
| Conversations | 1,000,000 |
| Models | 25 |
| Users | 210,479 |
| Languages | 154 |
| Avg. # Turns per Sample | 2.0 |
| Avg. # Tokens per Prompt | 69.5 |
| Avg. # Tokens per Response | 214.5 |

## [Paper - LMSYS-CHAT-1M: A LARGE-SCALE REAL-WORLD LLM CONVERSATION DATASET](https://arxiv.org/pdf/2309.11998)

- LMSYS-Chat-1M is collected from April to August 2023 - on website [https://chat.lmsys.org/](https://chat.lmsys.org/)

- The dataset contains raw conversation text without any processing. To ensure the safe release of

  data, we have made our best efforts to remove conversations that contain personally identifiable

  information (PII).

- The dataset includes one million conversations from 25 state-of-the-art LLMs with 210K users

  across more than 150 languages.

- We remove prompts that are either too short (fewer than 32 characters) or too long (more than 1536 characters).

- Biased user distribution : The majority of users of our website are LLM hobbyists and researchers who are interested in trying and testing the latest LLMs. This suggests that the data

  might not fully represent the broader population. For instance, everyday users or individuals

  from different professions might interact with the LLMs in varied ways. Consequently, results

  derived from this dataset might not generalize across all user groups.

- Containing repeated and low-quality data : The lack of user registration and data filtering can

  result in a significant amount of low-quality and duplicate data. However, we choose to not

  apply any filtering on purpose to reflect the real-world distribution.

- No human preference annotations. This dataset contains raw conversations without any human

  preference annotations. While our website does collect some user votes, we plan to examine

  the quality further before releasing them. We encourage the community to check the human

  preference data released in (Zheng et al., 2023).

# We can compare the Kaggle dataset with 1m dataset

- is PII added and removed more similar prompts or questions as suggested by paper ?

- Generate targets for the filtered dataset using GPT-4

- We can probe LB to check is this data topics exists in private LB ( as 20 clusters  for random 100k as per paper )



---

 # Comments from other users

> ## Lisa DunlapCompetition Host
> 
> Hello! Organizer here: yes it is allowed :)
> 
> 
> 


---

> ## Gaurav Rawat
> 
> Had exactly the same question about some of the lmsys datasets on hugging face ideally most are open I am guessing should be fine
> 
> 
> 
> > ## SeshuRaju 🧘‍♂️Topic Author
> > 
> > I expected the same, till now organiser not conformed. maybe we can consider it as Yes
> > 
> > 
> > 


---



</div>
<div class="column-right">

# 日本語訳

# LMSYS チャット 1M (使用可能？ - データセットは ChatBot Arena からのユーザーインタラクションで構成されています) [解決済み - 使用可能]
**SeshuRaju 🧘‍♂️** *2024年5月3日 金曜日 14:00:35 GMT+0900 (日本標準時)* (24票)
## [IMSYS チャット 1M](https://huggingface.co/datasets/lmsys/lmsys-chat-1m)
## キーバリュー
| メトリック | 値 |
| --- | --- |
| 会話 | 1,000,000 |
| モデル | 25 |
| ユーザー | 210,479 |
| 言語 | 154 |
| サンプルあたりの平均ターン数 | 2.0 |
| プロンプトあたりの平均トークン数 | 69.5 |
| 応答あたりの平均トークン数 | 214.5 |
## [論文 - LMSYS-CHAT-1M: 大規模な現実世界のLLM会話データセット](https://arxiv.org/pdf/2309.11998)
- LMSYS-Chat-1M は、2023年4月から8月にかけて、ウェブサイト [https://chat.lmsys.org/](https://chat.lmsys.org/) から収集されました。
- データセットには、処理されていない生の会話テキストが含まれています。データの安全な公開を確保するために、個人を特定できる情報 (PII) を含む会話を削除するために最善を尽くしました。
- データセットには、150以上の言語で210,000人のユーザーによる、25の最先端のLLMからの100万回の会話が含まれています。
- 32文字未満または1536文字を超えるプロンプトは削除しています。
- バイアスのかかったユーザー分布: ウェブサイトのユーザーの大部分は、最新のLLMを試してテストすることに興味のあるLLM愛好家や研究者です。これは、データがより広範な人口を完全に代表していない可能性を示唆しています。たとえば、日常的なユーザーやさまざまな職業の人々は、LLMとさまざまな方法でやり取りする可能性があります。その結果、このデータセットから得られた結果は、すべてのユーザーグループにわたって一般化されない可能性があります。
- 繰り返しと低品質のデータを含む: ユーザー登録とデータフィルタリングの不足により、低品質で重複したデータが大量に発生する可能性があります。ただし、現実世界の分布を反映するために、意図的にフィルタリングを適用しないことを選択しました。
- ヒューマン・プレファレンス・アノテーションはありません。このデータセットには、ヒューマン・プレファレンス・アノテーションのない生の会話が含まれています。ウェブサイトではユーザー投票を収集していますが、リリースする前に品質をさらに調査する予定です。コミュニティは、(Zheng et al., 2023) で公開されているヒューマン・プレファレンス・データを確認することをお勧めします。
# Kaggle データセットと 1M データセットを比較できます
- 論文で示唆されているように、PII は追加および削除され、より類似したプロンプトまたは質問ですか？
- GPT-4 を使用して、フィルタリングされたデータセットのターゲットを生成します。
- プライベート LB にこのデータのトピックが存在するかどうかを確認するために、LB を調査できます (論文によると、ランダムに選択した 100,000 件のデータは 20 のクラスタに分類されます)。
---
 # 他のユーザーからのコメント
> ## Lisa Dunlapコンペティションホスト
> 
> こんにちは！主催者です: はい、使用可能です :)
> 
> 
> 
---
> ## Gaurav Rawat
> 
> Hugging Face の一部の LMSYS データセットについて、まったく同じ質問がありました。理想的には、ほとんどはオープンなので、問題ないと思います。
> 
> 
> 
> > ## SeshuRaju 🧘‍♂️トピック作成者
> > 
> > 私も同じことを期待していましたが、主催者はまだ確認していません。おそらく、使用可能と考えてもよいでしょう。
> > 
> > 
> > 
---




</div>