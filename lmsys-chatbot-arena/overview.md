# LMSYS - Chatbot Arena Human Preference Predictions

Predicting Human Preferences in the Wild



[Overview](/competitions/lmsys-chatbot-arena/overview)　[Data](/competitions/lmsys-chatbot-arena/data)　[Code](/competitions/lmsys-chatbot-arena/code)　[Models](/competitions/lmsys-chatbot-arena/models)　[Discussion](/competitions/lmsys-chatbot-arena/discussion)　[Leaderboard](/competitions/lmsys-chatbot-arena/leaderboard)　[Rules](/competitions/lmsys-chatbot-arena/rules)　

## Overview

This competition challenges you to predict which responses users will prefer in a head-to-head battle between chatbots powered by large language models (LLMs). You'll be given a dataset of conversations from the [Chatbot Arena](https://chat.lmsys.org/), where different LLMs generate answers to user prompts. By developing a winning machine learning model, you'll help improve how chatbots interact with humans and ensure they better align with human preferences.

### Description

Large language models (LLMs) are rapidly entering our lives, but ensuring their responses resonate with users is critical for successful interaction. This competition presents a unique opportunity to tackle this challenge with real-world data and help us bridge the gap between LLM capability and human preference.

We utilized a large dataset collected from Chatbot Arena, where users chat with two anonymous LLMs and choose the answer they prefer. Your task in this competition is to predict which response a user will prefer in these head-to-head battles.

This challenge aligns with the concept of "reward models" or "preference models" in reinforcement learning from human feedback (RLHF). Previous research has identified limitations in directly prompting an existing LLM for preference predictions. These limitations often stem from biases such as favoring responses presented first (position bias), being overly verbose (verbosity bias), or exhibiting self-promotion (self-enhancement bias).

We encourage you to explore various machine-learning techniques to build a model that can effectively predict user preferences. Your work will be instrumental in developing LLMs that can tailor responses to individual user preferences, ultimately leading to more user-friendly and widely accepted AI-powered conversation systems.

### Evaluation

