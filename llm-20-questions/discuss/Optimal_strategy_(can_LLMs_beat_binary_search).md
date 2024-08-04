# Optimal strategy (can LLMs beat binary search?)

**Khoi Nguyen** *Fri May 17 2024 21:29:31 GMT+0900 (日本標準時)* (8 votes)

Just a thought experiment. I'm not an expert on this game but from what I gathered, it looks like the optimal strategy when you have a finite pool of possible answers, assuming the correct answer is completely random, is to attempt to divide the remaining pool by half with each of your question.

Now in order to get a near perfect split while being sure that the answer agent did not hallucinate the result, a rule based approach like this is the best:

- Ask: Is the answer in this list <answer pool>, if answer is no, fallback to freestyle mode and pray to LLM god.

If answer is yes:

- Ask: Is the answer in this list <insert half of the remaining answer pool>

- Get a yes/no answer, this is guaranteed to be correct if everyone complies and use a specific asking syntax.

- Repeat from step 2 until there is only one answer left.

Looking at the keywords.py file, we can definitely crawl a large pool of possible countries, cities and landmarks for the private test. (if the landmark is too obscure for crawling I doubt the LLMs have enough information about it to guess anyway)

What edge do LLMs offer over this approach? I mean if the answer was chosen by a known LLM then it's prior knowledge that we can exploit, but when its completely random? 

citation that Gemini gave me: [https://www.cns.nyu.edu/~reuben/blog/20-questions-info-theory/](https://www.cns.nyu.edu/~reuben/blog/20-questions-info-theory/)

Note: Even when if the answer pool is non-crawlable or quasi-infinite (all possible English words), this is still a strong approach, just ask for stuff like: Is the first character of that word in this list […] or something.



---

 # Comments from other users

> ## Bovard Doerschuk-Tiberi
> 
> The list of possible words will change after the final submission deadline (meaning you won't be able to update your agent with the new list). I would strongly advise against any strategies that hard code in the list of possible words.
> 
> Final Evaluation
> 
>   At the submission deadline on August 13, 2024, submissions will be locked. From August 13, 2024 to August 27th, 2024 we will continue to run episodes against a new set of unpublished, secret words. At the conclusion of this period, the leaderboard is final.
> 
> 
> 


---

> ## chris
> 
> I had a similar thought. You do only get 2000 characters in your question (which means you can't really ask a question like "Is the answer in this list", but it does seem like a good approach to have some fixed list of possible values and do some kind of binary search.
> 
> 2^20 = 1,048,576
> 
> So if you hit every split exactly 50% then you could go through a list of ~1M things
> 
> If you use that approach though, you'd better hope that the thing is in your list! So it might be tricky if we're not given more information about the types of words in the private set.
> 
> EDIT: oh, I guess you have to use one guess to actually guess the word, right? So in that case you only get 2^19 = 524,288 max words.
> 
> 
> 
> > ## Khoi NguyenTopic Author
> > 
> > If no information are given about the words in the private set is it even possible to guess it? If the binary search method works perfectly like you said we can only narrow the search space down 2^19 times, anything beyond that is pure luck based.
> > 
> > 
> > 
> > > ## chris
> > > 
> > > There are ~90,000 nouns in english, but presumably they wouldn't use that full list but just pull from the top N most common.
> > > 
> > > There are far more individual places and people, but again, I would presume they would only pull the top N most famous of each.
> > > 
> > > So to solve the problem this way, the trick may just be where you do a cutoff.
> > > 
> > > 
> > > 
> > > ## Khoi NguyenTopic Author
> > > 
> > > Yeah top N most popular things is a fine assumption, so it's a risk vs reward thing in the private set when you either want to guess things faster or have higher chance for a successful guess and who have the N closest to the hosts' wins?
> > > 
> > > 
> > > 


---

> ## G John Rao
> 
> "Ask: Is the answer in this list , if answer is no, fallback to freestyle mode and pray to LLM god."
> 
> I don't think this is exactly what this competition is about. 
> 
> From the overview:
> 
> This competition will evaluate LLMs on key skills like deductive reasoning, efficient information gathering through targeted questioning, and collaboration between paired agents. It also presents a constrained setting requiring creativity and strategy with a limited number of guesses. Success will demonstrate LLMs' capacity for not just answering questions, but also asking insightful questions, performing logical inference, and quickly narrowing down possibilities.
> 
> The keywords.py contains 3 categories: country, city, landmark
> 
> I don't think the categories are limited to those 3, if that's the case, the competition is no fun. 
> 
> The starter notebook has a system prompt:
> 
> system_prompt = "You are an AI assistant designed to play the 20 Questions game. In this game, the Answerer thinks of a keyword and responds to yes-or-no questions by the Questioner. The keyword is a specific person, place, or thing."
> 
> For person and place one can make a list, I don't think it's worth it to make a list for "thing". Because a "thing" can be anything really. It can be a noun, a concept, an object, an idea, a feeling, or even an abstract entity. I think that's where the fun is, and that's where the LLMs come into play. 
> 
> "What edge do LLMs offer over this approach? I mean if the answer was chosen by a known LLM then it's prior knowledge that we can exploit, but when its completely random?"
> 
> I think the secret word has to be random. And all the participants work it to eliminate the randomness with each question. 
> 
> But my only question remains is: What if the opponent answerer straight up denies and lies or in someway lacks understanding of the questioner LLM? Or starts hallucinating?
> 
> If the answerer LLM is from the hosts, it would have been equal grounds for all questioner LLMs. If not, the power is shifted a lot towards the answerer LLM. 
> 
> Maybe we will have more clarity later on
> 
> 
> 
> > ## Khoi NguyenTopic Author
> > 
> > I mean "specific person, place, or thing" may as well mean "any arbitrary thing", you will need some prior knowledge to narrow it down somehow.
> > 
> > 
> > 
> > > ## G John Rao
> > > 
> > > And we do that by crafting our first question. After we get answer to our first question, the secret won't be as arbitrary as it began with. 
> > > 
> > > 
> > > 


---

