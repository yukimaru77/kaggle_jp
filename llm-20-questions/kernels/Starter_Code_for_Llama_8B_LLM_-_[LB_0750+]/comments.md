# Comments 

> ## shiv_314
> 
> This notebook is awesome! How did you come up with the fact that you can use a model with 8B parameters as an upper limit? Can you walk me through the guesstimate?
> 
> 
> 
> > ## Chris DeotteTopic Author
> > 
> > Using 1xT4 GPU, we can actually infer 17B model (because I show how to infer 34B model with 2xT4 [here](https://www.kaggle.com/code/cdeotte/infer-34b-with-vllm)). When we begin with an 17B model, after 4bit quantization it becomes 10GB on disk which fits easily into 1xT4's 16GB VRAM. (UPDATE: and maybe we can infer 20B model)
> > 
> > 
> > 


---

> ## Istvan Habram
> 
> Where is it specified that the agent needs to implement a fuction called def agent_fn(obs, cfg)?
> 
> 
> 
> > ## Chris DeotteTopic Author
> > 
> > We learn this from Kaggle admin's starter notebook [here](https://www.kaggle.com/code/ryanholbrook/llm-20-questions-starter-notebook) or by reading Kaggle's GitHub [here](https://github.com/Kaggle/kaggle-environments/tree/master/kaggle_environments/envs/llm_20_questions) which shows the code that runs our agents.
> > 
> > 
> > 
> > > ## Istvan Habram
> > > 
> > > It is clear now, thank you for your quick response!
> > > 
> > > 
> > > 


---

> ## Toshi
> 
> great notebook!
> 
> when I run this, I found the above error
> 
> ImportError: numpy>=1.17,<2.0 is required for a normal functioning of this module, but found numpy==2.0.0.
> 
> Try: pip install transformers -U or pip install -e '.[dev]' if you're working with git main
> 
> Did you find this when you run??
> 
> 
> 
> > ## Chris DeotteTopic Author
> > 
> > No. I have never seen that error. Are you running this notebook as is? Or changing something? Do you set the notebook option environment to "pin to original"? Or are you using Kaggle's latest docker. We should use "pin to original" if Kaggle's latest is causing errors.
> > 
> > If you have changed something which is causing not liking numpy==2.0.0, you can try pip installing an older numpy like pip install numpy==1.17
> > 
> > 
> > 
> > > ## FullEmpty
> > > 
> > > [@cdeotte](https://www.kaggle.com/cdeotte) Thank you for your notebook - I always learn a lot from your posts and comments. I haven't master Kaggle notebooks, but this notebook works when copied and run, but it doesn't with the above error when downloaded, imported back and run, even on the Pin to Original Environment. 
> > > 
> > > But the issue can be solved with either:
> > > 
> > > !rm -rf /tmp/submission/lib/numpy-2.0.1.dist-info
> > > 
> > > or, preferably,
> > > 
> > > os.system("pip install accelerate==0.33.0 bitsandbytes==0.43.2 huggingface_hub==0.24.2 -t /tmp/submission/lib")
> > > 
> > > 
> > > 


---

> ## Kartikeya Pandey
> 
> Great notebook I have learned alot from this
> 
> 
> 


---

> ## El haddad Mohamed
> 
> Great notebook! Very well-structured and informative. 👍
> 
> 
> 


---

> ## ISAKA Tsuyoshi
> 
> Hi [@cdeotte](https://www.kaggle.com/cdeotte) . Thank you for sharing such an excellent notebook!
> 
> Can you tell me more about the model (Llama-3-Smaug-8B) used in this notebook? Is it superior to the llama-3 model?
> 
> 
> 
> > ## Chris DeotteTopic Author
> > 
> > Llama-3-Smaug-8B is the model Llama-3-8B-Instruct with additional finetuning. It does better than Llama-3-8B-Instruct in some ways and probably does worse in some ways. There is a research paper describing how Smaug was trained [here](https://arxiv.org/abs/2402.13228). I discovered this model because at some point in time this model was higher on the Open LLM Leaderboard than plain Llama.
> > 
> > Another interesting model which was doing well on Open LLM Leaderboard at one time is jondurbin/bagel-7b-v0.5 [here](https://huggingface.co/jondurbin/bagel-7b-v0.5). This is Mistral-7B with additional finetuning. There is a GitHub describing how Bagel is trained [here](https://github.com/jondurbin/bagel)
> > 
> > And another model which does well on Open LLM Leaderboard is Qwen/Qwen2-7B-Instruct [here](https://huggingface.co/Qwen/Qwen2-7B-Instruct). I'm a big fan of the Qwen2 models. This v2 series just got released a month ago (previously it was v1.5 series) and quickly became the top Open LLM Leaderboard model.
> > 
> > (For completeness, I'll mention that the classic models are Llama3, Mistral, Gemma2, and Phi3)
> > 
> > 
> > 
> > > ## ISAKA Tsuyoshi
> > > 
> > > Thank you for the detailed explanation! There are so many options available.
> > > 
> > > 
> > > 


---

