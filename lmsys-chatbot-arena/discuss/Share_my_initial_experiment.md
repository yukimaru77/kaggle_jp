# Share my initial experiment

**suguuuuu** *Thu Jul 04 2024 01:24:22 GMT+0900 (日本標準時)* (22 votes)

Since it seems I won't be able to continue this competition, I am sharing a concept that I explored a month ago. It's possible that similar content has already been shared in other discussions.

It might be completely meaningless information.

## update (2024/07/06)

Upload results. [https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/516806#2905904](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/516806#2905904)

## Initial Approach

Compare texts across various criteria  based on a weighted average score according to categories.

### Evaluation Criteria:

```
1. **Clarity**: AI can provide clear answers to specific questions. However, when questions are ambiguous or open to multiple interpretations, AI may not always deliver the optimal response.

2. **Accuracy of Information**: AI answers are based on the data and information provided. Thus, if the source is accurate, the AI's response is accurate. However, AI lacks the capability to discern incorrect information from sources.

3. **Completeness**: AI can provide comprehensive answers to questions, but only within the scope of what it has understood and learned. Unlike humans, AI does not possess the ability to supplement information based on intuition or experience.

4. **Conciseness**: AI is capable of delivering concise responses. However, what qualifies as "concise" can largely depend on context and human subjectivity, making it challenging for AI to always meet human expectations for brevity.

```

### Categories:

- Informational Queries:

Accuracy of Information: Most crucial. If the information sought by the user is inaccurate, the value of the response significantly decreases.
Completeness: Next in importance. Providing all necessary information comprehensively is expected to fully resolve the user's queries.
Clarity: It is also important that accurate information is presented in an understandable manner.
Conciseness: Important, but often secondary to accuracy and completeness. However, irrelevant information should be avoided.

- Dialogue and Engagement Queries:

Clarity: For engaging effectively, it is crucial that responses are easy to understand.
Conciseness: Favored for maintaining fluid dialogue; responses should be brief and clear.
Accuracy of Information: Accuracy remains important in dialogic contexts, but because entertainment elements may be involved, strict accuracy isn't always necessary.
Completeness: Important, but not always necessary to cover every aspect to advance the dialogue.

- Emotional Support and Consultation Queries:

Clarity: Responses that resonate with users' emotions need to be particularly clear.
Accuracy of Information: Reliable information or advice is necessary when providing emotional support.
Completeness: Providing a comprehensive view on the issue helps users feel reassured.
Conciseness: While important, it is somewhat secondary compared to other factors.

- Troubleshooting Queries:

Accuracy of Information: Accurate troubleshooting steps and information are extremely crucial.
Clarity: Solutions must be clear for users to resolve issues.
Completeness: Covering all necessary steps required for problem resolution is demanded.
Conciseness: Useful but considered least crucial among the factors, though irrelevant information should be omitted.

## Experiments :

Utilized ChatGPT-4o for a trial with 500 data points.

- normal_prediction
Accuracy : 0.492

- predict with criteria
Accuracy : 0.514

Example result:

- ground truth and input data

```
  winner_model_a    0
  winner_model_b    1
  winner_tie        0
  ["What is the scientific probability of earth being the only habitable planet in the universe?","I don't think it really matters what some scientists \"think\" because it's very possible it could all be a simulation. And there's actual evidence to back that up.","But what makes that a \"radical\" possibility, when it's the possibility with actual evidence?"]

```

- Predict with ChatGPT-4o

winner model B

```
  ★res_a:
  Clarity: 4
  Accuracy of Information: 4
  Completeness: 5
  Conciseness: 3

  Reasoning:
  - Clarity: Responses are generally clear and appropriate for the questions, but occasionally complex words or concepts are used, requiring specialized knowledge for full understanding.
  - Accuracy of Information: The provided information is accurate and based on the latest scientific findings, although some claims about the simulation hypothesis are philosophical and lack scientific evidence.
  - Completeness: Responses are very comprehensive, considering the issue from multiple perspectives.
  - Conciseness: While detailed, the responses are sometimes lengthy and can feel redundant, so a more concise presentation could improve them.

  ★res_b:
  Clarity: 5
  Accuracy of Information: 5
  Completeness: 5
  Conciseness: 4

  This response is clear and accurate, providing relevant information comprehensively. However, some parts are slightly verbose, thus a conciseness score of 4.

```

- prompt/code

```
import requests
import pandas as pd
from time import sleep
from tqdm import tqdm

def generate_response_for_LMSYS(api_key, prompt):
    url = "https://api.openai.com/v1/chat/completions"
    headers = {
        "Authorization": f"Bearer {api_key}",
        "Content-Type": "application/json",
    }
    data = {
        "model": "gpt-4o",
        "messages": [
            {"role": "system",                  
                "content": "Please evaluate each response on a scale of up to 5 points. Format it as 'Clarity:x, Accuracy of Information:x, Completeness:x, Conciseness:x'. "},         
            {"role": "user", "content": prompt}
        ],
        "temperature": 0.7,
        "max_tokens": 1000
    }

    response = requests.post(url, json=data, headers=headers)
    if response.status_code == 200:
        return response.json()['choices'][0]['message']['content']
    else:
        return "Error: " + response.text    

idx = 150
print(train[["winner_model_a","winner_model_b","winner_tie"]].iloc[idx])

print(train["prompt"].iloc[idx])

print()
print("======================")
print( train["response_a"].iloc[idx])

print()
print("======================")
print( train["response_b"].iloc[idx])

all_prompt = f"""
        Analyze the prompt and responses(response_a, response_b) from two chatbots(model_a, model_b).
        Then predict the human preference of those responses- if it is "winner_model_a", "winner_model_b" or
        "winner_tie". Return the answer as the correspoding preference label "winner_model_a", "winner_model_b" or
        "winner_tie".
        ----------------------------------------------------------------------------------------------------------
        prompt: {train["prompt"].iloc[idx]}
        ----------------------------------------------------------------------------------------------------------
        response_a: {train["response_a"].iloc[idx]}
        ----------------------------------------------------------------------------------------------------------
        response_b: {train["response_b"].iloc[idx]}
        ----------------------------------------------------------------------------------------------------------
        Preference=  """.strip()

res = generate_response_for_LMSYS(api_key, all_prompt)
print(res)

```



---

 # Comments from other users

> ## Valentin Werner
> 
> What was your idea behind this approach?
> 
> At first it seems logical to try this with text generation, apart from the downfall of generation speed, which is way slower than sequence classification. However, you dont want to classify a winner, but probabilities - so every misclassification hurts so much more. 
> 
> I think its pretty interesting to see that GPT-4o with Reasoning does not necessarily outperform / is on-par with a properly finetuned deberta3base 
> 
> 
> 
> > ## suguuuuuTopic Author
> > 
> > Thanks for your comments!
> > 
> > I am going to implement DeBERTa or LLaMA3 as an auxiliary loss. 
> > 
> > The reason is that I hypothesized this will enable the model itself to score based on the Criteria and Categories of the text, ultimately having a positive impact on performance.
> > 
> > I came up with this idea from this discussion. I thought that performance might improve by making this more detailed.
> > 
> > [https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/499756](https://www.kaggle.com/competitions/lmsys-chatbot-arena/discussion/499756)
> > 
> > I'll skip the explanation of the effects of AuxLoss, as it's used in other Kaggle competitions as well.
> > 
> > e.g. [https://www.kaggle.com/competitions/rsna-breast-cancer-detection/leaderboard](https://www.kaggle.com/competitions/rsna-breast-cancer-detection/leaderboard)
> > 
> > I was preparing to do labeling using ChatGPT.
> > 
> > 
> > 
> > > ## nahyat
> > > 
> > > I've learned a lot from this. Thank you.
> > > 
> > > You said that you use Llama3 or Deberta as auxiliary loss, but does auxiliary loss mean that you obtain the output of the main task and the output of the subtask from a single model by branching and use them for the loss?
> > > 
> > > I would appreciate it if you could let me know if you could share your thought and ideas.
> > > 
> > > 
> > > 
> > > ## suguuuuuTopic Author
> > > 
> > > Yes, at first, I was going to use subtask as you said.
> > > 
> > > My just idea, It would be interesting to use the subtask prediction results and lightgbm to predict the final results.
> > > 
> > > 
> > > 


---

> ## suguuuuuTopic Author
> 
> I uploaded results of my experiment. It is written in Japanease. 
> 
> [https://www.kaggle.com/datasets/sugupoko/chatbotarena-output-by-gpt4o](https://www.kaggle.com/datasets/sugupoko/chatbotarena-output-by-gpt4o)
> 
> 
> 
> > ## Shota Yamasaki
> > 
> > 有益な情報をありがとうございます！
> > 
> > カテゴリに応じた加重平均スコアに基づいて、さまざまな基準でテキストを比較することは重要だと理解できました。
> > 
> > この実験で得た結果をこの後どう活かすつもりだったのでしょうか？
> > 
> > 非常に興味深いです。
> > 
> > 
> > 
> > > ## suguuuuuTopic Author
> > > 
> > > I wrote it above!
> > > 
> > > 
> > > 


---

