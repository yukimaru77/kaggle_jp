# 要約 
このディスカッションは、Kaggleの「LLM 20 Questions」コンペティションにおけるエージェントのキャンセル方法についてです。

ユーザーのfrancesco fiamingoは、様々な設定でエージェントを試しており、良いエージェントはそのままにしておきたい一方で、悪いエージェントは入れ替えたいと考えています。しかし、エージェントの入れ替えは提出日時と関連しているため、以前提出したエージェントを維持しながら特定のエージェントをキャンセルする方法がわかりません。

Chris Deotteは、アクティブなエージェント3つは選択できず、最も最近提出された3つが自動的に選択されると説明します。つまり、現在のエージェントを置き換えるには、新しいエージェントを提出する必要があるということです。

francesco fiamingoは、このロジックが理解できないとコメントし、Chris Deotteも同様の意見を表明します。Chris Deotteは、Kaggleがボットのオンオフを切り替えられるようにしたくない可能性があると推測し、その理由として、ボットのスコア操作を防ぐためだと説明します。

このディスカッションは、コンペティションにおけるエージェントの管理方法に関する疑問と、その理由についての推測で締めくくられています。


---
# エージェントのキャンセル方法について

**francesco fiamingo** *2024年7月27日(土) 03:55:41 JST* (3 votes)

皆さん、こんにちは。

様々な設定で様々なエージェントを試しているのですが、良いエージェントはそのままにしておきたい一方で、悪いエージェントは入れ替えたいと思っています。しかし、入れ替えは（同時に最大3つ、1日に最大5つ）エージェントの提出日時と関連しているようで、以前提出したエージェントを「生きて」維持しながら、特定のエージェントをキャンセルする方法がわかりません。良い方法があれば教えてください！勝利を目指して頑張りましょう！

---
# 他のユーザーからのコメント

> ## Chris Deotte
> 
> アクティブなエージェント3つは選択できません。最も最近提出された3つが自動的に選択されます。（つまり、現在のエージェントを置き換えるには、新しいエージェントを提出する必要があります）。
> 
> 
> 
> > ## francesco fiamingoトピック作成者
> > 
> > ありがとうございます。しかし、少なくともテスト段階ではそのロジックが理解できません。
> > 
> > 
> > 
> > > ## Chris Deotte
> > > 
> > > 僕もそのロジックが理解できません。
> > > 
> > > 恐らくKaggleは、ボットのオンオフを切り替えられるようにしたくないのでしょう。例えば、ボットがハイスコアを達成したら、スコアが下がるのを防ぐためにボットを無効化できます。そして、コンペティションの最後の1時間でボットを有効化して、パブリックLBで1位を獲得できます。
> > > 
> > > パブリックLBでの最終順位は、プライベートLBへのシードになると思うので、上記のようなことが有利になるかもしれません。好きな時にボットのオンオフを切り替えることで、LBを操作できる方法は他にもあるでしょう。
> > > 
> > > 
> > > 
---
