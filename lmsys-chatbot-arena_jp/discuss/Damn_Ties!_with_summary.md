# 要約 
このコンペティションのディスカッションでは、参加者たちがアノテーターによるラベル付けのノイズ、特に引き分けの予測の難しさについて議論しています。

**cm391** は、アノテーターの好みが主観的で、基準が人によって異なるため、引き分けを予測することが難しいと指摘しています。具体例として、2つの応答のどちらが優れているか判断しにくいケースを挙げています。

**Hadi Ai** は、アノテーターのプロンプトから情報を得て、引き分けクラスを予測する小さなモデルを作成することを提案しています。

**justin1357** は、引き分けの予測は人間にとっても難しい課題であり、アノテーターの基準は時間とともに変化するため、モデルを信頼することが難しいと述べています。

このディスカッションは、コンペティション参加者にとって、引き分けの予測という課題に対する理解を深め、新たな解決策を探るための重要な機会となっています。


---
# 難しい引き分け！
**cm391** *2024年7月25日 木曜日 05:02:47 日本標準時* (6票)

このコンペティションで使用されているラベルは、多様なアノテーターによって割り当てられており、その名前が示すように、好みをベースにしています。以下の2つの例からわかるように、引き分けを正しく予測することは難しい場合があります。

もしかしたら、Morphalumpaliciousness は単に短すぎるのでしょうか？
2文多すぎるのでしょうか？

皆さんはこのようなノイズをどのように処理していますか？私は引き分けを予測する際にランダムより良い結果が出せません…

---
# 他のユーザーからのコメント
> ## Hadi Ai
> 
> アノテーターのプロンプトから何か情報を得られるのではないかと考えています。そして、それを小さなモデルで使用して引き分けクラスを予測し、それを現在行っていることと組み合わせるのです。いずれにせよ、このコンペティションでは探索する時間がほとんどありません :-)
> 
> 
> 
---
> ## justin1357
> 
> 引き分けは本当に予測が難しいです… 人間として、私もいつ引き分けになるのかはわかりません。誰もが基準が異なり、その基準は時間の経過とともに変化します。私はモデルを信頼したいです…
> 
> 
> 
--- 
