---
layout: post
title: NBA Teams Represented in the Finals
date: 2025-07-13 00:00:00-0000
description: Double checking a popular stat about the Knicks
tags: data
categories: data
related_posts: false
---

There has been a stat floating around for a few years now claiming that every year of the NBA has featured a Finals with at least one player who's a current, past, or future Knick. [This one](https://www.reddit.com/r/nba/comments/1l3ursw/the_streak_continues_all_75_years_of_the_nba_have/), for example. It seemed rather unlikely to me that the Knicks (NYK) are the _only_ team with a streak like this; "current, past, or future" casts a pretty wide net with the amount of player movement in the NBA, after all. So I decided to figure out if any other teams have a similar streak. 

To do that, I pulled data from [Basketball Reference](https://www.basketball-reference.com/) for every NBA Finals matchup, with the first being in 1950. I gathered the complete rosters for each Finals team, then gathered every franchise each of those players had been on throughout their careers. From there, I could count how many times a player associated with each team had been in the Finals each year. As an example of how this works, if a player was on the Bulls (CHI) in 2012, played in the 2020 Finals with the Heat (MIA), then later joined the Warriors (GSW) in 2025, that 2020 Finals appearance would count toward all three teams' totals.

Full code for everything I did is in [this repo](https://github.com/SBroecker/finals_rosters).

To jump straight to the end, these are the total counts for every current NBA team. There have been 76 NBA Finals in total, with 75 being the most that any team achieved.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0 text-center">
        {% include figure.liquid loading="eager" path="assets/blogs/teams_per_year.png" class="img-fluid rounded z-depth-1 w-75" %}
    </div>
</div>
<div class="caption">
    The total count for each team. This count represents the total number of years that a current, past, or future player of a particular team was in the NBA Finals in any given year. The team abbreviations used here are the abbreviations used by Basketball Reference.
</div>

## Key Takeaways

Here are the main takeaways from the data I put together. 

**The original claim about the Knicks was wrong**. The Knicks have _not_ had a connection to every Finals. They've missed at least one year.

**Two teams are tied for the lead**. The Knicks and the Hawks (ATL) both have connections to 75 Finals appearances.

## Digging Deeper

Tallying up every team's Finals appearances confirmed my suspicion that having a connection to the Finals (almost) every year isn't very rare. Eight teams have a connection to more than 70 of the 76 total Finals. 

However, the more interesting discovery for me was identifying exactly where the Knicks' streak was broken. For that, this might help:

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0 text-center">
        {% include figure.liquid loading="eager" path="assets/blogs/heatmap.png" class="img-fluid rounded z-depth-1 w-75" %}
    </div>
</div>
<div class="caption">
    A heatmap of Finals appearances, where the x-axis is the team, the y-axis is the year, and the color represents whether a player from a team was in the Finals that year.
</div>

1967 for the Knicks should draw your attention. My data indicates that no Knick was in the Finals that year, even though stats cited in the past would say otherwise. Previous lists claim that Art Heyman, a former Knick, played in the Finals in 1967. The [1967 NBA Finals](https://www.basketball-reference.com/playoffs/1967-nba-finals-warriors-vs-76ers.html) was between the 76ers and the Warriors, and Art Heyman [played in the ABA](https://www.basketball-reference.com/players/h/heymaar01.html) that season.

Another thing worth mentioning is the Hawks (ATL). They're sitting on 75 player appearances right now, with the only missed Finals being this year. The stat we're looking at is for current, past, or _future_ players on a team, meaning that if any of the players from the Pacers (IND) or the Thunder (OKC) (this year's Finals teams) ends up on the Hawks at some point in the future, the Hawks will have a perfect streak.

## Notes About the Data

An important thing to note about the final figures I'm using here is that they include every previous iteration of the 30 current NBA teams. The Washington Wizards (WAS), for example, used to be the Chicago Packers (CHP), Chicago Zephyrs (CHZ), Baltimore Bullets (BAL), Capital Bullets (CAP), and Washington Bullets (WSB) before landing on their current iteration, the Washington Wizards. Data for all of those previous versions was folded into the data for the Wizards. Some teams, like the Knicks, have gone by the same name since their founding as NBA teams, so no extra work was needed. [This page](https://www.basketball-reference.com/teams/) is how I tracked the evolution of each team.

I am also only considering _NBA_ Finals in this exercise. Basketball Reference includes Finals stats from other leagues as well, but I limited my data to the NBA. 

## Conclusion

So what does all this data tell us about the original claim that sparked this whole investigation? NBA player movement has created a very well-connected web of connections to the Finals. Even though the Knicks don't have the perfect streak they're often credited with, it's remarkable to me that so many teams almost do. And who knows, maybe the Hawks will earn the elusive perfect streak that everyone thought the Knicks already had. 