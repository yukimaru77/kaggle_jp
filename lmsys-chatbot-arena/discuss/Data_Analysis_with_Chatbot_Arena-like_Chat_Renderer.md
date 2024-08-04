# Data Analysis with Chatbot Arena-like Chat Renderer

**AbaoJiang** *Mon May 27 2024 17:00:34 GMT+0900 (日本標準時)* (8 votes)

Hi everyone,

This is the first time I join an NLP competition. I'm so excited because I need to learn everything from scratch! The very first step is to analyze the data. To facilitate model comparison side by side, instead of scrolling up and down to analyze responses from two models, I write a simple static chat renderer with Chatbot Arena-like UI (co-author by ChatGPT). Following is a screenshot of one chat,

[](https://postimg.cc/Tyyhq5RC)

This renderer supports,

Pair comparison between responses from two models.
Markdown rendering powered by [<md-block>](https://md-block.verou.me/).
- e.g., strong and italic fonts, unordered and ordered lists, etc.

Unicode rendering.
- Characters like emojis can be shown.

[](https://postimg.cc/VdffWZ1K)

Also, winner is displayed at the bottom! I hope this can make raw text analysis more handy.

In addition, I also implement the win rate and battle count heatmaps in [the official paper](https://arxiv.org/pdf/2403.04132). We can use this to find frequent model pairs (i.e., battle counts) and which model has the higher win rate (e.g., gpt-4-1106-preview has only 17.42% lose rate).

[](https://postimg.cc/ThswTMDB)

For detailed implementation, please refer to [LMSYS - Detailed EDA](https://www.kaggle.com/code/abaojiang/lmsys-detailed-eda/notebook).

I'll share more analysis and insights during this interesting learning journey. Hope you like it!



---

 # Comments from other users

> ## Hafiz Nouman
> 
> Amazing Improvement keep it up 
> 
> Review my dataset and give some suggestions on it how I can improve my work
> 
> 
> 


---

