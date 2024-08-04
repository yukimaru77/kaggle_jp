# ファイルサイズを減らす方法

**Yuang Wu** *2024年7月14日(日) 21:44:07 日本標準時* (1票)

Gemma2とGemma 7b-itを試しましたが、どちらの場合も提出ファイルのサイズが大きくなってしまいます。解決策はありますか？

---

# 他のユーザーからのコメント

> ## Jasper Butcher
> 
> どの圧縮アルゴリズムを使用していますか？提出ファイルのサイズは100GBまでですが、ほとんどの約80億パラメータのモデルは10〜15GB程度しか占有しません。
> 
> このコンペティションでは、ほとんどの人がpigz圧縮プログラムを使用しています。
> 
> ```
> !tar --use-compress-program='pigz --fast --recursive | pv' -cf submission.tar.gz -C /kaggle/input/path/to/weights . -C /kaggle/working/submission .
> 
> ```
> 
> 以下のように、submission/ディレクトリ内のすべてのファイルを複製することもできます。-9は最大圧縮レベルを示します。
> 
> ```
> !tar -cf - -C submission . | pigz -9 > submission.tar.gz 
> 
> ```
> 
> 
> 
> > ## Yuang Wuトピック作成者
> > 
> > えっ、私の上限は19.5GBなんですけど…
> > 
> > 
> > 
> > > ## Chris Deotte
> > > 
> > > Yuangさん、Kaggleノートブックの出力サイズの上限を指しているのかもしれません。ローカルに100GBのファイルを作成すれば、アップロードしてこのコンペティションに提出できます。ただし、Kaggleノートブックの出力フォルダの上限は20GBだと思います。
> > > 
> > > 
> > > 
--- 

