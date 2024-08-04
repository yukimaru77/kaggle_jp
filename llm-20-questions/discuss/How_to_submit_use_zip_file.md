# How to submit use zip file?

**sakura** *Thu Jun 06 2024 17:26:32 GMT+0900 (日本標準時)* (0 votes)

Hi, all. I want to submit my agent through a zip file. Here is my file structure:

```
├── lib
├── main.py
├── models

```

I uploaded through kaggle competitions submit -c llm-20-questions -f submission.zip -m "debug-file-upload". But the agent check failed and the log from agent-1 and 2 are both empty, and there is no replay. It seems that I somehow put the main.py in the wrong place?

I'm wondering how will this zip file be processed after uploading. Where will it be put and how will it be decompressed? Should I include a submission/ subdir for the zip file?



---

 # Comments from other users

> ## Chris Deotte
> 
> During submit, your zip will be uncompressed to folder "/kaggle_simulations/agent/", so you must add this to system path so that your code can find your models. Add the following code to the beginning of your main.py:
> 
> ```
> KAGGLE_AGENT_PATH = "/kaggle_simulations/agent/"
> if os.path.exists(KAGGLE_AGENT_PATH):
>     sys.path.insert(0, os.path.join(KAGGLE_AGENT_PATH, 'lib'))
> else:
>     sys.path.insert(0, "/kaggle/working/submission/lib")
> 
> ```
> 
> 
> 
> > ## sakuraTopic Author
> > 
> > Thanks for your reply! I know about this, and I indeed have code like this. Moreover, I can submit successfully with the Starter Notebook after I copy all of my main.py, paste it to the corresponding position in the Starter Notebook, and submit the notebook. But somehow when I'm uploading the zip file it doesn't work (and without error message).
> > 
> > 
> > 
> > > ## Chris Deotte
> > > 
> > > ok then maybe there is another error.
> > > 
> > > If your code fails the validation game (where your bot plays against your bot), there is a button to download logs. If you download logs, you will see the specific error message.
> > > 
> > > Also you can use print statements inside your main.py file and print debugging info. These print statements will show up in your logs.
> > > 
> > > 
> > > 


---

> ## Bovard Doerschuk-Tiberi
> 
> can you try tar.gz instead of zip?
> 
> 
> 


---

> ## sakuraTopic Author
> 
> Update: this my structure use unzip command:
> 
> ```
> unzip -l example.zip | awk -F/ 'NF<=3'
> 
> ```
> 
> 
> 


---

