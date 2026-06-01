---
layout: post
title: NBA MVP Voting Concentration
date: 2026-05-29 00:00:00-0000
description: Determining whether NBA MVP voting has gotten more concentrated over time
tags: data
categories: data
related_posts: false
pretty_table: true
---

If you've ever needed evidence that people are increasingly living in their own media bubbles, then boy do I have the data for you. I've been seeing people make the claim that voting for the NBA's Most Valuable Player (MVP) award has gotten more concentrated over time because all of the voters live in the same media bubble and are just following what everyone else is doing. While I can't actually make any claims about media diets among NBA MVP voters, I _can_ figure out if MVP voting has gotten more concentrated over time (and really, that's more fun anyway).

To begin with, how does MVP voting work? According to the definitive source on all things, [Wikipedia](https://en.wikipedia.org/wiki/NBA_Most_Valuable_Player), the MVP is selected by a panel of sportswriters and broadcasters. Each panel member casts a ballot that ranks five players, points are given to players based on how they were ranked on ballots, and then the player with the most points wins. Simple enough!

To actually measure how concentrated votes are, we need some metrics. Luckily, people have tried to measure the concentration of data before. The first metric we'll use is the [Herfindahl–Hirschman index (HHI)](https://en.wikipedia.org/wiki/Herfindahl%E2%80%93Hirschman_index), a metric generally used to measure competition in a market by looking at the size of firms in relation their industry. High HHI means more concentration. We're also going to use [Shannon Entropy](https://en.wikipedia.org/wiki/Entropy_(information_theory)), a metric in information theory that measures the "uncertainty" of data. Lower entropy means more concentration. Then, because those are complicated, we're going to look at some simpler metrics as sanity checks. First we'll check how many total players get MVP votes every year (we would expect fewer players to get votes if votes are more concentrated). Then we'll check the total vote share taken up by the top two candidates in a given year, where "vote share" is the percentage of total points that a player gets.

Now, let's look at some data. I pulled MVP voting data from the ever-trusty [Basketball Reference](https://www.basketball-reference.com/awards/awards_2026.html) for every year starting in 1981, the first year where the current MVP selection format was used. You can see all the code I used in [this repo](https://github.com/SBroecker/nba_mvp_voting). To start, let's look at the HHI per year.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0 text-center">
        {% include figure.liquid loading="eager" path="assets/blogs/hhi.png" class="img-fluid rounded z-depth-1 w-75" %}
    </div>
</div>
<div class="caption">
    Vote concentration per year, as measured by HHI. Blue points are true values and the dashed orange line is the line of best fit as calculated by linear regression. 
</div>

What do we see? Concentration is going up! There's been a steady rise in vote concentration as measured by HHI.

As a side note: since HHI is sometimes used to measure the concentration of firms in antitrust, we can pretend that MVP candidates are firms and decide if they are a monopoly. Going back to our trusty Wikipedia, HHI values above 0.25 are generally considered to indicate that a market is highly concentrated. From the plot we can see that the last few years are starting to get into this anti-competitive territory, and thus we can conclude that NBA candidates are, in fact, a monopoly.

What about entropy?

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0 text-center">
        {% include figure.liquid loading="eager" path="assets/blogs/shannon_entropy.png" class="img-fluid rounded z-depth-1 w-75" %}
    </div>
</div>
<div class="caption">
    Vote concentration per year, as measured by Shannon Entropy. The lines and colors mean the same as above.
</div>

Entropy is going down, which means concentration is going up! More evidence to support the theory. What about the "simpler" metrics?

<div class="row mt-3">
    <div class="col-12 col-md-6 mt-3 mt-md-0 text-center">
        {% include figure.liquid loading="eager" path="assets/blogs/top_2_share.png" class="img-fluid rounded z-depth-1 w-100" caption="The share of MVP votes going to the top two candidates, as a percent of overall MVP votes. The lines and colors mean the same as above." %}
    </div>
    <div class="col-12 col-md-6 mt-3 mt-md-0 text-center">
        {% include figure.liquid loading="eager" path="assets/blogs/number_candidates.png" class="img-fluid rounded z-depth-1 w-100" caption="The total number of players receiving MVP votes. The lines and colors mean the same as above." %}
    </div>
</div>

The simple metrics tell the same story! The share of votes going to the top two candidates has been going up and the size of the overall pool of candidates receiving votes is going down.

This feels like pretty solid evidence that the MVP voting body has gotten more homogenous in their opinions over the years. It also got me thinking: does that homogeneity extend to other voting categories? We can look at HHI per year for Rookie of the Year (ROY) and Coach of the Year (COY) to get an idea.

<div class="row mt-3">
    <div class="col-12 col-md-6 mt-3 mt-md-0 text-center">
        {% include figure.liquid loading="eager" path="assets/blogs/hhi_roy.png" class="img-fluid rounded z-depth-1 w-100" caption="Vote concentration per year for Rookie of the Year voting, as measured by HHI" %}
    </div>
    <div class="col-12 col-md-6 mt-3 mt-md-0 text-center">
        {% include figure.liquid loading="eager" path="assets/blogs/hhi_coy.png" class="img-fluid rounded z-depth-1 w-100" caption="Vote concentration per year for Coach of the Year voting, as measured by HHI." %}
    </div>
</div>

Turns out: maybe? The picture here is much less clear. It looks like before about 2000 voting was erratically homogenous before settling into a more predictable trend. Now it seems like candidate concentration is slowly rising in both cases. One thing to note here is that the scale for HHI is much different in all three HHI plots. MVP HHI was about 0.25 in 2026, ROY HHI was 0.41, and COY HHI was 0.31. Could I rescale the images to make the comparison easier? Yes. Will I? No.

Going back to our original question then about whether MVP voting has gotten more concentrated, what can we conclude? I think it's safe to say that yes, based on all of the metrics we tested, voting appears to be getting more concentrated. And, since that conclusion feels too scientific and narrow, I'm also going to conclude, based on no evidence, that the reason is because of media bubbles. Take that, science.