Submissions are evaluated on the [log loss](https://www.kaggle.com/code/metric/log-loss?scriptVersionId=151169978) between the predicted probabilities and the ground truth values (with "eps=auto"). 

## Submission File

For each id in the test set, you must predict the probability for each target class. The file should contain a header and have the following format:

```
 id,winner_model_a,winner_model_b,winner_tie
 136060,0.33,0,33,0.33
 211333,0.33,0,33,0.33
 1233961,0.33,0,33,0.33
 etc

```

### Timeline


- May 2, 2024 - Start Date. 

- July 29, 2024 - Entry Deadline. You must accept the competition rules before this date in order to compete. 

- July 29, 2024 - Team Merger Deadline. This is the last day participants may join or merge teams. 

- August 5, 2024 - Final Submission Deadline. 

All deadlines are at 11:59 PM UTC on the corresponding day unless otherwise noted. The competition organizers reserve the right to update the contest timeline if they deem it necessary.

### Prizes


- 1st Place - $25,000

- 2nd Place - $20,000

- 3rd Place - $20,000

- 4th Place - $20,000

- 5th Place - $15,000

### Code Requirements



### This is a Code Competition

Submissions to this competition must be made through Notebooks. In order for the "Submit" button to be active after a commit, the following conditions must be met:

- CPU Notebook <= 9 hours run-time

- GPU Notebook <= 9 hours run-time

- Internet access disabled

- Freely & publicly available external data is allowed, including pre-trained models

- Submission file must be named submission.csv

- Submission runtimes have been slightly obfuscated. If you repeat the exact same submission you will see up to 15 minutes of variance in the time before you receive your score.

Please see the [Code Competition FAQ](https://www.kaggle.com/docs/competitions#notebooks-only-FAQ) for more information on how to submit. And review the [code debugging doc](https://www.kaggle.com/code-competition-debugging) if you are encountering submission errors.

### Citation

Wei-lin Chiang, Lianmin Zheng, Lisa Dunlap, Joseph E. Gonzalez, Ion Stoica, Paul Mooney, Sohier Dane, Addison Howard, Nate Keating. (2024). LMSYS - Chatbot Arena Human Preference Predictions. Kaggle. https://kaggle.com/competitions/lmsys-chatbot-arena

## Competition Host

LMSYS ORG

[](/organizations/lmsysorg)## Prizes & Awards

$100,000

Awards Points & Medals

## Participation

8,928 Entrants

2,323 Participants

1,791 Teams

38,283 Submissions

## Tags

[Languages](/competitions?tagIds=2107-Languages)[Text Conversation](/competitions?tagIds=16723-Text+Conversation)[Log Loss]()Table of Contentscollapse_all[Overview](/competitions/lmsys-chatbot-arena/overview/abstract)[Description](/competitions/lmsys-chatbot-arena/overview/description)[Evaluation](/competitions/lmsys-chatbot-arena/overview/evaluation)[Timeline](/competitions/lmsys-chatbot-arena/overview/timeline)[Prizes](/competitions/lmsys-chatbot-arena/overview/prizes)[Code Requirements](/competitions/lmsys-chatbot-arena/overview/code-requirements)[Citation](/competitions/lmsys-chatbot-arena/overview/citation)

# LMSYS - Chatbot Arena Human Preference Predictions

Predicting Human Preferences in the Wild



[Overview](/competitions/lmsys-chatbot-arena/overview)　[Data](/competitions/lmsys-chatbot-arena/data)　[Code](/competitions/lmsys-chatbot-arena/code)　[Models](/competitions/lmsys-chatbot-arena/models)　[Discussion](/competitions/lmsys-chatbot-arena/discussion)　[Leaderboard](/competitions/lmsys-chatbot-arena/leaderboard)　[Rules](/competitions/lmsys-chatbot-arena/rules)　

## Overview

This competition challenges you to predict which responses users will prefer in a head-to-head battle between chatbots powered by large language models (LLMs). You'll be given a dataset of conversations from the [Chatbot Arena](https://chat.lmsys.org/), where different LLMs generate answers to user prompts. By developing a winning machine learning model, you'll help improve how chatbots interact with humans and ensure they better align with human preferences.

### Description

Large language models (LLMs) are rapidly entering our lives, but ensuring their responses resonate with users is critical for successful interaction. This competition presents a unique opportunity to tackle this challenge with real-world data and help us bridge the gap between LLM capability and human preference.

We utilized a large dataset collected from Chatbot Arena, where users chat with two anonymous LLMs and choose the answer they prefer. Your task in this competition is to predict which response a user will prefer in these head-to-head battles.

This challenge aligns with the concept of "reward models" or "preference models" in reinforcement learning from human feedback (RLHF). Previous research has identified limitations in directly prompting an existing LLM for preference predictions. These limitations often stem from biases such as favoring responses presented first (position bias), being overly verbose (verbosity bias), or exhibiting self-promotion (self-enhancement bias).

We encourage you to explore various machine-learning techniques to build a model that can effectively predict user preferences. Your work will be instrumental in developing LLMs that can tailor responses to individual user preferences, ultimately leading to more user-friendly and widely accepted AI-powered conversation systems.

### Evaluation

Submissions are evaluated on the [log loss](https://www.kaggle.com/code/metric/log-loss?scriptVersionId=151169978) between the predicted probabilities and the ground truth values (with "eps=auto"). 

## Submission File

For each id in the test set, you must predict the probability for each target class. The file should contain a header and have the following format:

```
 id,winner_model_a,winner_model_b,winner_tie
 136060,0.33,0,33,0.33
 211333,0.33,0,33,0.33
 1233961,0.33,0,33,0.33
 etc

```

### Timeline


- May 2, 2024 - Start Date. 

- July 29, 2024 - Entry Deadline. You must accept the competition rules before this date in order to compete. 

- July 29, 2024 - Team Merger Deadline. This is the last day participants may join or merge teams. 

- August 5, 2024 - Final Submission Deadline. 

All deadlines are at 11:59 PM UTC on the corresponding day unless otherwise noted. The competition organizers reserve the right to update the contest timeline if they deem it necessary.

### Prizes


- 1st Place - $25,000

- 2nd Place - $20,000

- 3rd Place - $20,000

- 4th Place - $20,000

- 5th Place - $15,000

### Code Requirements



### This is a Code Competition

Submissions to this competition must be made through Notebooks. In order for the "Submit" button to be active after a commit, the following conditions must be met:

- CPU Notebook <= 9 hours run-time

- GPU Notebook <= 9 hours run-time

- Internet access disabled

- Freely & publicly available external data is allowed, including pre-trained models

- Submission file must be named submission.csv

- Submission runtimes have been slightly obfuscated. If you repeat the exact same submission you will see up to 15 minutes of variance in the time before you receive your score.

Please see the [Code Competition FAQ](https://www.kaggle.com/docs/competitions#notebooks-only-FAQ) for more information on how to submit. And review the [code debugging doc](https://www.kaggle.com/code-competition-debugging) if you are encountering submission errors.

### Citation

Wei-lin Chiang, Lianmin Zheng, Lisa Dunlap, Joseph E. Gonzalez, Ion Stoica, Paul Mooney, Sohier Dane, Addison Howard, Nate Keating. (2024). LMSYS - Chatbot Arena Human Preference Predictions. Kaggle. https://kaggle.com/competitions/lmsys-chatbot-arena

## Competition Host

LMSYS ORG

[](/organizations/lmsysorg)## Prizes & Awards

$100,000

Awards Points & Medals

## Participation

8,928 Entrants

2,346 Participants

1,808 Teams

39,452 Submissions

## Tags

[Languages](/competitions?tagIds=2107-Languages)[Text Conversation](/competitions?tagIds=16723-Text+Conversation)[Log Loss]()Table of Contentscollapse_all[Overview](/competitions/lmsys-chatbot-arena/overview/abstract)[Description](/competitions/lmsys-chatbot-arena/overview/description)[Evaluation](/competitions/lmsys-chatbot-arena/overview/evaluation)[Timeline](/competitions/lmsys-chatbot-arena/overview/timeline)[Prizes](/competitions/lmsys-chatbot-arena/overview/prizes)[Code Requirements](/competitions/lmsys-chatbot-arena/overview/code-requirements)[Citation](/competitions/lmsys-chatbot-arena/overview/citation)

# LMSYS - Chatbot Arena Human Preference Predictions

Predicting Human Preferences in the Wild



[Overview](/competitions/lmsys-chatbot-arena/overview)　[Data](/competitions/lmsys-chatbot-arena/data)　[Code](/competitions/lmsys-chatbot-arena/code)　[Models](/competitions/lmsys-chatbot-arena/models)　[Discussion](/competitions/lmsys-chatbot-arena/discussion)　[Leaderboard](/competitions/lmsys-chatbot-arena/leaderboard)　[Rules](/competitions/lmsys-chatbot-arena/rules)　

## Overview

This competition challenges you to predict which responses users will prefer in a head-to-head battle between chatbots powered by large language models (LLMs). You'll be given a dataset of conversations from the [Chatbot Arena](https://chat.lmsys.org/), where different LLMs generate answers to user prompts. By developing a winning machine learning model, you'll help improve how chatbots interact with humans and ensure they better align with human preferences.

### Description

Large language models (LLMs) are rapidly entering our lives, but ensuring their responses resonate with users is critical for successful interaction. This competition presents a unique opportunity to tackle this challenge with real-world data and help us bridge the gap between LLM capability and human preference.

We utilized a large dataset collected from Chatbot Arena, where users chat with two anonymous LLMs and choose the answer they prefer. Your task in this competition is to predict which response a user will prefer in these head-to-head battles.

This challenge aligns with the concept of "reward models" or "preference models" in reinforcement learning from human feedback (RLHF). Previous research has identified limitations in directly prompting an existing LLM for preference predictions. These limitations often stem from biases such as favoring responses presented first (position bias), being overly verbose (verbosity bias), or exhibiting self-promotion (self-enhancement bias).

We encourage you to explore various machine-learning techniques to build a model that can effectively predict user preferences. Your work will be instrumental in developing LLMs that can tailor responses to individual user preferences, ultimately leading to more user-friendly and widely accepted AI-powered conversation systems.

### Evaluation

Submissions are evaluated on the [log loss](https://www.kaggle.com/code/metric/log-loss?scriptVersionId=151169978) between the predicted probabilities and the ground truth values (with "eps=auto"). 

## Submission File

For each id in the test set, you must predict the probability for each target class. The file should contain a header and have the following format:

```
 id,winner_model_a,winner_model_b,winner_tie
 136060,0.33,0,33,0.33
 211333,0.33,0,33,0.33
 1233961,0.33,0,33,0.33
 etc

```

### Timeline


- May 2, 2024 - Start Date. 

- July 29, 2024 - Entry Deadline. You must accept the competition rules before this date in order to compete. 

- July 29, 2024 - Team Merger Deadline. This is the last day participants may join or merge teams. 

- August 5, 2024 - Final Submission Deadline. 

All deadlines are at 11:59 PM UTC on the corresponding day unless otherwise noted. The competition organizers reserve the right to update the contest timeline if they deem it necessary.

### Prizes


- 1st Place - $25,000

- 2nd Place - $20,000

- 3rd Place - $20,000

- 4th Place - $20,000

- 5th Place - $15,000

### Code Requirements



### This is a Code Competition

Submissions to this competition must be made through Notebooks. In order for the "Submit" button to be active after a commit, the following conditions must be met:

- CPU Notebook <= 9 hours run-time

- GPU Notebook <= 9 hours run-time

- Internet access disabled

- Freely & publicly available external data is allowed, including pre-trained models

- Submission file must be named submission.csv

- Submission runtimes have been slightly obfuscated. If you repeat the exact same submission you will see up to 15 minutes of variance in the time before you receive your score.

Please see the [Code Competition FAQ](https://www.kaggle.com/docs/competitions#notebooks-only-FAQ) for more information on how to submit. And review the [code debugging doc](https://www.kaggle.com/code-competition-debugging) if you are encountering submission errors.

### Citation

Wei-lin Chiang, Lianmin Zheng, Lisa Dunlap, Joseph E. Gonzalez, Ion Stoica, Paul Mooney, Sohier Dane, Addison Howard, Nate Keating. (2024). LMSYS - Chatbot Arena Human Preference Predictions. Kaggle. https://kaggle.com/competitions/lmsys-chatbot-arena

## Competition Host

LMSYS ORG

[](/organizations/lmsysorg)## Prizes & Awards

$100,000

Awards Points & Medals

## Participation

8,928 Entrants

2,346 Participants

1,808 Teams

39,456 Submissions

## Tags

[Languages](/competitions?tagIds=2107-Languages)[Text Conversation](/competitions?tagIds=16723-Text+Conversation)[Log Loss]()Table of Contentscollapse_all[Overview](/competitions/lmsys-chatbot-arena/overview/abstract)[Description](/competitions/lmsys-chatbot-arena/overview/description)[Evaluation](/competitions/lmsys-chatbot-arena/overview/evaluation)[Timeline](/competitions/lmsys-chatbot-arena/overview/timeline)[Prizes](/competitions/lmsys-chatbot-arena/overview/prizes)[Code Requirements](/competitions/lmsys-chatbot-arena/overview/code-requirements)[Citation](/competitions/lmsys-chatbot-arena/overview/citation)

