# 要約 
このディスカッションは、KaggleのLMSYS - Chatbot Arena Human Preference Predictionsコンペティションにおける、RickPackユーザーが遭遇した提出エラーに関するものです。

RickPackは、PythonとRの両方で作成したノートブックがローカルでは正常に動作するものの、提出時に「ノートブックで例外が発生しました」というエラーが発生することを報告しました。このエラーはログには表示されず、提出画面でのみ表示されるため、原因を特定することが困難でした。

他のユーザーからのコメントでは、David.Ricardo.H.Xも同様の問題に遭遇したことが明らかになりました。

RickPackは、確率の行の合計が常に1にならないことに気づき、これが問題の原因である可能性を指摘しました。Fae Gazeは、正規化の問題やRとPythonのライブラリ間の数値精度や最適化の違いが原因である可能性を指摘しました。

最終的にRickPackは、すべてのレコードに対する予測が得られていなかったことが原因であることを突き止めました。テストを予測に左結合し、予測が欠落している場合は予測を補完することで、問題は解決しました。

このディスカッションから、以下のことがわかります。

* Kaggleの提出プロセスでは、ローカルでの実行と異なる動作をする場合がある。
* 提出エラーの原因を特定することは困難な場合がある。
* 確率の正規化やデータの結合などの問題が、提出エラーの原因となる可能性がある。
* RとPythonのライブラリ間の違いが、異なる結果を生み出す可能性がある。

このディスカッションは、Kaggleコンペティションに参加する際に、提出前にコードを徹底的にテストし、潜在的な問題を事前に解決しておくことの重要性を示しています。


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

# Unspecified exception, only when submitted (later = Submission Scoring error)

**RickPack** *Tue May 21 2024 01:00:22 GMT+0900 (日本標準時)* (5 votes)

