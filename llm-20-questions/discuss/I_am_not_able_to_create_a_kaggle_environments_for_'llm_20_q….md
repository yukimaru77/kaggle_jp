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

