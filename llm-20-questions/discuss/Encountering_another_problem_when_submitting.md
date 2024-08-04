# Encountering another problem when submitting

**Yuang Wu** *Wed Jul 17 2024 16:15:50 GMT+0900 (日本標準時)* (1 votes)

My model using now is Gemma 2 9b it. During Validation process, the agent 0 log shows like this, and there is no content in agent 1 log.

[[{"duration": 1.089666, "stdout": "", "stderr": "Traceback (most recent call last):\n  File \"/opt/conda/lib/python3.10/site-packages/transformers/models/auto/configuration_auto.py\", line 951, in from_pretrained\n    config_class = CONFIG_MAPPING[config_dict[\"model_type\"]]\n  File \"/opt/conda/lib/python3.10/site-packages/transformers/models/auto/configuration_auto.py\", line 653, in __getitem__\n    raise KeyError(key)\nKeyError: 'gemma2'\n\nDuring handling of the above exception, another exception occurred:\n\nTraceback (most recent call last):\n  File \"/opt/conda/lib/python3.10/site-packages/kaggle_environments/agent.py\", line 50, in get_last_callable\n    exec(code_object, env)\n  File \"/kaggle_simulations/agent/main.py\", line 69, in <module>\n    config = AutoConfig.from_pretrained(model_id)\n  File \"/opt/conda/lib/python3.10/site-packages/transformers/models/auto/configuration_auto.py\", line 953, in from_pretrained\n    raise ValueError(\nValueError: The checkpoint you are trying to load has model typegemma2but Transformers does not recognize this architecture. This"}]]

Has anyone met this problem?



---

 # Comments from other users

> ## gwh666
> 
> It seems that AutoConfig can not match Gemma-2 in transformers right now,you can only use AutoModelForCasualLM to load it.
> 
> 
> 
> > ## Yuang WuTopic Author
> > 
> > Wow, good advice, I will try it. Thanks gwh
> > 
> > 
> > 
> > ## Yuang WuTopic Author
> > 
> > Seems like AutoModelForCausalLM will also use AutoConfig… Now I have no idea
> > 
> > 
> > 
> > > ## gwh666
> > > 
> > > model = AutoModelForCausalLM.from_pretrained(
> > > 
> > >     "google/gemma-2-9b-it",
> > > 
> > >     device_map="auto",
> > > 
> > >     torch_dtype=torch.bfloat16
> > > 
> > > )
> > > 
> > > try it?
> > > 
> > > 
> > > 


---

> ## Chris Deotte
> 
> You will need to pip install a more recent version of Transformers that includes code for Gemma2
> 
> 
> 
> > ## Yuang WuTopic Author
> > 
> > Yeah, I saw the advice in Huggingface, but I have already run "pip install -U transfromers", but still useless
> > 
> > 
> > 


---

