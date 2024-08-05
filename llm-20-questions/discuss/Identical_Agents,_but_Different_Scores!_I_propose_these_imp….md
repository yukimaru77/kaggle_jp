# Identical Agents, but Different Scores! I propose these improvements. What do you think?

**tiod0611** *Sun Jul 07 2024 00:01:30 GMT+0900 (日本標準時)* (2 votes)

Hello everyone. 

I've noticed an issue in the current competition where agents, built with the same model and code, are receiving significantly different scores—sometimes differing by more than 100 points!

Here are my thoughts on the potential reasons and some proposed solutions. I would like to share these with you for further discussion.

## Issues

Agents created from the same code are receiving different scores.

The reasons for this could be:

### Keyword Difficulty Variability:

- Some words are difficult even for humans to guess, and large language models (LLMs) would also struggle with these words. Agents encountering easier words score higher, while those facing harder words tend to have more draws. This issue has been repeatedly raised:

[https://www.kaggle.com/competitions/llm-20-questions/discussion/515751#2902081](https://www.kaggle.com/competitions/llm-20-questions/discussion/515751#2902081)

[https://www.kaggle.com/competitions/llm-20-questions/discussion/509839](https://www.kaggle.com/competitions/llm-20-questions/discussion/509839)

### [Err]-Generating Agents:

- When an agent encounters an [Err]-generating agent, other agents gain higher scores effortlessly.

Due to these factors, agents frequently encountering easy words and [Err] agents can score higher than others.

## Proposed Solutions

To address these issues, I propose the following improvements:

### Balancing Keyword Difficulty:

- Assuming Kaggle knows the accuracy rate of each keyword, agents should encounter a balanced mix of high and low accuracy rate words.

- For instance, if keywords are divided into five groups based on accuracy rates, agents should compete in games that cover each group, ensuring fair play. This cycle should repeat continuously.

- However, The first cycle after an agent is submitted should not take too long, ideally completed within a day, to provide participants with timely feedback on their model performance.

- To prevent cheating, some matches could be conducted blind.

### Improving [Err] Handling:

- Matches resulting in [Err] should not count towards the score and should be immediately replayed.

- If an agent repeatedly causes [Err], it should be excluded from further matches.

Thank you for reading my suggestions. I look forward to a productive discussion.