My [Python notebook](https://www.kaggle.com/code/rickpack/python-average-prob-per-word-no-gpu) and [R notebook](https://www.kaggle.com/code/rickpack/r-average-prob-per-word-no-gpu/) run without issue but when I submit them, I get a "Notebook Threw Exception" error that is only visible on the Submissions screen. The log shows no errors.

Does anyone have a potential solution?

R:             [https://www.kaggle.com/code/rickpack/r-average-prob-per-word-no-gpu/](https://www.kaggle.com/code/rickpack/r-average-prob-per-word-no-gpu/)

Python:   [https://www.kaggle.com/code/rickpack/python-average-prob-per-word-no-gpu](https://www.kaggle.com/code/rickpack/python-average-prob-per-word-no-gpu)

[@sohier](https://www.kaggle.com/sohier), [@addisonhoward](https://www.kaggle.com/addisonhoward) 



---

 # Comments from other users

> ## David.Ricardo.H.X
> 
> i got the same problem
> 
> 
> 


---

> ## RickPackTopic Author
> 
> Reopening this [@sohier](https://www.kaggle.com/sohier), [@addisonhoward](https://www.kaggle.com/addisonhoward) in hopes of getting thoughts, please? Both the R and Python notebooks are failing with a Submission Scoring Error after minor modifications. I see that the row sums of the probabilities are not always exactly 1 (e.g., 1.002, 0.999, 1.000). If that could be the problem, could you please see if you can comment on what might repair that problem? I have tried various kinds of rounding and standardizing as you will see in code. Thank you!
> 
> R:           [https://www.kaggle.com/code/rickpack/r-average-prob-per-word-no-gpu?scriptVersionId=179034682](https://www.kaggle.com/code/rickpack/r-average-prob-per-word-no-gpu?scriptVersionId=179034682)
> 
> Python:  [https://www.kaggle.com/code/rickpack/python-average-prob-per-word-no-gpu?scriptVersionId=179035436](https://www.kaggle.com/code/rickpack/python-average-prob-per-word-no-gpu?scriptVersionId=179035436)
> 
> 
> 
> > ## Fae Gaze
> > 
> > [@rickpack](https://www.kaggle.com/rickpack) , I think that the reason that the issue of row sum of the probabilities suggested that you may have a normalization issue. Also different scores of R and python may suggest that they handle the data differently. I mean, even if the same statistical methods or the same algorithm, their implementation in r and Python libraries can differ in terms of numerical precision or optimizations. 
> > 
> > 
> > 


---

> ## RickPackTopic Author
> 
> Fixed! I have not studied why but I appeared to not get a prediction for every record. By left joining test on my predictions and imputing predictions where missing, both notebooks produced unimpresssive scores. Interesting that little differences between the notebooks yielded different scores.
> 
> 
> 
> > ## Fae Gaze
> > 
> > [@rickpack](https://www.kaggle.com/rickpack) , I suggest that the columns used to join datasets are correctly specified and contain matching data formats. After the join, I think it is better to identify any rows where predictions are missing
> > 
> > 
> > 
> > > ## RickPackTopic Author
> > > 
> > > Thank you for your reply. I did not have any NA values in the data frame because of a replacement the code included. However, this version justworked ([https://www.kaggle.com/code/rickpack/r-average-prob-per-prompt-word-no-gpu?scriptVersionId=185084007](https://www.kaggle.com/code/rickpack/r-average-prob-per-prompt-word-no-gpu?scriptVersionId=185084007)) after I included a 3rd decimal place (zeros!) in the assignment of values to the 3 target columns where NA occurs. Compare to this version that failed to generate a score ([https://www.kaggle.com/code/rickpack/r-average-prob-per-prompt-word-no-gpu?scriptVersionId=184945388](https://www.kaggle.com/code/rickpack/r-average-prob-per-prompt-word-no-gpu?scriptVersionId=184945388))
> > > 
> > > 
> > > 


---



</div>
<div class="column-right">

# 日本語訳

# 提出時にのみ発生する不明な例外（後から提出エラーになる）
**RickPack** *2024年5月21日 火曜日 01:00:22 GMT+0900 (日本標準時)* (5票)

私の[Pythonノートブック](https://www.kaggle.com/code/rickpack/python-average-prob-per-word-no-gpu)と[Rノートブック](https://www.kaggle.com/code/rickpack/r-average-prob-per-word-no-gpu)は問題なく実行されますが、提出すると、「ノートブックで例外が発生しました」というエラーが表示されます。このエラーは提出画面でのみ表示され、ログにはエラーが表示されません。
解決策をご存知の方はいらっしゃいますか？
R:             [https://www.kaggle.com/code/rickpack/r-average-prob-per-word-no-gpu/](https://www.kaggle.com/code/rickpack/r-average-prob-per-word-no-gpu/)
Python:   [https://www.kaggle.com/code/rickpack/python-average-prob-per-word-no-gpu](https://www.kaggle.com/code/rickpack/python-average-prob-per-word-no-gpu)
[@sohier](https://www.kaggle.com/sohier), [@addisonhoward](https://www.kaggle.com/addisonhoward) 
---
 # 他のユーザーからのコメント
> ## David.Ricardo.H.X
> 
> 私も同じ問題に遭遇しました。
> 
> 
> 
---
> ## RickPackTopic 作成者
> 
> 再開します [@sohier](https://www.kaggle.com/sohier), [@addisonhoward](https://www.kaggle.com/addisonhoward) ご意見をお聞かせください。RとPythonの両方のノートブックで、わずかな修正を加えた後に提出エラーが発生しています。確率の行の合計が常に正確に1にならない（例：1.002、0.999、1.000）ことに気づきました。これが問題である場合、この問題を解決する可能性についてコメントしていただけますか？コードでわかるように、さまざまな丸めと標準化を試してみました。ありがとうございます！
> 
> R:           [https://www.kaggle.com/code/rickpack/r-average-prob-per-word-no-gpu?scriptVersionId=179034682](https://www.kaggle.com/code/rickpack/r-average-prob-per-word-no-gpu?scriptVersionId=179034682)
> 
> Python:  [https://www.kaggle.com/code/rickpack/python-average-prob-per-word-no-gpu?scriptVersionId=179035436](https://www.kaggle.com/code/rickpack/python-average-prob-per-word-no-gpu?scriptVersionId=179035436)
> 
> 
> 
> > ## Fae Gaze
> > 
> > [@rickpack](https://www.kaggle.com/rickpack) 、確率の行の合計に関する問題から、正規化の問題がある可能性が示唆されていると思います。また、RとPythonの異なるスコアは、データの処理方法が異なることを示唆している可能性があります。つまり、同じ統計的手法やアルゴリズムであっても、RとPythonのライブラリでの実装は、数値精度や最適化の点で異なる場合があります。 
> > 
> > 
> > 
---
> ## RickPackTopic 作成者
> 
> 解決しました！理由はまだ調査していませんが、すべてのレコードに対する予測が得られていなかったようです。テストを予測に左結合し、予測が欠落している場合は予測を補完することで、両方のノートブックは印象的なスコアを生成しました。ノートブック間のわずかな違いが異なるスコアを生み出したのは興味深いことです。
> 
> 
> 
> > ## Fae Gaze
> > 
> > [@rickpack](https://www.kaggle.com/rickpack) 、データセットを結合するために使用した列が正しく指定され、一致するデータ形式が含まれていることを確認することをお勧めします。結合後、予測が欠落している行を特定することをお勧めします。
> > 
> > 
> > 
> > > ## RickPackTopic 作成者
> > > 
> > > ご回答ありがとうございます。コードに含まれている置換のため、データフレームにNA値はありませんでした。しかし、このバージョンは、NAが発生する3つのターゲット列に値を割り当てる際に、3桁目（ゼロ！）を含めたため、正常に動作しました ([https://www.kaggle.com/code/rickpack/r-average-prob-per-prompt-word-no-gpu?scriptVersionId=185084007](https://www.kaggle.com/code/rickpack/r-average-prob-per-prompt-word-no-gpu?scriptVersionId=185084007))。スコアが生成されなかったこのバージョンと比較してください ([https://www.kaggle.com/code/rickpack/r-average-prob-per-prompt-word-no-gpu?scriptVersionId=184945388](https://www.kaggle.com/code/rickpack/r-average-prob-per-prompt-word-no-gpu?scriptVersionId=184945388))
> > > 
> > > 
> > > 
---



</div>