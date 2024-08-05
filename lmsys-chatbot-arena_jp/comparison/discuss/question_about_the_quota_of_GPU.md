# 要約 
このディスカッションは、KaggleコンペティションにおけるGPUクォータの消費について議論しています。

**質問:** ユーザーdlondmikeは、提出がGPUクォータを消費するかどうか、そして消費する場合はどのくらい消費するのかを尋ねています。

**回答:** 複数のユーザーが回答しており、要約すると以下のようになります。

* 提出は、ノートブックを保存して実行する際にGPUクォータを消費します。
* スコア付けされた実行はGPUクォータを消費しませんが、提出されたノートブックバージョンを生成するためには消費します。
* 提出時に2つのノートブックが実行されます。スコア付けノートブックはGPUクォータを使用しませんが、もう1つは使用します。
* ノートブックを保存しても、クォータを超えてもクラッシュしません。

**追加情報:**

* ユーザーYi-Fu Chenは、提出されたノートブックの先頭にコードを追加することで、試行実行ノートブックをすぐに閉じ、スコア付けされた実行を保持する方法を提案しています。
* ユーザーRavi Ramakrishnanは、スクリプトで提出する場合、ダミーのLB提出時にGPUクォータを使い果たさないようにするためのコードを提供しています。

**結論:** 提出はGPUクォータを消費しますが、スコア付けされた実行は消費しません。ユーザーは、GPUクォータを節約するために、ノートブックをキャンセルしたり、コードを最適化したりすることができます。


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

# question about the quota of GPU

**Dlond Mike** *Mon Jul 29 2024 20:57:34 GMT+0900 (日本標準時)* (1 votes)

Does submission take the quota of GPU?if so,how much quota it will take?



---

 # Comments from other users

> ## CPMP
> 
> saving your notebook runs it again using your quota. Once this is done, submitting does not use your quota anymore.
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
> Adding the above code at the front of the submitted notebook will quickly close the trial run notebook and retain the scored run.
> 
> 
> 


---

> ## Ravi Ramakrishnan
> 
> I usually submit to code competitions in a script. I use the below to ensure I don't use up my GPU quotas during my dummy LB submission- 
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
>     ....... (your script)
> 
> ```
> 
> [@dlondmike](https://www.kaggle.com/dlondmike) best of luck!
> 
> 
> 


---

> ## SeshuRaju 🧘‍♂️
> 
> [@dlondmike](https://www.kaggle.com/dlondmike) for scorning won't take GPU quota, but for generating the submitted notebook version ( even after submit, you can cancel the notebook, so GPU quota can be saved )
> 
> 
> 
> > ## Valentin Werner
> > 
> > From what I know (and experienes last week), the "save" notebook (not submit) also doesnt crash if it goes above quota. I think I ended last week on 32/30 hrs by accident 😃
> > 
> > 
> > 


---

> ## bao
> 
> There are two notebooks running when submitted. The scoring notebook does not use GPU quota, while the other one does.
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

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



</div>