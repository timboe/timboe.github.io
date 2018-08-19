---
layout: post
title: World Cup Monte Carlo - Part 1
feature-img: "img/header_02.jpg"
---

 > Just how sophisticated a model is needed to predict the football?

## Introduction

Back in 2014, one of our more football-interested German post-docs at Warwick, Michel, had the idea to run an office World Cup prediction competition on the [kicktipp](https://www.kicktipp.co.uk/) site. Here groups of friends guess the result for every game in the tournament to score points and compete against each other. Getting the exact result nets four points; an otherwise correctly guessed goal difference is worth three points or, lastly, getting at least the correct outcome of the match is worth two points. With World Cups being O(50) matches - this represents a large number of predictions.

Not being particularly football savvy, this made me question what minimal model I could use to make reasonable predictions on my behalf. The raw model I came up with was both basic and quick, being hashed out in a working form over a couple of lunch breaks. It uses *two tunable parameters*: a lower and higher threshold for the **"goaliness"** of a game of World Cup football, these are used in conjunction with a list of World Cup qualified teams - sorted by their [official FIFA ranking](http://www.fifa.com/fifa-world-ranking/ranking-table/men/index.html). First, each completing team gets a goaliness score based on their country's classification with respect to other countries in the tournament and the upper threshold for goaliness. Second, the two team's goaliness scores are renormalised to bring them into the range of regular World Cup matches. Due to the typically small number of goals scored in football matches, [Poissonian statistics](https://en.wikipedia.org/wiki/Poisson_distribution) are then used to generate an integer number of goals scored from each team's goaliness rating.

## Tuning The Model

So at this point, I had a simple model designed to generate results which are typical of World Cup games, it knew of which of the teams were "better" than the other - but still contained a random element, and it had two free parameters to tune to data. The tuning dataset comprised the results of previous World Cup matches, for each match the two recorded quantities were the total number of goals from both teams $$(G_A + G_B)$$ and the goal difference $$abs(G_A - G_B)$$. These let us know "how many goals are there per match" and "how much better is one team than the other" on aggregate.

The fitting procedure varied goaliness between  0.1 - 5.0 in coarse steps of 0.1. 10,000 rounds of the group stages provided the statistics to evaluate each parameter point with the total goals and goal difference for each game recorded. Once normalised, a $$\chi^2$$ test quantifies the agreement of the prediction to the data. Both the total goals and the goal difference have equal weighting, so the algorithm locates the values which minimised the sum of the $$\chi^2$$ of both distributions. A refinement stage repeats the search in a window of $$\pm 0.5$$ around the coarse optimal values, this time using fine steps of 0.01.

Plotted below is the result of the training, here tuned to the results of the 2014 World Cup where we see that a rather narrow goaliness range of **1.52 - 1.79** best matches the data. The data statistics from a single tournament are somewhat sparse, but still large enough to [include interesting outliers](https://en.wikipedia.org/wiki/Brazil_at_the_2014_FIFA_World_Cup#Brazil_vs_Germany). The prediction for total goals is in good agreement with the data, while the prediction for the goal difference is a little over-fitted.  

![Fitted Results]({{ site.baseurl }}/img/WCMC_Tuning_1.png)

## 2014, 2016 And Lessons Learned

Back in 2014, data from past World Cups tuned the first incarnation of Monte Carlo (`WCMC_2014`), and it was at this point that I made a grave error. In the spirit of making interesting predictions (and not in the spirit of the Monte Carlo method) *I ran the tuned model only once*. Every World Cup has some irregularly scoring games, and so did my prediction - but the probability that my guess of which game's score was anomalous would line up with reality was very slim. As a result, `WCMC_2014` did OK, but not great.

In 2016 the UEFA European Championship was held, things went better this time. Rather than taking the results after running `WCMC_2016` only once, **a per match average over multiple thousand trial tournaments gave a more accurate prediction**. This averaging over the ensemble produced much more boring, mundane score predictions but performed significantly better in the competition.

At this stage of its life, `WCMC_2016` could still only predict the outcome of fixed match pairings, meaning that it needed to be updated as the tournament progressed with which teams were playing each other in the later rounds. Kicktipp has a bonus round which allows punters to earn four bonus points each for predicting (before the tournament starts) the winners of each group, the teams reaching the semi-finals and the overall winner. Disregarding these bonus points (which `WCMC_2016` could not offer a prediction for), `WCMC_2016` beat all of its human competitors and **held a clean margin of 13 points to its nearest challenger**.   

## `WCMC_2018`

The same basic underlying model which was knocked together in around two lunch breaks back in 2014 forms the bases for the 2018 variant. The big difference now being that `WCMC_2018` knows how the tournament progression system works, this means that *it can predict how far each team will progress in the tournament, and therefore `WCMC_2018` can also answer the kicktipp bonus questions* this year.

I detail the predictions of `WCMC_2018` below based on 100,000 pseudo-tournaments. To test these predictions against a more informed crowd, **I will be betting £1 on the exact score of all games in the 2018 World Cup** as predicted by `WCMC_2018` and on all of the bonus questions. The predictions for the exact results of knock-out rounds will be evaluated and entered once the teams are known, and a follow-up blog post will contain these numbers, and a debrief on how well or poorly `WCMC_2018` performed against other members of the department and on the Betfair betting exchange.

## The Group Stages

There are eight groups, A-H, each group consists of four countries which play each other round-robin totalling six games per group.

England (tournament rank 12$$^{th}$$) is playing in Group G against Panama (ranked 29$$^{th}$$), Belgium (ranked 3$$^{rd}$$) and Tunisia (ranked 13$$^{th}$$). The 2D distributions below plot the normalised outcome of all 100,000 pseudo-tournaments for each pairing of the teams, **the most likely outcome is the most populous bin of the distribution** as plotted in the figures.

![England's Group Stage]({{ site.baseurl }}/img/WCMC_GroupStage_7.png)

Predictions of this nature are made for all of the groups: [A]({{ site.baseurl }}/img/WCMC_GroupStage_1.png), [B]({{ site.baseurl }}/img/WCMC_GroupStage_2.png), [C]({{ site.baseurl }}/img/WCMC_GroupStage_3.png), [D]({{ site.baseurl }}/img/WCMC_GroupStage_4.png), [E]({{ site.baseurl }}/img/WCMC_GroupStage_5.png), [F]({{ site.baseurl }}/img/WCMC_GroupStage_6.png), [G]({{ site.baseurl }}/img/WCMC_GroupStage_7.png) and [H]({{ site.baseurl }}/img/WCMC_GroupStage_8.png).

FIFA rules dictate that a team scores three points for a win, one for a draw and none for losing. At the end of the group stage, the top two teams of each group progress. Team ranking is judged first on points, then goal difference (total goals scored minus total goals conceded), then the total number of goals scored. If things are still equal at this stage then it [gets a bit more complicated](https://en.wikipedia.org/wiki/2018_FIFA_World_Cup#Group_stage), however, `WCMC_2018` will assume the team with the higher FIFA ranking will progress should everything else be equal.

![Group Stage Outcome]({{ site.baseurl }}/img/WCMC_GroupResults_1.png)

## Knockout stages

Supposing for a second that the World Cup was to be a 32-team round-robin tournament, there would be $$\frac{n}{2}(n-1) = 496$$ games and the winner would be the team to accrue the most points. In a scenario such as this, the probability of each side winning under the `WCMC` model would be directly proportional to the team's rankings in the model. However 496 is a *huge* number of games, the actual world cup consists of only 64 games (48 group stages & 16 knockouts). So, the **makeup of each group can have a significant impact on the chances of individual teams** and this, in turn, has a knock on effect as it **influences the probabilities of different pairings of teams to be brought together in the knockout stages**.

In the following figures, the probability is plotted for each team to progress through the different stages in the tournament. The countries along the bottom are identified by their [ISO Alpha-2 country code](http://www.nationsonline.org/oneworld/country_code_list.htm) and are ordered by the [official FIFA ranking](http://www.fifa.com/fifa-world-ranking/ranking-table/men/index.html) which ranks **Germany** top and **Saudi Arabia** bottom in 32$$^{nd}$$ place (while **Saudi Arabia's** FIFA ranking is currently 67, the classification used here is only with respect to other countries taking part in the tournament).

Straight away we see a shaping of the distribution in that lucky **Uruguay** (ranked 16$$^{th}$$) has an estimated 82% chance to progress from the group stage - the same as **Germany** (ranked 1$$^{st}$$). This is due to **Uruguay** being placed against **Russia** (ranked 31$$^{st}$$), **Saudi Arabia** (ranked 32$$^{nd}$$) and **Egypt** (ranked 26$$^{th}$$). **Egypt** also benefits from being the 2$$^{nd}$$ highest ranked team in this group with its 56% chance to progress being significantly higher than that of **Egypt's** immediate neighbours in the rankings: **Morocco** (24% chance to progress) and **Nigeria** (28% chance to progress). These two teams face much stiffer competition from the likes of **Portugal** and **Argentina**. In the other groups, **Poland** also have a notably higher predicted probability of clearing the group stage than the higher-ranked **Switzerland**, **France** and **Spain**.

![Group Stage Summary]({{ site.baseurl }}/img/WCMC_KnockoutResults_1.png)

Progressing to the round of 16 and focusing on the top of the leader-board, it's **Germany**, **Portugal**, **Argentina**, **Spain** and **Poland** at the high-end who are in the best position to do well. With **Brazil**, **Belgium**, **Switzerland** and **France** most disadvantaged by the draw. This pattern holds into the quarterfinals with **Switzerland** particularly disadvantaged against passing on into the semis. **England** are neither advantaged or disadvantaged by their group placement; a 30% predicted chance of passing the round of 16 and 14% chance of passing the quarterfinals are both in line with **England's** rank of 12$$^{th}$$ in the tournament.   

![Round of 16 Summary]({{ site.baseurl }}/img/WCMC_KnockoutResults_2.png)

![Quarter Finals Summary]({{ site.baseurl }}/img/WCMC_KnockoutResults_3.png)

In the semifinals, **Germany** are clear the favourites to progress to the final. **Poland** manages to keep punching above its weight with a 13% predicted chance of reaching the final which is 5% higher than might otherwise be expected given **Poland's** rank of 9$$^{th}$$.

![Semi Finals Finals Summary]({{ site.baseurl }}/img/WCMC_KnockoutResults_4.png)

Finally: `WCMC_2018` predicts **Germany** will come out on top for the second tournament in a row with a 17% chance of victory, which are odds of roughly one in six. Other likely candidates group into two clusters: **Brazil**, **Belgium**, **Portugal** and **Argentina** all have roughly a 10% chance (one in ten). While **Switzerland**, **France**, **Spain** and **Poland** all have approximately a 5% chance (one in twenty). **England** are not too far behind, at 3% (one in thirty-three).  

![Tournament Final Summary]({{ site.baseurl }}/img/WCMC_KnockoutResults_5.png)

## Bonus - Goals Per Team

One other bonus question asked by [kicktipp](https://www.kicktipp.co.uk/) the team which will produce the highest goal scorer. While not something the `WCMC` can answer directly, **Germany** comes out on top when ranking teams by the average number of goals scored per tournament with a mean of 10.

![Goals Per Team]({{ site.baseurl }}/img/WCMC_Goals_1.png)

## Bonus - How Could England Win?

**England's** first victory occurs in pseudo-tournament 24. Here's how it happened.

| Group A (Uruguy, Saudi Ar.) | Group B (Portugal, IR Iran) | Group C (France, Peru)  | Group D (Argentina, Iceland) |
|-----------------------------|-----------------------------|-------------------------|------------------------------|
| Russia:1 - Saudi Ar.:2      | Portugal:2 - Spain:1        | France:1 - Australia:0  | Argentina:3 - Iceland:0      |
| Russia:0 - Egypt:1          | Portugal:4 - Morocco:0      | France:0 - Peru:2       | Argentina:2 - Croatia:1      |
| Russia:1 - Uruguay:3        | Portugal:0 - IR Iran:0      | France:2 - Denmark:1    | Argentina:1 - Nigeria:1      |
| Saudi Ar.:3 - Egypt:0       | Spain:0 - Morocco:1         | Australia:2 - Peru:0    | Iceland:2 - Croatia:0        |
| Saudi Ar.:0 - Uruguay:4     | Spain:2 - IR Iran:0         | Australia:0 - Denmark:1 | Iceland:3 - Nigeria:2        |
| Egypt:1 - Uruguay:3         | Morocco:1 - IR Iran:4       | Peru:2 - Denmark:2      | Croatia:3 - Nigeria:1        |

**Saudi Arabia** makes it through their easy group, despite being ranked last in the tournament. In a more substantial upset, **Spain** loose to **Morocco** meaning that **IR Iran** make it through Group B.

| Group E (Brazil, Switzerland) | Group F (Korea Rp., Mexico) | Group G (England, Belgium) | Group H (Senegal, Poland) |
|-------------------------------|-----------------------------|----------------------------|---------------------------|
| Brazil:4 - Switzerland:1      | Germany:0 - Mexico:1        | Belgium:0 - Panama:0       | Japan:1 - Senegal:3       |
| Brazil:4 - Costa Rica:0       | Germany:2 - Sweden:1        | Belgium:1 - Tunisia:1      | Japan:1 - Colombia:1      |
| Brazil:1 - Serbia:1           | Germany:1 - Korea Rp.:1     | Belgium:3 - England:2      | Japan:1 - Poland:4        |
| Switzerland:2 - Costa Rica:0  | Mexico:1 - Sweden:0         | Panama:1 - Tunisia:2       | Senegal:2 - Colombia:0    |
| Switzerland:4 - Serbia:3      | Mexico:0 - Korea Rp.:2      | Panama:1 - England:3       | Senegal:1 - Poland:1      |
| Costa Rica:0 - Serbia:0       | Sweden:0 - Korea Rp.:1      | Tunisia:0 - England:1      | Colombia:4 - Poland:0     |

In the second set of groups, the defending champions **Germany** make a shock exit following a win over **Sweden** and a draw against the **Korean Republic** which was insufficient to save them with the **Korean Republic** and **Mexico** both going through with two wins apiece. **England** win two of their games to progress as the leaders of group G.

| Round | Score                       | Winner    |
|-------|-----------------------------|-----------|
| 16    | Uruguay:2 - IR Iran:2       | Uruguay   |
| 16    | France:0 - Iceland:2        | Iceland   |
| 16    | Saudi Ar.:0 - Portugal:1    | Portugal  |
| 16    | Peru:1 - Argentina:0        | Peru      |
| 16    | Brazil:3 - Mexico:2         | Brazil    |
| 16    | England:1 - Poland:0        | England   |
| 16    | Switzerland:1 - Korea Rp.:1 | Korea Rp. |
| 16    | Belgium:2 - Senegal:2       | Senegal   |

**Iceland** knock out **France** and the **Korean Republic** manages to eliminate **Switzerland** on goal difference due to **Switzerland's** poor showing against **Brazil** in the group rounds. As a side note, draws in the knockout round should be settled by penalty shoot-out but this is not implemented in `WCMC_2018`, neither is any consideration of overtime, maybe next time. **Belgium** draw with **Senegal** but get eliminated on goal difference.

| Round | Score                    | Winner    |
|-------|--------------------------|-----------|
| QF    | Uruguay:2 - Iceland:2    | Uruguay   |
| QF    | Brazil:1 - England:3     | England   |
| QF    | Portugal:1 - Peru:4      | Peru      |
| QF    | Korea Rp.:1 - Senegal:4  | Senegal   |

In the quarterfinals, **Uruguay** take out **Iceland** on goal difference while **England** on terrific form beat **Brazil** 3-1. A plucky **Peruvian** national team manage to defeat **Portugal** and **Senegal** also perform well to eliminate the **Korean Republic**.

| Round | Score                    | Winner    |
|-------|--------------------------|-----------|
| SF    | Uruguay:1 - England:1    | England   |
| SF    | Peru:0 - Senegal:1       | Senegal   |
| F     | England:4 - Senegal:0    | England   |

**Senegal** make it past the quarterfinals for the first time in their history to come against **England** who are now in their second ever World Cup final. **England** easily outclasses the **Senegalese** team to bank their second world cup victory.

## Source Code

`WCMC` the World Cup Monte Carlo is written in `C++` and uses the [ROOT library](https://root.cern.ch/) for plotting. 100,000 pseudo-tournaments run in less than 30 seconds.

[WCMC on Github](https://github.com/timboe/WCMC){: .button}
