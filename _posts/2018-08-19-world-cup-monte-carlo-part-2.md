---
layout: post
title: World Cup Monte Carlo - Part 2
feature-img: "img/header_08.jpg"
---

 > A data-driven debrief.


This is a follow on post from  [Part 1]({{ site.baseurl }}{% post_url 2018-05-20-world-cup-monte-carlo-part-1 %}).

## The Tournament

2018's World Cup turned out to be very interesting from a dramatic-games perspective. But, given the aim of this exercise was to predict the outcome, 'interesting' is not necessarily a good thing. There are two elements of the predictions to explore, the game-by-game predictions and the overall tournament progression.

## Goal and Goal Difference Distributions

Comparing the 2018 tournament data with the 2014 data and the model tuned to it, we see overall a good agreement between the datasets. This is promising and means that in future they can be combined to reduce the somewhat large statistical errors, which will more stringently test if `WCMC` possesses enough freedom to describe all the features of the data. The best-combined fit to the 2014 dataset had a $$\chi^2$$ of 0.82 per degree of freedom. The same tune, when compared to the 2018 dataset, yield a poorer fit of 1.42. But given the uncertainties on the data, not much more can be concluded.

While there were two games with 7 goals in 2018, there were actually more high-scoring games in 2014. A discrepancy is, however, observed in the zero-goals bin, goalless draws were significantly rarer in 2018, down from 10% in 2014 to 2% in 2018. This was no doubt a critical factor in the perceived excitement of the tournament.

![Fitted Results Including 2018 Data]({{ site.baseurl }}/img/WCMC_Tuning_2018.png)

## Individual Game Results

There were 64 games in the tournament, for each match the results of all 100,000 trial tournaments were plotted on a 2D distribution and the most populous bin identified as the most likely outcome. A £1 bet was placed on the Betfair sports-book backing the predicted score in each game. Ideally I would have liked to use Betfair's exchange where members bet against each other, however here the minimum bet there was £2.

If we assume the existence of such thing as the 'real probability' for a given outcome in a match, then Betfair's job as a bookmaker is to compete with me to estimate this number as accurately as possible. While my input data is relatively simple, they will be using all sorts of sophisticated input data.

However, Betfair doesn't want to offer their calculated odds to me. If they did this and they were correct, then they would not make any profit. Instead, they should offer me worse odds - but not too much worse, or I would go to a rival bookmaker. 

Of the 64 games, 11 had their exact score predicted correctly, winning £73.50. Taking off the £64 used to place the bets, this leaves £9.50 of profit, great! But how great? We can estimate this by running $$100\times 10^{6}$$ toy betting rounds using the odds given by Betfair, these ranged from 4.5 to 12.0 as seen in the figure below. The return is plotted on a graph under three scenarios: Betfair's odds are fair, and I should expect to draw even (even if guessing randomly); Betfair's odds are unfair, and I should expect to lose on average, or, Betfair's odds are generous (or, miscalculated) and I should expect to make a profit. For the unfair scenario, the underlying odds are increased by 20%, and for generous decreased by 20%, this only affects the chance of the bet to win - not the subsequent payout.

An interesting structure is seen for small returns, driven by the distribution of odds. If only a small number of games are won in a given toy betting round, then some values of total winnings are more likely than others, just like 7 is the most likely outcome of two dice. This effect is washed out by the larger combinatorics as the winnings grow. Correctly fitting these distributions would probably require the sum of a Gaussian with a cosine modulated by a falling exponential to model the peaks at low values. However a regular Gaussian is used here as we only really care about the width, this does an OK job.  

The results of the fit are:

| Odds      | Mean $$(\mu)$$      | Width $$(\sigma)$$ | Significance of £73.50 Return     |
|---------------------------------|--------------------|-----------------------------------|
| Unfair    | £$$52.98 \pm 0.02$$ | £$$19.40 \pm 0.01$$ | $$1.06$$                          |
| Fair      | £$$63.74 \pm 0.02$$ | £$$20.61 \pm 0.01$$ | $$0.47$$                          |
| Generous  | £$$80.23 \pm 0.02$$ | £$$22.03 \pm 0.01$$ | $$-0.31$$                         |

Taking the Unfair scenario as the most likely then the upward fluctuation is only $$1.06\sigma$$ which is well within the bounds of random chance. So given the outcome of the 2018 tournament, we do not have enough data to tell if the simple `WCMC` model is doing any better than random chance. More data is needed from more tournaments.  

![Odds Distribution]({{ site.baseurl }}/img/WCMC_toyBets_1.png)

## Input Rankings

The second input the `WCMC` model uses to make predictions is the ranking of all the teams in the tournament. The percentage probability of winning at the start of the competition are compared using the FIFA rankings from before and after the tournament, there are some significant differences. 

With the updated rankings, 3$$^\textrm{rd}$$ place Belgium gets the best odds at 15%, with the ultimate winners France next at 13%. England increased from 3% to 8%. 

This all goes to indicate that FIFA rankings might not be the best choice of data to base the next round of predictions on.

Using FIFA Rankings from before the World Cup.
![Winner Prediction]({{ site.baseurl }}/img/WCMC_KnockoutResults_5.png)

Using FIFA Rankings from after the World Cup.
![Winner Prediction]({{ site.baseurl }}/img/WCMC_KnockoutResults_Mode0_5_Updated.png)


## Tournament Progression

The model was re-run after each stage of the tournament to update the probabilities and generate the most probable scores for the next round of bets.

Germany exiting as last in Group F was a significant upset. `WCMC` gave this a 5% chance, and with a World Cup every four years that is an 80 year return period. It has been 84 years since Germany started playing in one form or another in 1932 and this is their first exit in the groups. Or to put it another way, if you look at enough individual statistics, you will always find at least one 'once in a century' event. 

After the group stage, `WCMC` most favoured Belgium and Switzerland & Spain. France did not have an easy half of the draw from this point.

![After group stage]({{ site.baseurl }}/img/WCMC_KnockoutResults_Mode1_1.png)

England's easier half shows up clearly when going into the quarterfinals. Going so far as giving them the 2$$^\textrm{nd}$$ highest chance of winning the tournament at this stage (22%), with Brazil at 28%.

![After round of 16]({{ site.baseurl }}/img/WCMC_KnockoutResults_Mode2_1.png)
![After round of 16]({{ site.baseurl }}/img/WCMC_KnockoutResults_Mode2_2.png)

By the semis, there is hardly any freedom left for different paths through the tournament and the results of `WCMC` start reflecting the input FIFA rankings. Belgium was tipped at this point, France's probability was _still_ only at the 20% level even here. 

![After quarter finals]({{ site.baseurl }}/img/WCMC_KnockoutResults_Mode3_1.png)

Only once it came to the finals did France complete their fight out of the difficult half of the draw, with `WCMC` favouring them to win for the first time at 70% based on the difference in FIFA ranking compared to Croatia.

![Ater semi finals]({{ site.baseurl }}/img/WCMC_KnockoutResults_Mode4_1.png)

## Source Code

`WCMC` the World Cup Monte Carlo is written in `C++` and uses the [ROOT library](https://root.cern.ch/) for plotting. 

[WCMC on Github](https://github.com/timboe/WCMC){: .button}
