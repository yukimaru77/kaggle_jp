# kaggle docker

**A. John Callegari Jr.** *Wed Jun 19 2024 01:07:43 GMT+0900 (日本標準時)* (0 votes)

I'm trying to pull the latest kaggle docker image using "docker pull gcr.io/kaggle-gpu-images/python:latest" but permission is denied.  How can I obtain access to the up-to-date kaggle dockers on Google Container Registry?  

thanks,

John



---

 # Comments from other users

> ## Melinda
> 
> Did you already try doing gcloud auth configure-docker gcr.io first?
> 
> 
> 
> > ## A. John Callegari Jr.Topic Author
> > 
> > Yes, I had executed that command and the other google-cloud-cli formulas listed on the GCR website but I still ran into permission denied.  I did get the pull command to work after following the link to upgrade my Kaggle notebook to a google notebook and in the process creating a pay tier gcloud account (without spending any money on Google).  Google may require you to associate your gcloud account with a payment method (apart from your general gsuite payment method) in order for your account login to pass cli authentication to work for the docker pull
> > 
> > 
> > 


---
