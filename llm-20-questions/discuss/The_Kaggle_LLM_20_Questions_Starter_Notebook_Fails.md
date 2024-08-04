# The Kaggle "LLM 20 Questions Starter Notebook" Fails

**marketneutral** *Thu May 16 2024 08:03:39 GMT+0900 (日本標準時)* (5 votes)

All I did was clone the notebook; save it; and hit submit. And it fails… Any ideas why?

[fail.PNG](https://storage.googleapis.com/kaggle-forum-message-attachments/2815506/20702/fail.PNG)

---

 # Comments from other users

> ## Ryan Holbrook
> 
> Hi [@marketneutral](https://www.kaggle.com/marketneutral), You'll need to submit the output of the notebook instead of the notebook itself. Check out the first cell of the notebook for more details.
> 
> 
> 
> > ## marketneutralTopic Author
> > 
> > Ok. Got it. Thank you. I tried that. It still errors. The log file:
> > 
> > ```
> > [[{"duration": 0.077924, "stdout": "Initializing model\n", "stderr": "Traceback (most recent call last):\n  File \"/opt/conda/lib/python3.10/site-packages/kaggle_environments/agent.py\", line 159, in act\n    action = self.agent(*args)\n  File \"/opt/conda/lib/python3.10/site-packages/kaggle_environments/agent.py\", line 130, in callable_agent\n    agent(*args) \\\n  File \"/kaggle_simulations/agent/main.py\", line 245, in agent_fn\n    response = get_agent('answerer')(obs)\n  File \"/kaggle_simulations/agent/main.py\", line 229, in get_agent\n    agent = GemmaAnswererAgent(\n  File \"/kaggle_simulations/agent/main.py\", line 187, in __init__\n    super().__init__(*args, **kwargs)\n  File \"/kaggle_simulations/agent/main.py\", line 106, in __init__\n    model = GemmaForCausalLM(model_config)\n  File \"/kaggle_simulations/agent/lib/gemma/model.py\", line 400, in __init__\n    self.tokenizer = tokenizer.Tokenizer(config.tokenizer)\n  File \"/kaggle_simulations/agent/lib/gemma/tokenizer.py\", line 24, in __init__\n    assert os.path.isfile(model_path), model_path\nAssertionError: /kaggle_simulations/agent/gemma/py"}]]
> > 
> > ```
> > 
> > 
> > 
> > > ## marketneutralTopic Author
> > > 
> > > Has anyone been able to submit the Kaggle baseline agents?
> > > 
> > > 
> > > 


---

