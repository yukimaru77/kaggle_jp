# 要約 
**ディスカッション要約: ファイルサイズを削減する方法**

参加者のYuang Wuが、Gemma2とGemma 7b-itモデルを試したが、提出ファイルのサイズが制限を超えたことを報告しました。これに対して、他のユーザーが圧縮アルゴリズムの使用を問うコメントを寄せました。特に、pigz圧縮プログラムを使うことを提案し、圧縮コマンドの例も提供されました。

Yuang Wuは、提出ファイルのサイズ上限が19.5GBであることを指摘しました。それに対し、Chris Deotteは、Kaggleノートブックの出力サイズ制限が20GBである可能性を示唆し、ローカルで作成した100GBのファイルを提出できることを説明しました。要するに、ノートブックの出力制限が問題の一因だとされています。

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

# How to reduce file size

**Yuang Wu** *Sun Jul 14 2024 21:44:07 GMT+0900 (日本標準時)* (1 votes)

I've tried Gemma2 and Gemma 7b-it, and the submission file exceeds in both situation. What could be the solution?



---

 # Comments from other users

> ## Jasper Butcher
> 
> What compression algorithm are you using? The submission file caps out at 100 Gb's, and most ~8b parameter models take up only around 10-15 Gbs.
> 
> The pigz compression programme is what most people are using for this competition:
> 
> ```
> !tar --use-compress-program='pigz --fast --recursive | pv' -cf submission.tar.gz -C /kaggle/input/path/to/weights . -C /kaggle/working/submission .
> 
> ```
> 
> You can also just use the following to clone every file in your submission/ directory, where -9 indicates the maximum level of compression:
> 
> ```
> !tar -cf - -C submission . | pigz -9 > submission.tar.gz 
> 
> ```
> 
> 
> 
> > ## Yuang WuTopic Author
> > 
> > What? My cap is 19.5GB…
> > 
> > 
> > 
> > > ## Chris Deotte
> > > 
> > > Yuang, maybe you are referring the the limit output size to a Kaggle notebook. If you create a 100GB file locally, you can upload it and submit to this comp. However the output folder of a Kaggle notebook caps at 20GB i think.
> > > 
> > > 
> > > 


---



</div>
<div class="column-right">

# 日本語訳

# ファイルサイズを削減する方法
**Yuang Wu** *2024年7月14日 21:44:07 JST* (1票)
Gemma2とGemma 7b-itを試しましたが、提出ファイルがどちらも制限を超えています。解決策は何でしょうか？

---
# 他のユーザーからのコメント
> ## Jasper Butcher
> 
> どの圧縮アルゴリズムを使用していますか？提出ファイルの上限は100GBで、ほとんどの約8bパラメータモデルは10-15GB程度です。
> 
> このコンペティションでは、多くの人がpigz圧縮プログラムを使用しています：
> 
> ```
> !tar --use-compress-program='pigz --fast --recursive | pv' -cf submission.tar.gz -C /kaggle/input/path/to/weights . -C /kaggle/working/submission .
> ```
> 
> または、次のコマンドを使用して、submissionディレクトリ内のすべてのファイルをコピーすることもできます。-9は最大圧縮レベルを示します：
> 
> ```
> !tar -cf - -C submission . | pigz -9 > submission.tar.gz 
> ```

> 
> > ## Yuang Wu (トピック作成者)
> > 
> > 何ですって？私の上限は19.5GBです...
> > 
> > 
> > > ## Chris Deotte
> > > 
> > > Yuangさん、もしかするとKaggleノートブックへの出力サイズの制限を指しているのかもしれません。もし100GBのファイルをローカルで作成した場合、それをアップロードしてこのコンペに提出できます。しかし、Kaggleノートブックの出力フォルダーは20GBに制限されていると思います。
> > > 
> > > > 
---


</div>