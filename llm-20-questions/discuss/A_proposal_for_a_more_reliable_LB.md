# A proposal for a more reliable LB

**c-number** *Wed Jul 31 2024 23:49:37 GMT+0900 (日本標準時)* (10 votes)

Many participants have pointed out that there's too much of a luck factor in the current LB because wins and losses are heavily dependent on teammates' abilities.

While ratings might converge given an infinite number of games, realistically, we're dealing with a finite number. Looking at [my submissions](https://www.kaggle.com/competitions/llm-20-questions/discussion/520928#2942026), it's unlikely to converge at all in two weeks, at least with the current number of matches.

Additionally, for players with similar abilities, the final result will be heavily influenced by luck (e.g., getting paired with a high- or low-ranked player) in the final few games.

To overcome this problem or at least reduce the dependence on luck, I propose introducing the following two types of games:

2 Guessers, 1 Answerer: Three players are in a game, with two guessers paired with the same answerer. The outcome will depend solely on the guessers' abilities. Only the guessers' ratings will be updated.

2 Answerers, 1 Guesser: Three players are in a game, with two answerers paired with the same guesser. The outcome will depend solely on the answerers' abilities. Only the answerers' ratings will be updated.

In both game types, ratings can be updated using the normal Elo rating system.

This approach not only reduces the luck factor but also addresses the "pit of dumbness" problem by allowing lower-ranked players to be paired with higher-ranked players more frequently (with no risk of losing rates for the high-ranked players).

I understand that changing the ranking system at this stage is technically challenging and may be unfavorable for some participants who rely on luck. However, I believe this change would benefit many others and make the competition's leaderboard more stable and reliable.

I hope the Kaggle staff will consider this proposal.

[@bovard](https://www.kaggle.com/bovard)



---

 # Comments from other users

> ## Kha Vo
> 
> Your ideas are great indeed!
> 
> However, I prefer no other competition rule change. It's nearly the end and many of us don't want to deal with some major disruption via this critical time, including moving the submission deadline. (but extending post final evaluation period is a good idea)
> 
> 
> 


---

> ## gguillard
> 
> The simplest solution regarding teams pairing would be to pair all guessers against the same official answerer bot.
> 
> Although it was very fun to randomly pair teams, it's now clear that it only leads to a large scoring injustice because of dummy bots.
> 
> On the other hand, the answerer bot is straightforward to implement, and there's no challenge here.  We could even develop an open source official answerer in a collaborative way.
> 
> Finally, if the hosts still want to assess that each team has a valid answerer bot, it is also straightforward to test, as a single game with yes/no questions is needed.
> 
> 
> 
> > ## loh-maa
> > 
> > This would be a different game rather than a solution. All the effort would focus on the single answering reference bot. Less fun I think.
> > 
> > 
> > 
> > > ## gguillard
> > > 
> > > 
> > > All the effort would focus on the single answering reference bot.
> > > 
> > > What do you mean ?  AFAIK there is only a single right answer to each question between yes or no, no strategy to counter a yesbot or a nobot besides throwing random guesses, and no strategy to recover from several wrong answers…
> > > 
> > > 
> > > 


---

> ## loh-maa
> 
> In my opinion, if I may, we may assume the current ranking algorithm is temporarily modified and in the final stage it's going to keep evaluating all agents regardless of their score, so this will largely improve the convergence. I think the suggestions are very interesting, but it is already late, indeed. Stability is important, too. Personally I definitely would not appreciate such last minute changes in any competition, even if they were considered good ideas.
> 
> 
> 


---

