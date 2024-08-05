# Traing steps cannot match the sample size!

**godmysalary** *Fri Jul 05 2024 12:49:34 GMT+0900 (日本標準時)* (1 votes)

Hello everyone! We were using the vscode to run the amazing fine-tune work by [https://www.kaggle.com/code/hotchpotch/train-llm-detect-ai-comp-mistral-7b/notebook](url)

The only difference is that we change the model to Llama3. 

And when I run the code on Kaagle GPU, everything is fine. The sample size is 500, gradient_accumulate_steps is 16, batch_size=1, so we will undergo 31 steps, which is shown by the first picture below. 

However when I just COPY the same code to my vscode which is connected to a remote server, the total steps became 10! The sample size, gradient_accumulate_steps, batch_size stay unchanged but the total steps became 10, which is shown in the second picture and means only about 160 (16*10) samples are processed? Only one GPU is used on the vscode. 

Could anybody give me a hint about what is going on? The packages are updated. 



---

 # Comments from other users

> ## godmysalaryTopic Author
> 
> Hello everybody! We checked this probelm again and finally found the "killer"! Our remote server has 3 GPUs and so as you may suspect, the program is parallelled. The most annoying part is that when we loaded the model, we set device_map={'': 0} but somehow it still ran parallelly. So we explicitly set CUDA_VISIBLE_DEVICES = 0 at the beginning of our code and the problem faded! Hope this help you for your fine-tuning.
> 
> 
> 


---

> ## Valentin Werner
> 
> Did you check the length of your data? Did you accidentally swap train and validation dataset?
> 
> 
> 
> > ## godmysalaryTopic Author
> > 
> > yes! the length of train_dataset is 500 and the length of evaluation_dataset is 100.
> > 
> > 
> > 


---
