# 要約 
ディスカッションでは、ユーザーRinku SahuがKaggle環境での'llm_20_question'コンペにおいて、kaggle_environmentsパッケージの古いバージョンしか表示されない問題に直面していることを報告しています。彼は新しいバージョンをインストールしたにもかかわらず、古いバージョンが表示され続け、パッケージをアンインストールして再インストールしても解決しないと述べています。

他のユーザー、特にJosef LeutgebとBovard Doerschuk-Tiberiは、バージョンの確認を促し、正しいバージョンをインストールする手順を提案しています。Josefは最新バージョン（>= 1.14.11）を確認し、必要な場合には特定のバージョンをインストールするようにアドバイスしていますが、Rinkuは試行しても問題が解決しないことを反映しています。

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

# I am not able to create a kaggle environments for 'llm_20_question'

**Rinku Sahu** *Sun Jun 02 2024 00:47:24 GMT+0900 (日本標準時)* (0 votes)





---

 # Comments from other users

> ## Josef Leutgeb
> 
> I had the same Issue. Check 
> 
> import kaggle_environments
> 
> kaggle_environments.__version__
> 
> If it is below 1.14.11 do 
> 
> pip install kaggle_environments==1.14.11
> 
> and restart the kernel.
> 
> 
> 
> > ## Rinku SahuTopic Author
> > 
> > I tried to install newer version and then did import but still it is showing older version of package.
> > 
> > 
> > 


---

> ## Bovard Doerschuk-Tiberi
> 
> What version of kaggle-environments are you using? Make sure it's the latest (>= 1.14.11)
> 
> 
> 
> > ## Rinku SahuTopic Author
> > 
> > I tried to install the '1.14.11' version but after importing and checking version, it is still showing the '1.14.11'.  following things I tried
> > 
> > Uninstall the package '',  but import kaggle_environments still works and gives 1.14.9 version. 
> > After uninstallation, again installed it but still showing older version 1.14.9.
> > After Installation, I tried to restart the kernal but still older version
> > 
> > 
> > 


---



</div>
<div class="column-right">

# 日本語訳

# 'llm_20_question'のKaggle環境が作成できません
**Rinku Sahu** *2024年6月2日 00:47:24 (日本標準時)* (0票)
---
## 他のユーザーからのコメント
> ## Josef Leutgeb
> 
> 私も同じ問題に直面しました。以下を確認してください。
> 
> ```python
> import kaggle_environments
> kaggle_environments.__version__
> ```
> 
> バージョンが1.14.11未満であれば、以下を実行してください。
> 
> ```bash
> pip install kaggle_environments==1.14.11
> ```
> 
> その後、カーネルを再起動してください。
> 
> 
> > ## Rinku Sahu トピック作成者
> > 
> > 新しいバージョンをインストールしてからインポートしましたが、まだ古いバージョンのパッケージが表示されます。
> > 
> > 
---
> ## Bovard Doerschuk-Tiberi
> 
> あなたの使用しているkaggle-environmentsのバージョンは何ですか？最新（>= 1.14.11）であることを確認してください。
> 
> > ## Rinku Sahu トピック作成者
> > 
> > '1.14.11'バージョンをインストールしようとしましたが、インポートしてバージョンを確認しても、まだ'1.14.11'が表示されています。以下のことを試しました。
> > 
> > パッケージをアンインストールしましたが、「import kaggle_environments」でまだ動作し、1.14.9が表示されます。アンインストール後、再度インストールしましたが、依然として古いバージョン1.14.9が表示されます。インストール後、カーネルを再起動しましたが、まだ古いバージョンが表示されます。
> > 
> > 
---


</div>