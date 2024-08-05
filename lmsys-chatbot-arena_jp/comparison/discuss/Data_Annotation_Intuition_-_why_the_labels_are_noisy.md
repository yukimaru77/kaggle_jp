# 要約 
## Kaggleコンペティション「LMSYS - Chatbot Arena 人間による好み予測チャレンジ」のディスカッション要約

このディスカッションは、コンペティションで使用されるデータのラベルに存在するノイズについて議論しています。

**主なポイント:**

* **ラベルの質:** データは、LLMの使用や理解に精通していないユーザーによってアノテーションされています。ユーザーは、質問しているトピックの専門家ではない場合も多く、アノテーションの質に影響を与えています。
* **アノテーター間一致率:** ユーザーの好みは主観的であるため、アノテーター間一致率を評価することは困難です。
* **ノイズの多いラベル:** これらの要因により、データにはノイズの多いラベルが含まれており、モデルのトレーニングに影響を与えます。
* **対処方法:** ノイズの多いラベルに対処するために、アクティブラーニング、アンサンブル、損失の変更などのテクニックが提案されています。
* **データクレンジング:** データクレンジングは有効な手段ですが、過剰なクレンジングはモデルのパフォーマンスに悪影響を与える可能性があります。
* **テストデータ:** テストデータにもノイズの多いラベルが含まれている可能性があり、モデルの評価に影響を与える可能性があります。

**ディスカッションの参加者:**

* Valentin Werner: トピック作成者。データアノテーションの専門家であり、ラベルノイズの問題を指摘しています。
* Lisa Dunlap: コンペティションホスト。ラベルノイズの問題を認識し、対処方法を模索しています。
* Fae Gaze: SnorkelなどのフレームワークやFocal Lossなどのロバストな損失関数を提案しています。
* Takamichi Toda: 短いプロンプトに対するLLMの応答の傾向について分析しています。
* JunHua Liao: ラベルノイズの解決策として、ラベルの変更やノイズデータの削除を提案しています。
* xiaotingting: データの質がモデルのパフォーマンスに大きな影響を与えることを強調しています。
* AbChk: テストデータにもノイズの多いラベルが含まれている可能性を指摘しています。

**結論:**

このディスカッションは、コンペティションのデータに存在するラベルノイズの問題を浮き彫りにし、参加者に対してノイズに対処するための戦略を検討するよう促しています。データの質はモデルのパフォーマンスに大きな影響を与えるため、参加者はノイズの多いラベルに対処するための適切なテクニックを選択することが重要です。


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

# Data Annotation Intuition - why the labels are noisy

**Valentin Werner** *Mon May 13 2024 23:10:26 GMT+0900 (日本標準時)* (32 votes)

I see that there are several ongoing discussions regarding label quality. As someone, who has spent a significant amount of time annotating data (and asking other people to annotate data for me), I want to share an opinion and intution of mine too.

In Data Annotation, you generally want professionals to annotate the data. They are supposed to (but sometimes do not do so) read the data carefully, select the labels carefully etc.; the annotated data is considered the GROUND TRUTH as these experts should be able to objectively decide the correct label (given same understand of the problem and annotation task). 

Then you generally compute an Inter-Annotator Agreement (are n people giving the same label on the same text), which was often seen as a ceiling for performance. Although this is not always the case in reality, this makes sense, because that means that your model is able to learn the intersection of knowledge from multiple annotators. 

Why is this important? The data we are training on is annotated by random people who wanted to try LLMs. While LMSYS is a great tool that I often use and recommend, it is for our problem mostly an annotation tool where the annotator can decide what question they want to annotate for and the data to annotate is generated in real time. 

However, there are several issues with this for our challenge:

- Users are not experts in using or understanding LLMs

- Users are often not experts in the topic they are asking about (and are often not fact-checking the responses)

- Unless users specify the same prompt and receive the same response, there is no way to evaluate Inter-Annotator Agreement

