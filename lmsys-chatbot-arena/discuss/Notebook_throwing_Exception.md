# Notebook throwing Exception

**Varun Jagannath** *Wed Jul 10 2024 23:45:51 GMT+0900 (日本標準時)* (0 votes)

After submitting the notebook. And, after some grueling hours it throws exception and there is no way to find out about it. Is there any other way to check.



---

 # Comments from other users

> ## Valentin Werner
> 
> This is just one potential issue, but how are you handling the "null" that sometimes occur? Doing this helped for me in the early submissions: response.replace("null","'null'") <-- note the extra ' to make it a string before loading the string representation of the list an actual list (e.g., with ast.literal_eval(response))
> 
> I really hope this is doing it for you - because these exceptions can be nasty. If not, maybe try debugging by predicting on training data again.
> 
> If the GPU goes OOM its not an OOM error on kaggle but an Exception, so maybe reduce batch size or max length too. Best of luck!
> 
> 
> 
> > ## Varun JagannathTopic Author
> > 
> > Looks like its an issue with batch size
> > 
> > 
> > 


---

> ## Robert Turro
> 
> Try clicking on the notebook then going to the Logs section.
> 
> 
> 


---

