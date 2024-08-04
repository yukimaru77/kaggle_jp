# Maximum context length error

**Kha Vo** *Sun Jun 02 2024 21:42:00 GMT+0900 (日本標準時)* (1 votes)

I have this strange error, sometimes it occurred in the 8th question, sometimes the 19th. 

I use a forked version of Rigging model from public(Rob Mulla)

Anybody has the similar ones?

[[{"duration": 82.005355, "stdout": "vLLM Started\n\n", "stderr": ""}],

 [{"duration": 1.975345, "stdout": "", "stderr": ""}],

 [{"duration": 3.674225, "stdout": "", "stderr": ""}],

 [{"duration": 2.703787, "stdout": "", "stderr": ""}],

 [{"duration": 3.001207, "stdout": "", "stderr": ""}],

 [{"duration": 4.30606, "stdout": "", "stderr": ""}],

 [{"duration": 1.13816, "stdout": "", "stderr": ""}],

 [{"duration": 3.413029, "stdout": "", "stderr": ""}],

 [{"duration": 1.112546, "stdout": "", "stderr": ""}],

 [{"duration": 4.805608, "stdout": "", "stderr": ""}],

 [{"duration": 3.679116, "stdout": "", "stderr": ""}],

 [{"duration": 3.024704, "stdout": "", "stderr": ""}],

 [{"duration": 1.29648, "stdout": "", "stderr": ""}],

 [{"duration": 5.255335, "stdout": "", "stderr": ""}],

 [{"duration": 2.962781, "stdout": "", "stderr": ""}],

 [{"duration": 375.321071, "stdout": "\n\u001b[1;31mGive Feedback / Get Help: [https://github.com/BerriAI/litellm/issues/new\u001b[0m\nLiteLLM.Info:](https://github.com/BerriAI/litellm/issues/new\u001b[0m\nLiteLLM.Info:) If you need to debug this error, use `litellm.set_verbose=True'.\n\n", "stderr": "OpenAIException - Error code: 400 - {'object': 'error', 'message': \"This model's maximum context length is 8192 tokens. However, you requested 8231 tokens in the messages, Please reduce the length of the messages.\", 'type': 'BadRequestError', 'param': None, 'code': 400}\nTraceback (most recent call last):\n  File \"/kaggle_simulations/agent/lib/litellm/llms/openai.py\", line 414, in completion\n    raise e\n  File \"/kaggle_simulations/agent/lib/litellm/llms/openai.py\", line 373, in completion\n    response = openai_client.chat.completions.create(*data, timeout=timeout)  # type: ignore\n  File \"/kaggle_simulations/agent/lib/openai/_utils/_utils.py\", line 277, in wrapper\n    return func(args, **kwargs)\n  File \"/kaggle_simulations/agent/lib/openai/resources/chat/completions.py\", line 590, in create\n    return self._post(\n  File \"/kaggle_simulations/agent/lib/openai/_base_client.py\", line 1240, in post\n    return cast(ResponseT, self.request(cast_to, opts, stream=stream, stream_cls=stream_cls))\n  File \"/kaggle_simulati"}]]



---

 # Comments from other users

> ## Rob Mulla
> 
> Hey [@khahuras](https://www.kaggle.com/khahuras) - I just noticed this post. Glad to hear you are using our rigging baseline! Did you ever figure out the root cause of this issue?
> 
> 
> 


---

> ## waechter
> 
> Questions are limited to 2000 characters, and some team use all of it with is the keyword in the list ... type of questions. So if your template contains all the questions asked previously, you run out of tokens when playing with them. (Just a guess)
> 
> 
> 
> > ## Kha VoTopic Author
> > 
> > I don’t allow my bot to have that kind of question though…
> > 
> > 
> > 
> > > ## waechter
> > > 
> > > What role (guesser or answerer) does your agent play when the error occurs?
> > > 
> > > I assumed answerer in my previous comment
> > > 
> > > 
> > > 


---
