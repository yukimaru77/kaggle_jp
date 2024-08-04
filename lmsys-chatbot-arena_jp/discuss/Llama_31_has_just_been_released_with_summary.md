# 要約 
このディスカッションは、Metaがリリースした新しい言語モデルLlama 3.1に関するものです。

投稿者は、Llama 3.1の8Bバージョンの重みがMetaのウェブサイトとHugging Faceで公開されていることを発表しました。また、開発プロセスを説明する技術記事へのリンクも共有しています。

コメント欄では、ユーザーはLlama 3.1の性能について議論しています。一部のユーザーは、Llama 3.1が以前のバージョンよりも優れていると報告していますが、他のユーザーは、Llama 3.1が以前のバージョンよりも優れているとは感じられないと報告しています。

また、ユーザーはLlama 3.1をKaggleでオフラインで使用する方法や、Llama 3.1をトレーニングする方法について議論しています。

全体として、このディスカッションは、Llama 3.1のリリースに対するコミュニティの興奮と、新しい言語モデルの性能に対する期待の高さを示しています。


---
# Llama 3.1 がリリースされました

**lightsource<3** *2024年7月24日 水曜日 00:08:21 GMT+0900 (日本標準時)* (21票)

8B バージョンの重みは [https://llama.meta.com](https://llama.meta.com) にあります。
HF: [https://huggingface.co/collections/meta-llama/llama-31-669fc079a0c406a149a5738f](https://huggingface.co/collections/meta-llama/llama-31-669fc079a0c406a149a5738f)
開発プロセスを説明する技術記事へのリンク: 
[https://scontent.fdxb2-1.fna.fbcdn.net/v/t39.2365-6/452256780_3788187148167392_9020150332553839453_n.pdf?_nc_cat=103&ccb=1-7&_nc_sid=3c67a6&_nc_ohc=XG3_BvYG0wwQ7kNvgEI9-4V&_nc_ht=scontent.fdxb2-1.fna&oh=00_AYAmG3EQLSTDlGlgdUqlvT6Z0uNBXoQcm_bCMhlFzDJ96A&oe=66A5A0DC](url)
---
 # 他のユーザーからのコメント
> ## Nicholas Broad
> 
> Kaggle でオフラインで使用したい場合は、新しい transformers が必要で、私の [Hugging Face ライブラリ用のオフラインデータセット](https://www.kaggle.com/datasets/nbroad/hf-libraries) に既に含まれています。
> 
> ```
> !pip install --no-deps --no-index /kaggle/input/hf-libraries/transformers/transformers-4.43.1-py3-none-any.whl
> 
> ```
> 
> 
> 
> > ## SAY WHAT
> > 
> > ありがとうございます。
> > 
> > torch のバージョンは何ですか？
> > 
> > 
> > 
> > > ## Nicholas Broad
> > > 
> > > ノートブックではデフォルトを使用できます。
> > > 
> > > 
> > > 
> > ## YingxiZhang
> > 
> > 思い出させてくれてありがとう。
> > 
> > 
> > 
---
> ## Valentin Werner
> 
> 
> 
> 止まれない、止まらない。
> 
> 
> 
> > ## Valentin Werner
> > 
> > 天に感謝。Mistral-Large 2 はクローズドソースだ。
> > 
> > 
> > 
---
> ## aadiAR
> 
> 教えてくれてありがとう！
> 
> 
> 
---
> ## Kishan Vavdara
> 
> 
> 
> 
> 
---
> ## Taimo
> 
> unsloth が 4bit 8B モデルをアップロードしました！
> 
> ベースモデル:
> 
> [https://huggingface.co/unsloth/Meta-Llama-3.1-8B-bnb-4bit](https://huggingface.co/unsloth/Meta-Llama-3.1-8B-bnb-4bit)
> 
> インストラクトモデル:
> 
> [https://huggingface.co/unsloth/Meta-Llama-3.1-8B-Instruct](https://huggingface.co/unsloth/Meta-Llama-3.1-8B-Instruct)
> 
> 
> 
> > ## Rishit Jakharia
> > 
> > 情報をありがとう！
> > 
> > 
> > 
---
> ## Weiren
> 
> 現在トレーニング中です。数ステップの損失プロットを見ると、Gemma-2 を凌駕しているようには見えません…。多分私のハイパーパラメータが良くないだけでしょう。🤡
> 
> 
> 
> > ## Rishit Jakharia
> > 
> > Llama 3.1 をチューニングする予定があれば、お知らせください。また、もし差し支えなければ、どのような量子化と設定を使用しているか教えてください。
> > 
> > 
> > 
> > ## Ivan Vybornov
> > 
> > 今までに 3 回トレーニングを試みましたが、Llama 3 を凌駕しているようには見えません。少なくとも、大きな差で優れているわけではありません。
> > 
> > 
> > 
> > > ## justin1357
> > > 
> > > 同じです。Llama 3 よりも劣っています。
> > > 
> > > 
> > > 
---
> ## Robert0921
> 
> トレーニングとテスト中です。
> 
> 
> 
---
> ## Muhammad Anas
> 
> 素晴らしいですね。
> 
> 
> 
---
> ## SAY WHAT
> 
> ロードに問題があるようです。
> 
> とにかく、弾丸を撃ちまくりましょう。
> 
> 
> 
---

