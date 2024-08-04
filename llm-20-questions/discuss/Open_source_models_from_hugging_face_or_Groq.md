# Open source models from hugging face or Groq

**G R Shanker Sai** *Mon Jul 15 2024 19:40:58 GMT+0900 (日本標準時)* (0 votes)

Hi ,

Is it possible to use models hosted in hugging face / groq, via an api call, as i am facing lot of issues to create a langchain based agent wrapper for the local llm?



---

 # Comments from other users

> ## Matthew S Farmer
> 
> The evaluation environment does not access the internet. Model weights must be loaded into submission. Therefore, an API call that relies on an internet connection would not work. Models on HF can be used, but you need to either download the snapshot and upload or use the save pretrained function within the transformers library. Since groq would rely on an internet connection, it would not work. 
> 
> 
> 


---

