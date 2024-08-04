# lmsys chat 1m (is Allowed? - dataset consists of user interactions from the ChatBot Arena) [Solved - Allowed]

**SeshuRaju 🧘‍♂️** *Fri May 03 2024 14:00:35 GMT+0900 (日本標準時)* (24 votes)

## [IMSYS Chat 1M](https://huggingface.co/datasets/lmsys/lmsys-chat-1m)

## KeyValue

| Metric | Value |
| --- | --- |
| Conversations | 1,000,000 |
| Models | 25 |
| Users | 210,479 |
| Languages | 154 |
| Avg. # Turns per Sample | 2.0 |
| Avg. # Tokens per Prompt | 69.5 |
| Avg. # Tokens per Response | 214.5 |

## [Paper - LMSYS-CHAT-1M: A LARGE-SCALE REAL-WORLD LLM CONVERSATION DATASET](https://arxiv.org/pdf/2309.11998)

- LMSYS-Chat-1M is collected from April to August 2023 - on website [https://chat.lmsys.org/](https://chat.lmsys.org/)

- The dataset contains raw conversation text without any processing. To ensure the safe release of

  data, we have made our best efforts to remove conversations that contain personally identifiable

  information (PII).

- The dataset includes one million conversations from 25 state-of-the-art LLMs with 210K users

  across more than 150 languages.

- We remove prompts that are either too short (fewer than 32 characters) or too long (more than 1536 characters).

- Biased user distribution : The majority of users of our website are LLM hobbyists and researchers who are interested in trying and testing the latest LLMs. This suggests that the data

  might not fully represent the broader population. For instance, everyday users or individuals

  from different professions might interact with the LLMs in varied ways. Consequently, results

  derived from this dataset might not generalize across all user groups.

- Containing repeated and low-quality data : The lack of user registration and data filtering can

  result in a significant amount of low-quality and duplicate data. However, we choose to not

  apply any filtering on purpose to reflect the real-world distribution.

- No human preference annotations. This dataset contains raw conversations without any human

  preference annotations. While our website does collect some user votes, we plan to examine

  the quality further before releasing them. We encourage the community to check the human

  preference data released in (Zheng et al., 2023).

# We can compare the Kaggle dataset with 1m dataset

- is PII added and removed more similar prompts or questions as suggested by paper ?

- Generate targets for the filtered dataset using GPT-4

- We can probe LB to check is this data topics exists in private LB ( as 20 clusters  for random 100k as per paper )



---

 # Comments from other users

> ## Lisa DunlapCompetition Host
> 
> Hello! Organizer here: yes it is allowed :)
> 
> 
> 


---

> ## Gaurav Rawat
> 
> Had exactly the same question about some of the lmsys datasets on hugging face ideally most are open I am guessing should be fine
> 
> 
> 
> > ## SeshuRaju 🧘‍♂️Topic Author
> > 
> > I expected the same, till now organiser not conformed. maybe we can consider it as Yes
> > 
> > 
> > 


---

