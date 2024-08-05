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