- LMSYS does not allow to undo or redo annotations (e.g., misclicked the wrong side)

- And most importantly: users have different preferences. This annotation task is not objective at all but PURELY subjective

This means we have NOISY labels and should employ techniques to deal with this; there are techniques such as active learning, ensembling, changing loss etc. which might work to address this issue - all of this needs to be tested (although ensembling is something we will do anyways 😉).



---

 # Comments from other users

> ## aotiandragon
> 
> Thanks a lot, It helped me to know the datas
> 
> 
> 


---

> ## Pranav Belhekar
> 
> Thanks for sharing your point. It helped me to analyze the competition.
> 
> 
> 


---

> ## Fae Gaze
> 
> Excellent insights on label noise! You might also explore robust loss functions like focal loss to mitigate noise impact, and consider frameworks like Snorkel to efficiently manage training data through programmable labeling functions
> 
> 
> 
> > ## Valentin WernerTopic Author
> > 
> > Have not heard of Snorkel yet - can you recommend some literature? 
> > 
> > 
> > 


---

> ## Takamichi Toda
> 
> Thank you for sharing. And I was thinking the same thing just now.
> 
> There are some samples in the training data consisting only of very short prompts (one word). A typical example is when the prompt is just "hey". The responses of LLMs to this can generally be divided into two patterns:
> 
> Simply respond with "Hello!".
> After saying "Hello", provide a cue to continue the conversation, such as "How can I assist you today?".
> 
> I think 2 seems to be better, but the training data shows that there were a reasonable number of tie and cases where 1 was winning.
> 
> |  | n_sample | id |
> | --- | --- | --- |
> | hello_lose | 5 | 189242591, 211357242, 326037335, 458677274, 3947327386 |
> | tie | 4 | 1329170872, 3422926530, 4197301939, 4265282380 |
> | hello_win | 2 | 1655058446, 2171261721 |
> 
> The "hay" pattern trend seems to be more to my liking (2 mostly), but there are many other patterns like this that need to be treated as a NOISY label, as you say.
> 
> 
> 
> > ## Valentin WernerTopic Author
> > 
> > And I think is one on the more obvious side, where people just voted a side eventhough both models give the same answer. These people were obviously not thinking of poor ML Developers that need to explain why they did it 😉
> > 
> > I think evaluating how truthful the responses are (if there is a good way to do it) could also be a good feature for training our models
> > 
> > 
> > 


---

> ## Lisa DunlapCompetition Host
> 
> I think this is an amazing point: one of the big challenges with this challenge (no pun intended) - the data is crowdsourced with very minimal filtering so learning how to deal with label noise is incredibly important!
> 
> 
> 


---

> ## JunHua Liao
> 
> I have also discovered the issue of labels noise, mainly due to the same prompt and reponses, where there is a winner, which should be winner_tie. The two solutions currently in mind are: (1). Change the label to winner_tie; (2) Delete noise data
> 
> 
> 
> > ## Lisa DunlapCompetition Host
> > 
> > It may also be beneficial to look in to prompt deduplication or down weighting overrepresented prompts
> > 
> > 
> > 


---

> ## xiaotingting
> 
> At present, cleaning data and selecting models have the greatest impact on the results. I feel that no matter what field you are in, even if you use a large model, the quality of the data is very important.
> 
> 
> 
> > ## Valentin WernerTopic Author
> > 
> > Looking forward to see how you cleaned data, we tried it a bit but were not able to get it to a point where it actually helped
> > 
> > 
> > 
> > > ## Fae Gaze
> > > 
> > > Hi, that is right. Too much cleaning will affect on the score adversely
> > > 
> > > 
> > > 


---

