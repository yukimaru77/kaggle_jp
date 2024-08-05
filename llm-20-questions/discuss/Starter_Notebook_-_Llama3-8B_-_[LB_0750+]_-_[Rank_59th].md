# Starter Notebook - Llama3-8B - [LB 0.750+] - [Rank 59th]

**Chris Deotte** *Tue Jul 16 2024 09:54:06 GMT+0900 (日本標準時)* (59 votes)

Hi everyone! I'm sharing my current submission which is currently achieving public LB 0.750+ and public LB rank 59th! (And before keyword update, this notebook was achieving 1st place public LB 🥇 😀 ). The notebook is [here](https://www.kaggle.com/code/cdeotte/starter-code-for-llama-8b-llm-lb-0-750). Enjoy!

## Good Stuff

This notebook has some problems (i.e. it uses some fixed keywords), but it also has a lot of helpful code to demonstrate stuff. The helpful things this notebook demonstrates are as follows:

- A strategy how to ask questions to narrow down search (and use a CSV of features behind the scenes).

- How to install pip libraries to be used during submission

- How to download and use any LLM model from Hugging Face

- How to perform EDA on your LLM's answering ability

- How to create agent code and create tarball for submission

- How to run Kaggle's API to watch your agent locally

## Bad Stuff

Some problems with this notebook are:

- uses (an old list of) fixed keywords which may change during private LB. (And have changed on public LB.)

- only asks questions about places (i.e. (1) which sub-category? (city, country, landmark), (2) which continent?, (3) which first letter? It does not ask questions about things) 

## How To Improve

Note that even if private LB keywords change, we can use this notebook's template and strategy to create a notebook which selects thousands or millions of words from Wikipedia and uses that list as a list of all potential keywords. 

Then we create new columns in that dataframe with additional features describing all the words and we create pre-determined questions asking if keyword has these additional featuers. Finally we make guesses based on the keywords in our created dataframe (with additonal column features) and the answerer's responses about features.

# Starter Code

The starter code is [here](https://www.kaggle.com/code/cdeotte/starter-code-for-llama-8b-llm-lb-0-750).



---

 # Comments from other users

> ## mxmm2123
> 
> great job!!!
> 
> 
> 


---

> ## Rishit Jakharia
> 
> Hey!, Thanks for sharing the notebook,
> 
> I noticed you used fp4 quantization in your implementation for the llama 3 model..
> 
> Wanted to ask whether you tried GGUF quantization, if yes what were the results compared to the current implementation
> 
> 
> 
> > ## Chris DeotteTopic Author
> > 
> > Hi. I have not tried GGUF quantization. In another project (i.e. not Kaggle's 20 question comp), I have tried AWQ quantization with Hugging Face's AutoModelForCausalLM and it was very slow compared with fp4. So when we evaluate GGUF, we must also consider its speed to.
> > 
> > 
> > 
> > > ## Rishit Jakharia
> > > 
> > > Okay, thanks !
> > > 
> > > 
> > > 


---

> ## Valentin Baltazar
> 
> This is great for beginners like me! Thank you.
> 
> 
> 


---

> ## torino
> 
> [@cdeotte](https://www.kaggle.com/cdeotte) Thank you for sharing the notebook. I was see you installed python package offline, but in my notebook I can't install new pytorch for the submit environment(It worked well on the normal notebook). Do you have any suggestion? You can see my issue [here](https://www.kaggle.com/competitions/llm-20-questions/discussion/520207)
> 
> 
> 


---

