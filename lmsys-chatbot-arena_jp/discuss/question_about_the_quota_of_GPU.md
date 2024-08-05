# GPU クォータに関する質問

**Dlond Mike** *2024年7月29日 20:57:34 (日本標準時)* (1票)
提出はGPUクォータを消費しますか？もしそうなら、どのくらいのクォータを消費しますか？
---
# 他のユーザーからのコメント
> ## CPMP
> 
> ノートブックを保存すると、あなたのクォータを使って再び実行されます。これが完了すると、提出はあなたのクォータを消費しなくなります。
> 
> 
> 
---
> ## Yi-Fu Chen
> 
> ```
> import os
> if os.getenv('KAGGLE_IS_COMPETITION_RERUN'):
>     pass
> else:
>     raise SystemExit
> 
> ```
> 
> 上記のコードを提出されたノートブックの先頭に追加すると、試行実行ノートブックがすぐに閉じられ、スコア付けされた実行が保持されます。
> 
> 
> 
---
> ## Ravi Ramakrishnan
> 
> 私は通常、コードコンペティションにスクリプトで提出します。ダミーのLB提出時にGPUクォータを使い果たさないようにするために、以下を使用しています。
> 
> ```
> import pandas as pd
> sub_fl = pd.read_csv(.......submission.csv)
> 
> if len(sub_fl) <=10:
>     print(f"Submitting the dummy file")
>     sub_fl.to_csv("submission.csv", index = None)
> 
> else:
>     ....... (あなたのスクリプト)
> 
> ```
> 
> [@dlondmike](https://www.kaggle.com/dlondmike) 頑張ってください！
> 
> 
> 
---
> ## SeshuRaju 🧘‍♂️
> 
> [@dlondmike](https://www.kaggle.com/dlondmike) スコア付けはGPUクォータを消費しませんが、提出されたノートブックバージョンを生成するためには消費します（提出後でもノートブックをキャンセルできるので、GPUクォータを節約できます）。
> 
> 
> 
> > ## Valentin Werner
> > 
> > 私の知る限り（そして先週の経験から）、ノートブックを「保存」（提出ではありません）しても、クォータを超えてもクラッシュしません。先週は誤って32/30時間になったと思います 😃
> > 
> > 
> > 
---
> ## bao
> 
> 提出時には2つのノートブックが実行されます。スコア付けノートブックはGPUクォータを使用しませんが、もう1つは使用します。
> 
> 
> 
--- 
