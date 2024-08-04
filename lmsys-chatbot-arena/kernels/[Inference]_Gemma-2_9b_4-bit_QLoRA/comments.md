# Comments 

> ## Cody_Null
> 
> Do you have any ideas on speeding up inference time without losing preformance?
> 
> 
> 
> > ## Eisuke MizutaniTopic Author
> > 
> > One easy way is to cache LoRA_A x LoRA_B when it's first calculated, though it may not speed up that much.
> > 
> > I'm also wondering if we can use an optimization library like TensorRT or vLLM.
> > 
> > 
> > 
> > > ## Cody_Null
> > > 
> > > Have you tried vLLM? I have tried it but have not figured out how to get it to work yet. 
> > > 
> > > 
> > > 
> > > ## Eisuke MizutaniTopic Author
> > > 
> > > Not yet. I am aware that log loss decreases as max_length increases but the improvement is very small over 2048. Going from 2048 to 4096 reduced log loss by 0.002 in my case. I'm currently working on somewhere else to optimize given the time remaining.
> > > 
> > > 
> > > 


---

> ## carvingfate
> 
> I previously ranked 30th, but this code makes all my work seem useless. However, I respect your spirit of sharing, and I believe this is what the spirit of the Internet should be.
> 
> 
> 
> > ## jointcc2
> > 
> > state of industry too I guess, one model overcomes all previous efforts
> > 
> > 
> > 


---

> ## Van chrn
> 
> why not vllm？It mabe faster!
> 
> 
> 
> > ## Eisuke MizutaniTopic Author
> > 
> > I'm working on it!
> > 
> > 
> > 
> > > ## Cody_Null
> > > 
> > > Did you ever end up getting this to work? I have never used vLLM and would love to see it working!
> > > 
> > > 
> > > 


---

> ## Dai LinLing
> 
> Thank you for sharing, which has been a great help to me and a lot of understanding.
> 
> 
> 


---

