# Dear Yes/No bot contributors...

**Matthew S Farmer** *Tue Jul 09 2024 00:18:52 GMT+0900 (日本標準時)* (6 votes)

Please update your answerer agent to be at least as good as the public answerer agent [published by the Rigging Team](https://www.kaggle.com/code/robikscube/phi3-intro-to-rigging-for-llm-20-questions?kernelSessionId=185594599). Simple yes/no bots are making robust question/guess agents suffer. It will help the competition tremendously. Of course, you'll need to update some of the code to make it work in your script.

```
async def answer(base: rg.ChatPipeline, observation: Observation) -> t.Literal["yes", "no"]:
    if not observation.keyword:
        print("Keyword wasn't provided to answerer", file=sys.stderr)
        return "yes" # override until keyword bug is fixed.

    last_question = observation.questions[-1]

    try:
        responses = []
        for i in range(5):
            # Loop 5 times and take the most frequent response
            chat = await (
                base.fork(
#                     f"""\
#                         20 Questions game. Answer yes/no for this keyword: [{observation.keyword}]

#                             Question: {last_question}

#                             Rules:
#                             1. Only consider [{observation.keyword}]
#                             2. Check each letter for letter questions
#                             3. Answer only yes or no

#                             Format:
#                             <answer>yes</answer>
#                             OR
#                             <answer>no</answer>

#                             Your answer:
#                         """
                    f"""
                    Keyword: [{observation.keyword}]

                    Q: {last_question}

                    Answer yes or no in Format: <answer>yes</answer> OR <answer>no</answer>
                    """
                )
                .until_parsed_as(Answer, attempt_recovery=True, max_rounds=20)
                .run()
            )
            responses.append(chat.last.parse(Answer).content.strip('*'))

        print(f'Responses are {responses}')
        return pd.Series(responses).value_counts().index[0]
    except rg.error.MessagesExhaustedMaxRoundsError:
        print('%%%%%%%%%%%% Error so answering yes %%%%%%%%%%%% ')
        return 'yes'

```



---

 # Comments from other users

> ## OminousDude
> 
> I also believe that most lower-level players in this competition should do something like this. However, in my testing, this does not help much because most bots will answer the same thing and it is unlikely to help much. More important is to use a good answerer bot and of the top model choices I believe that Llama 3 is the best answerer all around. So please if you are not consistently in the top ~100 (or even if you are) use Llama 3. It is by far the easiest to work with as it has the highest IF-Eval score.
> 
> *IF-Eval score is how well the model is at following instructions and it makes it so that your agent can have very rigorous prompt engineering.
> 
> ** [LLM Leaderboard use IF-Eval score](https://huggingface.co/spaces/open-llm-leaderboard/open_llm_leaderboard)
> 
> P.S.: I am seriously considering releasing my code because the dumb bots (no offense to you guys) are making me lose my mind
> 
> 
> 
> > ## Matthew S FarmerTopic Author
> > 
> > Agreed. Great point.
> > 
> >  I've been considering releasing some earlier code as well. 
> > 
> > 
> > 
> > > ## OminousDude
> > > 
> > > Same as my thinking. I am just so tired of seeing stuff like this
> > > 
> > > Question: "Is the keyword a thing/object or place/location" Answer: "no"
> > > 
> > > 
> > > 


---

> ## JK-Piece
> 
> Moreover, some people write their agents in a way that they as the wrong questions. This makes good models fail as well
> 
> 
> 


---

