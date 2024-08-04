# vllm issues

**padeof** *Sun Jul 28 2024 18:41:08 GMT+0900 (日本標準時)* (0 votes)

Anyone be able to run vllm directly by using the LLM class?

Tried to fix this "/kaggle_simulations/agent/srvlib/vllm/_C.cpython-310-x86_64-linux-gnu.so: undefined symbol" error for a week but no luck…

Running vllm as a server suffers from random start failures also.

Debugging a notebook submission is so hard 🤣



---

 # Comments from other users

> ## Chris Deotte
> 
> Here is a code example using vLLM on Kaggle. Even though vLLM is installed, we need to pip upgrade and change some files to make it work on Kaggle. [https://www.kaggle.com/code/cdeotte/infer-34b-with-vllm](https://www.kaggle.com/code/cdeotte/infer-34b-with-vllm)
> 
> 
> 
> > ## padeofTopic Author
> > 
> > Thank you! I have read your post.  However, this method does not work at submission time.  Looks like the torch module is loaded before any change made to sys path in agent script.  Thus the binary of vllm and torch do not match
> > 
> > 
> > 


---