> ## Turbo
> 
> [@emiz6413](https://www.kaggle.com/emiz6413)   Thanks for sharing the notebook.
> 
> 
> 


---

> ## Vitalii Bozheniuk
> 
> I can't get the idea of publishing silver tier solutions. Why not releasing 0.88 notebook so everybody has the 1st place? I do understand when people share some ideas or notebooks to do EDA or some baseline. But when it's literally a 30th place notebook, it doesn't make sense. All the challenge and competing atmosphere disappears.
> 
> 
> 
> > ## G John Rao
> > 
> > There is still a month to go though, for beginners, it's a boost; for seasoned professionals, one month is a lot of time to build on it or implement new ideas presented in the notebook. 
> > 
> > 
> > 


---

> ## Korey Ma
> 
> [@emiz6413](https://www.kaggle.com/emiz6413) Thank you for your notebook! I finetune some extra params and get  cv&lb(0.912&0.924).I want to try some other tricks to make it better😆
> 
> 
> 
> > ## Yichuan Gao
> > 
> > Would you like to share some more details? Are you tuning hyper params or adding more LoRA layers / rank? 
> > 
> > 
> > 
> > > ## Korey Ma
> > > 
> > > just adding "o_proj"&"gate_proj" 
> > > 
> > > 
> > > 


---

> ## samson
> 
> You made a decent notebook and your points in the comments are valid. 
> 
> Yet, why did you share the weights? If someone is truly passionate and eager to learn, they will use your method or adapt it to their own. However, you have prompted 100+ teams to blindly copy+submit. And now its is impossible for those who is in the middle of the pack to find proper teammates
> 
> 
> 


---

> ## superferg
> 
> Coooooooool
> 
> 
> 


---

> ## yuanzhe zhou
> 
> good job! So the key is using LLM? It seems that bert type models are too small to converge.
> 
> 
> 
> > ## Valentin Werner
> > 
> > Exactly this. I also thinkt that the LLMs are sufficiently finetuned on sequence generation, so they are more aware of AI generated texts and optimized for how text should look like. This makes them more fit for this task, basically fighting fire with fire.
> > 
> > 
> > 
> > > ## Eisuke MizutaniTopic Author
> > > 
> > > I actually tried full finetuning of deberta-v3-small and got something like 1.1.
> > > 
> > > I do think BERT style encoder architecture is theoretically more suitable for these classification tasks due to their bidirectional attention.
> > > 
> > > But, as you pointed out, practically LLM is much larger (deberta v2 xxlarge is 1.5B), which allows them to avoid overfitting and gives more memory capacity.
> > > 
> > > Another possible reason is instruction finetuning, which uses very similar data to this competition.
> > > 
> > > I haven't tested with vanilla gemma-2-9b, but it's interesting to see how it performs.
> > > 
> > > 
> > > 


---

> ## ano
> 
> [@emiz6413](https://www.kaggle.com/emiz6413) Thank you for your notebook! Can you tell me about the validation data and cv score of the fine-tuned model? Based on [your training notebook](https://www.kaggle.com/code/emiz6413/training-gemma-2-9b-4-bit-qlora-fine-tuning/notebook?scriptVersionId=187770530), I used around 20% of the data as validation based on the remainder of the number of rows divided by 5. Then I calculated the log loss, but the cv score was less than 0.9. I obviously made a mistake with the validation data because the cv score was written as 0.9371 in [your training notebook](https://www.kaggle.com/code/emiz6413/training-gemma-2-9b-4-bit-qlora-fine-tuning/notebook?scriptVersionId=187770530). Can you tell me how to create the validation data for the fine-tuned model used in this notebook?
> 
> 
> 
> > ## Eisuke MizutaniTopic Author
> > 
> > To create the validation data in my training notebook, please make sure the following line is not executed.
> > 
> > ```
> > # ds = ds.select(torch.arange(100))
> > 
> > ```
> > 
> > Then, this line in the last cell should select the validation set.
> > 
> > ```
> > ds.select(eval_idx)
> > 
> > ```
> > 
> > 
> > 
> > > ## ano
> > > 
> > > Thanks for your reply. Sure, I deleted the line to reduce the data. 
> > > 
> > > So, the validation data is selected with n_splits = 5 and fold_idx = 0 as in your training notebook? Hmm, then I might have made a mistake in my code to score CV. 
> > > 
> > > [UPDATE] I found a bug in my code. Thanks!
> > > 
> > > 
> > > 


---

> ## Guillermo Perez G
> 
> Brilliant! But I don't imagine that the score can be lowered further, or does it depend on the quality of the notebook?
> 
> 
> 
> > ## Eisuke MizutaniTopic Author
> > 
> > At the time of writing, the current top scorers are below 0.9. I presume there are still some ideas that can improve the score.
> > 
> > 
> > 
> > > ## floriandev
> > > 
> > > Hi Eisuke, many thx from my side for this great notebook! Did you mean by using your notebook one can go below 0.9?
> > > 
> > > 
> > > 


---

> ## Sparsh Tewatia
> 
> how much time it takes to finish , maybe we can do ensembling of two LLMs like LLAMA3 and Gemma 2 if time permits.
> 
> 
> 
> > ## Lorry Zou
> > 
> > It says around 4 hours in the notebook, so ensembling llama3 and gemma2 seems doable. 
> > 
> > 
> > 
> > > ## Eisuke MizutaniTopic Author
> > > 
> > > I could run llama3 and gemma2 ensemble within 9 hours. I used max_length=2048 and per_device_batch_size=4.
> > > 
> > > 
> > > 


---

> ## Lorry Zou
> 
> All the work I've done became useless…Sad😅 But great work though.
> 
> 
> 


---

> ## Sam
> 
> I decided to try the Gemma model with the same inference parameters (batch_size, max_length) as provided in this notebook. (Everything is the same except that I use the Bert-like model instead of llama). This notebook runs longer than 9 hours on a T4 x 2, so it's not getting to the end.
> 
> Decided to see what's up by running a test suite and saw that 25,000 examples would take ~17 hours to process with the Gemma model.
> 
> Can you advise what could be the issue? How can I speed up inference of Gemma model?
> 
> 
> 
> > ## Eisuke MizutaniTopic Author
> > 
> > [@andreysemenovmax](https://www.kaggle.com/andreysemenovmax) 
> > 
> > Dynamic quantization of Gemma2 9b with 8-bit weights and fp16 activation will run within 4.5h for submission.
> > 
> > 
> > 


---

> ## capyun007
> 
> I am new to Kaggle and I have a question. After running the following code to save  DataFrame as a CSV file:
> 
> submission_df.to_csv('submission.csv', index=False)
> 
> Where can I find the submission.csv file?
> 
> 
> 
> > ## Eisuke MizutaniTopic Author
> > 
> > If you commit & save the notebook, it should be visible in the output tab. If you execute in the interactive session, you can check in the working directory (./submission.csv)
> > 
> > 
> > 
> > > ## capyun007
> > > 
> > > <img src="https://www.googleapis.com/download/storage/v1/b/kaggle-forum-message-attachments/o/inbox%2F20838722%2F2bd6e2da0d08e709cca117654b058fd1%2FSnipaste_2024-07-20_20-00-44.png?generation=1721476909749673&alt=media" alt="![" />](https://www.googleapis.com/download/storage/v1/b/kaggle-forum-message-attachments/o/inbox%2F20838722%2F126ffa01a9b7f8c201c0abb0797ef9f4%2FSnipaste_2024-07-20_20-01-16.png?generation=1721476900963675&alt=media)
> > > 
> > > I use commit & save the notebook, But I can not see it in the output tab.
> > > 
> > > 
> > > 


---

> ## kanishka sriramoju
> 
> Hey there I'm a beginner here . I see you have loaded pre trained model from the kaggle input directory . In some competitions the notebooks run in an independent environment where these created directories cannot be accessed. Is this true for this competition as well or am i delusional
> 
> 
> 
> > ## Eisuke MizutaniTopic Author
> > 
> > I've made those datasets public, so they should be accessible during submission.
> > 
> > 
> > 


---

