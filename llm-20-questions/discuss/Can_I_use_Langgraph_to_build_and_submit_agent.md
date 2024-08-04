# Can I use Langgraph to build and submit agent

**Bikash Patra** *Mon Jun 10 2024 16:45:18 GMT+0900 (日本標準時)* (0 votes)

Dear Community,

  Can anyone , please tell me if we can use langgraph / langchain to create the agents? Or does it need to have pure python implementation without any other libraries / frameworks?



---

 # Comments from other users

> ## VolodymyrBilyachat
> 
> My understanding is you can use what ever you want as soon you are within
> 
> Timeouts, Limits and Penalties.
> 
> Questions are limited to 2000 characters
> 
> Guesses are limited to 100 characters
> 
> Timeouts
> 
> Agents are given 60 seconds per round to answer
> 
> Agents have an additional 300 overage seconds to use throughout the game
> 
> Any agent timing out will cause the game to end
> 
> Any answering agent responding with anything other than yes or no will result in the game ending and them losing the match.
> 
> Technical Specifications
> 
> 100 GB of disk space
> 
> 16 GB of RAM
> 
> 1 T4 GPU
> 
> 
> 


---

