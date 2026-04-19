---
layout: post
title: NCAA Basketball Transitive National Champions
date: 2026-04-19 00:00:00-0000
description: Finding all of the NCAA basketball transitive champions
tags: data
categories: data
related_posts: false
pretty_table: true
---

Every once in a while I'll see a post on Reddit asking a data-related question and think: "I bet I could find an answer to that." This is one of those times. I saw [this post](https://www.reddit.com/r/CollegeBasketball/comments/1sg35e1/how_is_your_school_the_national_champion_by/) on the college basketball subreddit asking how one's school is the national champion by transitive property. I figured that if you could do that for one school, it isn't very hard to do that for every school. So I did.

I pulled [game data](https://www.sports-reference.com/cbb/boxscores/) for every college basketball game in the 2025-26 season to find the winner and loser of every matchup. Then, with the fun of directed graphs, I found every team's shortest path to a national championship by transitive property. Full code is [here](https://github.com/SBroecker/transitive_national_champions). As a practical note, I'm including all games when constructing these graphs, including postseason ones. If the game happened between November 11th, 2025 and April 7th, 2026, it got included.

On the men's side, these are all the schools that can claim a transitive national championship and their shortest path to do so. 370 teams, excluding Michigan, can claim one. North Greenville has the claim on the longest shortest path with seven steps.

As an example for how to interpret the _Transitive Champion Path_ column, "Virginia->Ohio State->Wisconsin->Michigan" means: "Virginia beat Ohio State, who beat Wisconsin, who beat Michigan." Since there are three steps from Virginia to Michigan in that example, the _Path Length_ is three.

<style>
  .transitive-table-wrap {
    width: min(80vw, 50rem); /* 1vw = 1% browser width, rem * fontsize = pixel width */
    margin: 0 auto 1.5rem auto; /* adds space below each table block */
  }
</style>

<div class="transitive-table-wrap">
  <input
    id="mens-team-search"
    class="form-control form-control-sm mb-2"
    type="search"
    placeholder="Search men's teams..."
    aria-label="Search men's teams"
  >

  <div class="table-responsive" style="max-height: 70vh; overflow-y: auto;">
    <table
      class="table table-sm table-striped"
      data-search="true"
      data-search-selector="#mens-team-search"
      data-search-highlight="true"
      data-search-align="left"
    >
      <thead>
        <tr>
          <th data-field="team" data-searchable="true">Team</th>
          <th data-field="path" data-searchable="false">Transitive Champion Path</th>
          <th data-field="distance" data-searchable="false">Path Length</th>
        </tr>
      </thead>
      <tbody>
        {% for row in site.data.shortest_paths_to_michigan %}
        <tr>
          <td>{{ row.team }}</td>
          <td>{{ row.path }}</td>
          <td>{{ row.distance }}</td>
        </tr>
        {% endfor %}
      </tbody>
    </table>
  </div>
</div>

On the women's side, these are all of the transitive champions and their paths. Only 369 teams, excluding UCLA, can claim a national championship. There are eight teams that are tied for having the longest shortest path to a national championship with nine steps.

<div class="transitive-table-wrap">
  <input
    id="womens-team-search"
    class="form-control form-control-sm mb-2"
    type="search"
    placeholder="Search wommen's teams..."
    aria-label="Search wommen's teams"
  >

  <div class="table-responsive" style="max-height: 70vh; overflow-y: auto;">
    <table
      class="table table-sm table-striped"
      data-search="true"
      data-search-selector="#womens-team-search"
      data-search-highlight="true"
      data-search-align="left"
    >
      <thead>
        <tr>
          <th data-field="team" data-searchable="true">Team</th>
          <th data-field="path" data-searchable="false">Transitive Champion Path</th>
          <th data-field="distance" data-searchable="false">Path Length</th>
        </tr>
      </thead>
      <tbody>
        {% for row in site.data.shortest_paths_to_ucla %}
        <tr>
          <td>{{ row.team }}</td>
          <td>{{ row.path }}</td>
          <td>{{ row.distance }}</td>
        </tr>
        {% endfor %}
      </tbody>
    </table>
  </div>
</div>

Since I used network to find these paths, it's relatively straightforward to visualize all of the transitive champions as graphs. On the men's side the graph gets pretty out of hand after three steps, so here are all of the champions with a path of three or fewer steps, colored by their distance to Michigan.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0 text-center">
        {% include figure.liquid loading="eager" path="assets/blogs/mens_transitive_graph.png" class="img-fluid rounded z-depth-1 w-75" %}
    </div>
</div>
<div class="caption">
    <div class="caption"> Colors: reddish orange=nation champion, pale orange=one step removed, greenish beige=two steps, foam green=three steps. As a side note for anyone that wants to fall down this rabbit hole, <a href="https://stackoverflow.com/questions/22408237/named-colors-in-matplotlib">this is some more information on where those color names came from</a>. </div>.
</div>

The top teams tend to lose fewer games on the women's side, so you can get to four steps before things get messy. Here's what the graph looks like for teams that have four or fewer steps to a win over UCLA, colored by distance.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0 text-center">
        {% include figure.liquid loading="eager" path="assets/blogs/womens_transitive_graph.png" class="img-fluid rounded z-depth-1 w-75" %}
    </div>
</div>
<div class="caption">
    Colors: reddish orange=nation champion, pastel orange=one step removed, sand=two steps, pistachio=three steps, foam green=four steps.
</div>

Conveniently, the threshold for both the men's and the women's graph is right where Virginia enters the picture (literally). How nice.
