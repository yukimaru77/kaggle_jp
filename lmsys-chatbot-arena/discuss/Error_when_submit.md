# Error when submit

**Nguyễn Anh Tú** *Mon Jul 15 2024 16:23:48 GMT+0900 (日本標準時)* (0 votes)

I got the error "Submission Scoring Error" when I submitted  my notebook, I thought that I set the wrong format for my submission.csv. Then, I read the sample_submission.csv and change the the value of ['winner_model_a', 'winner_model_b', 'winner_tie'] columns with my y_predict. The worst thing is my notebook ran successful but when I submitted again I got the error "Notebook Threw Exception", please help me!



---

 # Comments from other users

> ## Valentin Werner
> 
> ### Submission scoring error -> make sure that you include id
> 
> An example way to get a working submission:
> 
> ```
> # Submit
> sub = pd.DataFrame(sm, index = test.id, columns = ["winner_model_a","winner_model_b","winner_tie"]).reset_index()
> sub.to_csv('submission.csv', index=False)
> sub.head()
> 
> ```
> 
> where sm is an array like np.array([0.123,0.567,0.234],…,[0.999,0.000,0.001])
> 
> ### Notebook threw exception
> 
> You managed to make a working notebook not work anymore 😀 This could have some reasons: GPU goes OOM (this does not trigger an OOM Error); There are some "null" responses in the responses which need to be handled (e.g., replace null with 'null' before loading the string representation of the list as real list); There is actually an error raised during runtime.
> 
> What you can do to evaluate the errors is try to run your inference code on the half the train set (which is basically the size of test) and see what happens.
> 
> 
> 
> > ## Nguyễn Anh TúTopic Author
> > 
> > It's very helpful for me. Thanks a lot.
> > 
> > 
> > 


---