> ## AbChk
> 
> Thanks for sharing your point. It seems like this issue makes us wonder if the test data also has noisy labels?
> 
> 
> 
> > ## Valentin WernerTopic Author
> > 
> > very likely so. I (maybe not so) boldly assume that they did not manually check 25k samples for quality. It is like chosen based on label distribution and models.
> > 
> > 
> > 
> > ## Fae Gaze
> > 
> > the test is also noisy. But, we are not able to clean the noise. Even cleaning the training will affect the score
> > 
> > 
> > 


---



</div>
<div class="column-right">

# 日本語訳

# データアノテーションの直感 - ラベルがノイズである理由
**Valentin Werner** *2024年5月13日(月) 23:10:26 JST* (32 votes)

ラベルの質に関する議論がいくつか進行しているのを見ました。データのアノテーションにかなりの時間を費やしてきた（そして他の人にデータのアノテーションを依頼してきた）私としても、自分の意見と直感を共有したいと思います。

データアノテーションでは、一般的に専門家にデータのアノテーションを依頼します。彼らはデータをよく読み、ラベルを慎重に選択するなどするはずですが（しかし、そうしない場合もあります）、アノテーションされたデータは**グランドトゥルース**とみなされます。なぜなら、これらの専門家は、（問題とアノテーションタスクの理解が同じであれば）正しいラベルを客観的に判断できるはずだからです。

その後、一般的に**アノテーター間一致率**（n人の人が同じテキストに同じラベルを付けているか）を計算します。これは、しばしばパフォーマンスの上限とみなされてきました。現実には必ずしもそうではありませんが、これは理にかなっています。なぜなら、それはあなたのモデルが複数のアノテーターからの知識の交差部分を学習できることを意味するからです。

なぜこれが重要なのでしょうか？私たちがトレーニングしているデータは、LLMを試したいと思ったランダムな人々によってアノテーションされています。LMSYSは私がよく使用し、推奨する素晴らしいツールですが、私たちの問題にとっては、アノテーターがアノテーションしたい質問を決定でき、アノテーションするデータがリアルタイムで生成されるアノテーションツールです。

しかし、私たちの課題にはいくつかの問題があります。

- ユーザーはLLMの使用や理解の専門家ではありません。
- ユーザーは、質問しているトピックの専門家ではないことが多く（そして、応答を事実確認していないことがよくあります）。
- ユーザーが同じプロンプトを指定して同じ応答を受け取らない限り、アノテーター間一致率を評価する方法はありません。
- LMSYSでは、アノテーションのやり直しや取り消しはできません（例：間違った側に誤ってクリックした場合）。
- そして最も重要なことですが、ユーザーには異なる好みがあります。このアノテーションタスクは、まったく客観的ではなく、完全に主観的です。

これは、私たちが**ノイズの多いラベル**を持っていることを意味し、この問題に対処するためのテクニックを採用する必要があります。アクティブラーニング、アンサンブル、損失の変更など、この問題に対処するために機能する可能性のあるテクニックがあります。これらすべてをテストする必要があります（アンサンブルはともかく、私たちは行うつもりです😉）。

