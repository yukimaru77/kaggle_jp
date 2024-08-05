# 要約 
このディスカッションは、LMSYS - Chatbot Arena Human Preference Predictionsコンペティションにおける分類ヘッドの代替案として、SVR（サポートベクター回帰）の使用について議論しています。

投稿者は、コンペティションで使用されている分類ヘッドが単純な線形層であることに気づき、データ量が多いことを考えると、SVRの方が良いパフォーマンスを発揮するのではないかと考えています。

しかし、SVRのパラメータが分類ヘッドとは独立して訓練されるため、パフォーマンスが低下する可能性があるという懸念も表明しています。

投稿者は、他の参加者がSVRを試したことがあるかどうか、そしてその結果について議論したいと考えています。


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

# Has anyone tried using an SVR (Support Vector Regression) to replace the original classification header?

**lllleeeo** *Sat Jul 20 2024 00:48:44 GMT+0900 (日本標準時)* (1 votes)

Has anyone tried using an SVR (Support Vector Regression) to replace the original classification head? I've noticed that the classification heads currently used in the public notebooks are simple linear fully connected layers, or two layers of linear heads with an activation function and dropout in the middle as someone mentioned in the comments section, and I'm wondering if using an SVR to generate predictions would perform better with the amount of data in the competition. 

I'm about to make an attempt at this but still have some concerns because then the parameters of the model are trained independently of the classification header that is ultimately used, and may blend even worse, so I'm wondering if anyone has experimented with this? We can discuss this together!😀





</div>
<div class="column-right">

# 日本語訳

# SVRを使って元の分類ヘッドを置き換える試みをした人はいますか？

**lllleeeo** *2024年7月20日土曜日 00:48:44 GMT+0900 (日本標準時)* (1票)

公開されているノートブックで現在使用されている分類ヘッドは、単純な線形全結合層か、コメント欄で誰かが言及したように、活性化関数とドロップアウトを中間層に持つ2層の線形ヘッドであることに気づきました。そこで、このコンペティションのデータ量に対して、SVRを使って予測を行う方が良いパフォーマンスを発揮するのではないかと考えています。

私は今まさにこの試みを行おうとしていますが、モデルのパラメータは最終的に使用される分類ヘッドとは独立して訓練されるため、さらに悪化する可能性があるという懸念があります。そのため、誰かがこの方法を試したことがあるかどうかを知りたいと思っています。一緒に議論しましょう！😀 



</div>