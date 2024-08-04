# Why is the scoring process so time-consuming

**David.Ricardo.H.X** *Thu May 30 2024 12:13:45 GMT+0900 (日本標準時)* (1 votes)


I submit successfully the code, the scoring is still running.
The submitted notebook throws error, the scoring is still running. 

Does anybody have the same issue? 



---

 # Comments from other users

> ## Valentin Werner
> 
> Note that time difference between Submission and save come from the data difference. During saving (the success / error you mentioned) the test data only has 3 rows, during submission its 25,000 rows. A subset of these rows are used for Public Leaderboard (what we see on Leaderboard right now), while most IS used for private Leaderboard / the score we see once the competition finished, and which is used for actual evaluation in the competition placement.
> 
> So you are running A LOT more data during submission, increasing runtime for row based operations
> 
> 
> 
> > ## Nguyễn Anh Tú
> > 
> > Does the data in file train.csv in submission environment different from the data in that file when we training model with our private notebook sir? 
> > 
> > 
> > 


---

> ## [Deleted User]
> 
> The scoring process can be time-consuming due to several factors:
> 
> Complexity of Notebook: Long-running computations or large datasets extend execution time.
> Resource Constraints: Limited computational resources and high submission volumes cause delays.
> Error Handling: Systems may attempt to run all cells despite errors to gather complete data.
> Automated Evaluation: Comprehensive testing and validation can take a significant amount of time.
> System Overhead: Infrastructure tasks such as container setup and data transfer add to the delay
> 
> 


---

