# submission scoreing error

**Xin** *Fri Aug 02 2024 04:32:13 GMT+0900 (日本標準時)* (0 votes)

Has anyone meet this problem when using gemma?  I just changed the inputs.

Thanks!!!



---

 # Comments from other users

> ## Enter your display name
> 
> This could be caused by many reasons, but the most common one is likely that the number of rows in your output submission.csv file does not match test.csv after rerunning on all hidden test data.
> 
> 
> 
> > ## XinTopic Author
> > 
> > Thanks!
> > 
> > By using:
> > 
> > ```
> > !python /kaggle/usr/lib/lmsys_script/lmsys_script.py
> > import pandas as pd
> > lmsys_with_metadata = pd.read_csv("/kaggle/working/lmsys_with_metadata.csv")
> > !rm /kaggle/working/lmsys_with_metadata.csv
> > test_df = pd.read_csv("/kaggle/input/lmsys-chatbot-arena/test.csv")
> > if len(test_df) != len(lmsys_with_metadata):
> >     1/0
> > 
> > ```
> > 
> > I got Notebook Throw Exception which proves you must right.
> > 
> > Why lmsys_script.py (as a utility script) will output different length after submitting submission.csv.
> > 
> > Inside the lmsys_script.py:
> > 
> > df = pd.read_csv("/kaggle/input/lmsys-chatbot-arena/test.csv")
> > 
> > 
> > 
> > > ## XinTopic Author
> > > 
> > > lmsys_script.py (as a utility script) will output same length using train.csv and test.csv before submitting submission.csv.
> > > 
> > > 
> > > 
> > > ## XinTopic Author
> > > 
> > > Finally I abandoned using utility script way to release GPU then the problem solved.
> > > 
> > > 
> > > 


---