---
# 他のユーザーからのコメント
> ## aotiandragon
> 
> ありがとう。データについて知ることができました。
> 
> 
> 
---
> ## Pranav Belhekar
> 
> ご意見を共有していただきありがとうございます。コンペティションを分析するのに役立ちました。
> 
> 
> 
---
> ## Fae Gaze
> 
> ラベルノイズに関する素晴らしい洞察です！ノイズの影響を軽減するために、Focal Lossのようなロバストな損失関数を探求することもできますし、Snorkelのようなフレームワークを使用して、プログラム可能なラベリング関数を通じてトレーニングデータを効率的に管理することもできます。
> 
> 
> 
> > ## Valentin Wernerトピック作成者
> > 
> > Snorkelについてはまだ聞いたことがありません。文献を推薦していただけますか？
> > 
> > 
> > 
---
> ## Takamichi Toda
> 
> ご共有いただきありがとうございます。私も今、同じことを考えていました。
> 
> トレーニングデータには、非常に短いプロンプト（1語）のみで構成されるサンプルがいくつかあります。典型的な例としては、プロンプトが「hey」だけのものがあります。LLMはこのようなプロンプトに対する応答を、一般的に2つのパターンに分類できます。
> 
> 単に「Hello!」と応答する。
> 「Hello」と言った後、「今日は何かお手伝いできますか？」のように、会話を続けるための合図を提供する。
> 
> 2の方が良いと思いますが、トレーニングデータでは、同点と1が勝っているケースがかなりあることが示されています。
> 
> |  | n_sample | id |
> | --- | --- | --- |
> | hello_lose | 5 | 189242591, 211357242, 326037335, 458677274, 3947327386 |
> | tie | 4 | 1329170872, 3422926530, 4197301939, 4265282380 |
> | hello_win | 2 | 1655058446, 2171261721 |
> 
> 「hay」パターンの傾向は、私の好み（主に2）に合っているように思えますが、このようにノイズの多いラベルとして扱う必要があるパターンは他にもたくさんあります。
> 
> 
> 
> > ## Valentin Wernerトピック作成者
> > 
> > そして、これは、両方のモデルが同じ答えを出しているにもかかわらず、人々が一方の側に投票したという、より明白な例だと思います。これらのユーザーは、明らかに、なぜそうしたのかを説明する必要があるかわいそうなML開発者のことを考えていませんでした😉
> > 
> > 応答の真実性を評価する方法（もし良い方法があれば）は、私たちのモデルをトレーニングするための良い特徴になると思います。
> > 
> > 
> > 
---
> ## Lisa Dunlapコンペティションホスト
> 
> これは素晴らしいポイントだと思います。この課題の大きな課題の1つ（言葉遊びではありません）は、データが非常に最小限のフィルタリングでクラウドソーシングされているため、ラベルノイズに対処する方法を学ぶことが非常に重要です！
> 
> 
> 
---
> ## JunHua Liao
> 
> ラベルノイズの問題も発見しました。これは、同じプロンプトと応答で、勝者がいる場合に、winner_tieになるべきなのに、勝者がいることが原因です。現在考えている2つの解決策は、(1) ラベルをwinner_tieに変更する、(2) ノイズデータを削除することです。
> 
> 
> 
> > ## Lisa Dunlapコンペティションホスト
> > 
> > プロンプトの重複排除や、過剰に表現されているプロンプトの重み付けを下げることも有益かもしれません。
> > 
> > 
> > 
---
> ## xiaotingting
> 
> 現在、データのクレンジングとモデルの選択が、結果に最も大きな影響を与えています。どんな分野であっても、たとえ大きなモデルを使用しても、データの質が非常に重要だと感じています。
> 
> 
> 
> > ## Valentin Wernerトピック作成者
> > 
> > データをどのようにクレンジングしたかを見るのが楽しみです。私たちは少し試してみましたが、実際に役立つレベルには到達できませんでした。
> > 
> > 
> > 
> > > ## Fae Gaze
> > > 
> > > はい、その通りです。クレンジングしすぎると、スコアに悪影響を与えます。
> > > 
> > > 
> > > 
---
> ## AbChk
> 
> ご意見を共有していただきありがとうございます。この問題から、テストデータにもノイズの多いラベルがあるのではないかと疑問に思うようになりました。
> 
> 
> 
> > ## Valentin Wernerトピック作成者
> > 
> > 非常に可能性が高いです。私は（それほどではないかもしれませんが）大胆にも、彼らは25,000個のサンプルを手動で品質チェックしていないと仮定しています。ラベルの分布とモデルに基づいて選択されたようなものです。
> > 
> > 
> > 
> > ## Fae Gaze
> > 
> > テストもノイズがあります。しかし、ノイズをクレンジングすることはできません。トレーニングをクレンジングしても、スコアに影響を与えます。
> > 
> > 
> > 
---



</div>