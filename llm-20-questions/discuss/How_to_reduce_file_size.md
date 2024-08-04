# How to reduce file size

**Yuang Wu** *Sun Jul 14 2024 21:44:07 GMT+0900 (日本標準時)* (1 votes)

I've tried Gemma2 and Gemma 7b-it, and the submission file exceeds in both situation. What could be the solution?



---

 # Comments from other users

> ## Jasper Butcher
> 
> What compression algorithm are you using? The submission file caps out at 100 Gb's, and most ~8b parameter models take up only around 10-15 Gbs.
> 
> The pigz compression programme is what most people are using for this competition:
> 
> ```
> !tar --use-compress-program='pigz --fast --recursive | pv' -cf submission.tar.gz -C /kaggle/input/path/to/weights . -C /kaggle/working/submission .
> 
> ```
> 
> You can also just use the following to clone every file in your submission/ directory, where -9 indicates the maximum level of compression:
> 
> ```
> !tar -cf - -C submission . | pigz -9 > submission.tar.gz 
> 
> ```
> 
> 
> 
> > ## Yuang WuTopic Author
> > 
> > What? My cap is 19.5GB…
> > 
> > 
> > 
> > > ## Chris Deotte
> > > 
> > > Yuang, maybe you are referring the the limit output size to a Kaggle notebook. If you create a 100GB file locally, you can upload it and submit to this comp. However the output folder of a Kaggle notebook caps at 20GB i think.
> > > 
> > > 
> > > 


---

