# How Are Keywords with Typographical Errors Handled?

**tiod0611** *Thu Jun 27 2024 20:40:22 GMT+0900 (日本標準時)* (5 votes)

Hello,

While analyzing the keywords, I found a few words that seem to contain typographical errors. The list of these words is as follows:

isafahan iran → isfahan

nurumberg germany → nuremberg

zincantan mexico → zinacantan

mount saint lias → mount saint elias

On the left are the words from the keywords.py file, and on the right are the actual words. I am curious about the scoring results when an agent encounters these keywords and provides the correct word.

I am concerned that answering "isfahan" for "isafahan" might result in an incorrect response.



---

 # Comments from other users

> ## DJ Sterling
> 
> Sorry for the mistakes here.  These keywords have been removed from the set entirely.
> 
> 
> 
> > ## tiod0611Topic Author
> > 
> > Thank you for your action. 😎
> > 
> > 
> > 


---

> ## RS Turley
> 
> Sadly, in those cases, the correctly spelled answer would not be recognized. 
> 
> While each keyword has a list of potential alternative strings that would be marked correct, none of the examples you shared above have correctly spelled alternatives in the file.
> 
> 
> 
> > ## tiod0611Topic Author
> > 
> > Thank you for answering. I think we should intentionally answer with the incorrect keyword. For example, if the keyword is "isfahan," we should answer "isafahan" instead.
> > 
> > 
> > 
> > ## Kirill Yakunin
> > 
> > What about capitalization? Does "headphones" vs "Headphones" matter? "Mount saint elias" vs "mount saint Elias"?
> > 
> > 
> > 
> > > ## tiod0611Topic Author
> > > 
> > > I think It doesn't matter. In game my agent played, the keyword was "granola", but it answered with "Granoal". It got the win.
> > > 
> > > 
> > > 


---

