# ChatBot Arena Prompts Can Distinguish Models. The Bradley-Terry model. Elo Ratings on Kaggle.

**Marília Prata** *Fri May 03 2024 14:27:26 GMT+0900 (日本標準時)* (42 votes)

# ChatBot Arena

Super cool Notebook Chatbot Arena MLE Elo Rating

[Chatbot Arena: MLE Elo Rating (Bradley-Terry model) Calculation (Apr 22, 2024)](#https://colab.research.google.com/drive/1KdwokPjirkTmpO_P1WByFNFiqxWQquwH#scrollTo=B_PYA7oVyaHO)

"Maximum Likelihood Estimation for Elo Ratings (aka Bradley-Terry model). In the context of LLM evaluation, models can be assumed to be static. In this case, the authors could directly fit the ratings by maximum likelihood estimation method (aka Bradley-Terry model), which produce significantly stable ratings. Here they provided an implementation with logistic regression."

[https://colab.research.google.com/drive/1KdwokPjirkTmpO_P1WByFNFiqxWQquwH#scrollTo=PbTdhkLQp113](https://colab.research.google.com/drive/1KdwokPjirkTmpO_P1WByFNFiqxWQquwH#scrollTo=PbTdhkLQp113)

# Chatbot Arena: An Open Platform for Evaluating LLMs by Human Preference

Authors: Wei-Lin Chiang, Lianmin Zheng, Ying Sheng, Anastasios N. Angelopoulos, Tianle Li, Dacheng Li, Banghua Zhu, HaoZhang, Michael I. Jordan, Joseph E. Gonzalez, Ion Stoica.

"To assess the performance of LLMs, the research community has introduced a variety of benchmarks. These benchmarks can be categorized based on two factors: the source of questions (either static or live) and the evaluation metric (either ground truth or human preference). According to these fac tors, benchmarks can be classified into four categories. While a range of benchmarks is beneficial, the most prevalent current method for evaluating LLMs remains a static, ground-truth-based evaluation, partly because such evaluations are inexpensive and reproducible."

"However, these static, ground-truth-based benchmarks exhibit several limitations. Firstly, the questions within these benchmarks are not open-ended, hindering the ability to capture the flexible and interactive use found in real-world settings. Secondly, the test sets in these benchmarks are static, meaning they can become contaminated over time, which undermines the reliability of the evaluation results. Furthermore,for many complex tasks, establishing a definitive ground truth is not only challenging but sometimes unattainable."

" Consequently, current benchmarks fail to adequately address the needs of state-of-the-art LLMs, particularly in evaluating user preferences. Thus, there is an urgent necessity for an open, live evaluation platform based on human preference that can more accurately mirror real-world usage."

"Creating such a benchmark platform entails significant challenges. It requires the collection of live, fresh, and diverse user questions to accurately represent real-world scenarios."

CONTRIBUTIONS MADE by the AUTHORS:

"They built the first large-scale crowd-sourced live LLM evaluation platform with over 1M users visit."

"They conducted an in-depth analysis of the collected data, including prompt diversity, quality, vote quality, and insights on human feedback."

"They will publicly release a human preference dataset with over 100K pairwise votes collected from Chatbot Arena."

"They designed an efficient sampling algorithm that actively chooses which model pairs to show, such that our sample efficiency improves, sometimes to a large degree."

# Risks of Static Benchmarks.

"Static benchmarks have certain issues, including contamination, saturation, overfitting, and a lack of human alignment. DynaBench identifies these challenges and recommends the use of a live benchmark that incorporates a human-in-the-loop approach for classical NLP benchmarks. Their system adopts a similar spirit."

DATA STATISTICS 

"The authors began collecting data in April 2023. As of Jan 2024, they have received around 240K votes from over 90K users. Their data involves more than 50 models, including both proprietary models like GPT-4, Claude, and Gemini, as well as open models such as LLaMA and Mistral. These conversations cover more than 100 languages, with 77% being in English, 5% in Chinese, and the remaining languages, such as Russian, German, Spanish, French, and Japanese, each representing less than 2% of the total. Each data point includes multi-turn conversations between the user and two LLMs, and a vote to indicate which model the user prefers."

# Can Arena Prompts Distinguish Models?

"The authors studied how effective are these topic clusters in distinguishing models strengths. Their result shows models may exhibit varying strengths in different areas, but also highlights some of the topic clusters in Chatbot Arena are effective in differentiate models."

[https://arxiv.org/pdf/2403.04132](https://arxiv.org/pdf/2403.04132)

# Elo Ratings

Remember that it is "Elo", not "ELO" since it was named after Arpad Elo. The USCF implemented Arpad Elo's suggestions in 1960, and the system quickly gained recognition as being both fairer and more accurate than the Harkness rating system.

[Elo rating system](https://en.wikipedia.org/wiki/Elo_rating_system)

"The Elo rating system is a method for calculating the relative skill levels of players, which has been widely adopted in chess and other competitive games. The difference in the ratings between two players serves as a predictor of the outcome of a match. The Elo rating system works well for our case because we have multiple models and we run pairwise battles between them. In this section, we present different methods for calculating Elo ratings."

Compute Ratings

"The authors first use the online linear update algorithm to compute Elo ratings. They chose a small K-factor of 4 to make the Elo ratings more stable and less biased towards recent games."

[https://colab.research.google.com/drive/1KdwokPjirkTmpO_P1WByFNFiqxWQquwH#scrollTo=B_PYA7oVyaHO](https://colab.research.google.com/drive/1KdwokPjirkTmpO_P1WByFNFiqxWQquwH#scrollTo=B_PYA7oVyaHO)

# Elo Ratings on Kaggle

KAGGLE TOPICS:

[Intro to Rating Systems](https://www.kaggle.com/competitions/chess/discussion/92) By Jeff Sonas - 14 y ago

[Elo Ratings Shiny App for Euro Soccer Teams](https://www.kaggle.com/datasets/hugomathien/soccer/discussion/31154) By Kevin Pan - 8 y ago

[Elo RATING ALGORITHM](https://www.kaggle.com/discussions/getting-started/216048) By Kaushik Deb

KAGGLE NOTEBOOKS:

[Elo Ratings in Python](https://www.kaggle.com/code/kplauritzen/elo-ratings-in-python) By Kasper P. Lauritzen

[Simple Simulation & Elo Rating Approach](https://www.kaggle.com/code/kenjee/simple-simulation-elo-rating-approach) By Ken Jee

[Custom Football Elo Rating](https://www.kaggle.com/code/thomasstokes/custom-football-elo-rating) By Thomas Stokes

There are many more on Kaggle. I've just picked a few to exemplify. Therefore, search by Code or Discussion if you intend to read more material.



