---
layout: default
title: Analysis
---

<div class="row row-cols-1">

<div class="col mb-4">
<div class="card shadow" data-aos="fade-up">
<div class="content p-4" markdown="1">

#### A quick word about articles!

As we said in the introduction, we want to associate each article to a country. But why does this actually make sense? Well, if we look at the two graphs below, we can see that almost all atricles among the top 20 can be associated to a country (*e.g. English_language to England*). The same is true for the bottom 20 articles (*e.g. Afghan hound to Afghanistan*). 

This motivates our decision to analyse the distributions of those countries within the Wikipedia graph. In the end, we are interested in whether players of the Wikispeedia game really tend to click more on articles that are associated with western countries or if this feature is due to the properties of the Wikipedia graph itself. 

</div>
</div>
</div>

<div class="col mb-4">
<div class="card shadow" data-aos="fade-up">
<div class="content">
<div id="carouselWorld" class="carousel slide" data-bs-theme="dark">
  <div class="carousel-inner">
    <div class="carousel-item active">
      <div class="graph-title"> Figure 1: Connectivity of most clicked articles </div>
      <iframe class="graph" src="{{ 'graphs/topic_1/most_used_articles_graph.html' | relative_url }}" ></iframe>
    </div>
    <div class="carousel-item">
      <div class="graph-title"> Figure 2: Connectivity of least clicked articles </div>
      <iframe class="graph" src="{{ 'graphs/topic_1/least_used_articles_graph.html' | relative_url }}" ></iframe>
    </div>
  </div>
  <button class="carousel-control-prev" type="button" data-bs-target="#carouselWorld" data-bs-slide="prev">
    <span class="carousel-control-prev-icon" aria-hidden="true"></span>
    <span class="visually-hidden">Previous</span>
  </button>
  <button class="carousel-control-next" type="button" data-bs-target="#carouselWorld" data-bs-slide="next">
    <span class="carousel-control-next-icon" aria-hidden="true"></span>
    <span class="visually-hidden">Next</span>
  </button>
</div>
</div>
</div>
</div>

<div class="col mb-4">
<div class="card shadow" data-aos="fade-up">
<div class="content p-4" markdown="1">

#### Which countries are most represented in the Wikipedia graph?

Now that all (most) articles are associated to a country, we can look at the distribution of those countries. Is there a country that is associated to more articles? (we have our little idea haha but let's check). 

We see that 8 countries make up for <sup>1</sup>/<sub>2</sub> of the articles in Wikipedia, namely the **US**, **UK**, **Australia**, **France**, **Germany**, **Italy**, **India** and **China**. Those are all in the top 10 of countries that publish the most!!

With *Figure 2*, we get a first intuition of the cultural bias that is present in the Wikipeedia graph: countries that publish most are also represented by more articles. When players play on this already biased graph, they will obviously click most on articles from those countries. So, later, when we analyze the behavior of the players, we will have to keep this in mind and normalize the click counts of the players by the number of articles per country! But this is for later, let's go on here!

</div>
</div>
</div>


<div class="col mb-4" id="plot1">
  <div class="card shadow" data-aos="fade-up">
    <div class="content p-4">
      <div class="graph-title"> Figure 2: Proportion of articles per country in Wikispeedia (2007) </div>
      <iframe class="graph" src="{{ '/graphs/topic_1/pie_plot_distribution_of_countries.html' | relative_url }}"></iframe>
    </div>
  </div>
</div>

<div class="col mb-4">
<div class="card shadow" data-aos="fade-up">
<div class="content p-4" markdown="1">

Let's now look at the connectivity between countries. 

<blockquote class="blockquote-content">
    Two countries are said to be <strong>connected</strong> if at least one article from the first country contains a link to an article associated to the other country.
</blockquote>

We contruct a graph of the Wikispeedia network overlayed with a world map for better visualization of the countries' importance. On this graph (bellow), we have: 
- each node is a country 
- the size and color of a node is proportional to the number of articles associtated to that node
- edges represent connnections between countries in the Wikipedia graph

With the slider on the top left part of the map we can select edges that occur more than a certain amount of times. We can see that edges that appear most (above 130 times) are those connecting countries that are associated to the most articles (e.g. USA, UK, France, Germany, Italy, India, Australia, China and Russia).

We also see that those same countries are central hubs of the network. They are part of most edges and are also connected to most other countries. This makes sense since the more articles there are, the more out-links there are and ultimately the higher the chance to be referenced by other articles. 

</div>
</div>
</div>

<div class="col mb-4" id="plot1">
  <div class="card shadow" data-aos="fade-up">
    <div class="content p-4">
      <div class="graph-title"> Figure 3: World map of connections between countries </div>
      <iframe class="graph" src="{{ '/graphs/topic_1/world_graph_map.html' | relative_url }}"></iframe>
    </div>
  </div>
</div>

<div class="col mb-4">
<div class="card shadow" data-aos="fade-up">
<div class="content p-4" markdown="1">

Lastly, let's look at the <a href="https://en.wikipedia.org/wiki/Directed_graph#Indegree_and_outdegree">in and out-degree</a> of each country. 

<blockquote class="blockquote-content" markdown="1">
For a given article A, the in-degree is the number of links found in other articles targetting A, while the out-degree is the number of outgoing links found in A. The in-degree of a country is then defined as the sum of the in-degrees of its articles. Same for the out-degree.

Thus, the higher the in degree of a country, the more central it is meaning that the more it is accessible from other countries.
</blockquote>

As expected, we observe that those same central hub countries, that make up for most of the articles in the graph, have also much more links that lead in and out of them.

</div>
</div>
</div>


<div class="col mb-4" id="plot1">
  <div class="card shadow" data-aos="fade-up">
    <div class="content p-4">
      <div class="graph-title"> Figure 4: Node degree of countries </div>
      <iframe class="graph" src="{{ '/graphs/topic_1/bar_plot_distribution_of_degrees.html' | relative_url }}"></iframe>
    </div>
  </div>
</div>


<div class="col mb-4">
<div class="card shadow" data-aos="fade-up">
<div class="content p-4" markdown="1">

#### Naive analysis of players click count

Now, let us analyze the players' behavior in the Wikispeedia game.

As seen previously, there is a unequal distribution of articles in Wikipedia, some countries are more represented than others. But, are those countries clicked more often by players within the Wikispeedia game? Or is there other countries that are clicked more often? We will now investigate if we see a bias independent from the countries distribution and whether the click count can be a good approximation of player's intention. 

To do so, a first naïve approach is simply to detect countries with higher click counts (see Figure 5). With this approach, it seems that players are highly biased in their way to play Wikispeedia as some countries like United States, United Kingdom, and Australia are represented by enormous dots due to their higher click count while other are almost not visible on the map.

However, a high click count can simply be due to the high number of articles associated to a particular country within the game. This does not necessarily tell us something about player's biases. Therefore, we rather focus on the ratio of click count divided by the number of articles to get a result closer to reality. On Figure 6, we see an overrepresentation of some countries like Vatican city, Brazil, or South Africa which are different from the previous ones. Therefore, part of the high click count can simply be explained by the high number of articles associated to a particular country. But there appear to be another factor influencing the click count per country as some countries remain more represented than other even when considering a scaled version of the click count.

But, can we rationally explain a differentially distributed click count? Is there other factors influcing the click count than simply player's biases? Onto the next topic to figure it out!

</div>
</div>
</div>

<div class="col mb-4">
<div class="card shadow" data-aos="fade-up">
<div class="content">
<div id="World_click_count" class="carousel slide" data-bs-theme="dark">
  <div class="carousel-inner">
    <div class="carousel-item active">
      <div class="graph-title"> Figure 5: World map of the click count per country and game path between countries before scaling </div>
      <iframe class="graph" src="{{ '/graphs/world_click_counts_before_scaling.html' | relative_url }}" ></iframe>
    </div>
    <div class="carousel-item">
      <div class="graph-title"> Figure 6: World map of the click count per country and game path between countries after scaling </div>
      <iframe class="graph" src="{{ '/graphs/world_click_counts_after_scaling.html' | relative_url }}" ></iframe>
    </div>
  </div>
  <button class="carousel-control-prev" type="button" data-bs-target="#World_click_count" data-bs-slide="prev">
    <span class="carousel-control-prev-icon" aria-hidden="true"></span>
    <span class="visually-hidden">Previous</span>
  </button>
  <button class="carousel-control-next" type="button" data-bs-target="#World_click_count" data-bs-slide="next">
    <span class="carousel-control-next-icon" aria-hidden="true"></span>
    <span class="visually-hidden">Next</span>
  </button>
</div>
</div>
</div>
</div>

<div class="col mb-4">
<div class="card shadow" data-aos="fade-up">
<div class="content p-4" markdown="1">

#### Dead ends analysis

[TODO: write that]()

</div>
</div>
</div>

<div class="col mb-4">
<div class="card shadow" data-aos="fade-up">
<div class="content p-4" markdown="1">

#### Accounting for the influence of the graph

As we saw in our first naive analysis, the click count metric, even when scaled by the number of articles per country, is not a good proxy for analyzing the players intentions. Indeed, it seems to be heavily influenced by the graph's structure. We will now explore how we can account for this influence and remove it as much as possible.

#### What variables influence the click count?

As seen before, countries with more articles have more clicks. This is very much expected, as the more articles a country has, the more likely it is that a user will encounter an article of that country. This is the most obvious example of a confounding variable that influences the click count. But this is not necessarily the only one. Indeed, it could be that other variables like the in-degree, out-degree, or even the categories of the articles have an influence on the click count. For example, for a given country, if the distribution of in-degrees is higher than the average, it means that players will see more links to that country, and thus might click more often on it.

</div>
</div>
</div>

<div class="col mb-4">
<div class="card shadow" data-aos="fade-up">
<div class="content p-4" markdown="1">

#### Ideal rebalancing

To make sure we account for as much confounders as possible, the ideal thing to do would be to set up some kind of propensity score matching. But how? Usually, propensity score matching is done between two groups that are compared in the experiment: a treatment group and a control group. However, in our case, we are comparing click counts across countries, meaning we do not have 2, but rather 249 groups that are compared with one another (one group per country).

The natural thing to do would then be to simply extend the propensity score matching to the 249 groups! Instead of looking for pairs of articles that have a similar propensity score, we would look for k-tuples, with k being the number of countries. But there are two issues with this approach:
1. Propensity score matching requires an algorithm that finds maximum cardinality matchings. Although there exists such algorithms that run in polynomial time when k=2, when k>2 <a href="https://en.wikipedia.org/wiki/3-dimensional_matching#Decision_problem">the problem is NP-hard</a>, meaning all currently known algorithms for this problem run in exponential time (pretty bad).
2. Alright, but our dataset is not that big! Couldn't we just use an exponential time algorithm and be done with it? Well, another problem would then arise: for a lot of countries, the number of articles assigned to them is 1. This means that we would only be able to create a single k-tuple, and then we would already have exhausted all articles for a lot of countries. That would mean that our rebalanced dataset would contain only one article per country, which of course is not enough to make any kind of analysis.

</div>
</div>
</div>

<div class="col mb-4">
<div class="card shadow" data-aos="fade-up">
<div class="content p-4" markdown="1">

#### A simpler approach

This means we need to consider something simpler. We will first analyze how much each variable influences the click count, and then manually normalize the click count by the variables that seem to have the most influence. This is a very naive approach, but it is the best we can do given the constraints of the problem.

#### Regression analysis

[TODO: explain regression analysis]()

</div>
</div>
</div>

<div class="col mb-4">
<div class="card shadow" data-aos="fade-up">
<div class="content p-4" markdown="1">

#### Normalizing the click count

Given the results of the regression analysis, we will only consider two confounders, which seem to have the most influence on the click count: the number of articles per country and the in-degree of each article. We will define a new metric, the normalized click count: for each country, we will divide the total number of clicks made to articles of that country by the total in-degree of that country. Note that given the high correlation between the in-degree of a country and the number of articles in that country (the more articles, the more links to those articles), this new metric is essentially accounting for both confounders at once.

Although it might seem like the way we computed this new metric is quite arbitrary, it actually still makes a lot of sense: we are essentially counting, for a given country, the average number of clicks that a single link to that country receives.

As we can see in the graph below, this already looks a lot more interesting. The top countries are no longer dominated by Western countries. We see countries like South Africa, Jordan or Mexico among the top. The USA is still pretty high (ending up at the second position), but it is now with Canada the only two Westerb countries left in the top 10.

</div>
</div>
</div>

<div class="col mb-4">
  <div class="card shadow" data-aos="fade-up">
    <div class="content p-4">
      <div class="graph-title"> Figure 7: World map of the normalized click count per country </div>
      <iframe class="graph" src="{{ '/graphs/normalized_click_counts.html' | relative_url }}" ></iframe>
    </div>
  </div>
</div>


<div class="col mb-4">
<div class="card shadow" data-aos="fade-up">
<div class="content p-4" markdown="1">

#### What variables influence the dead ends analysis?

[TODO: explain what was done to normalize the dead ends metric]()

</div>
</div>
</div>

<div class="col mb-4">
<div class="card shadow" data-aos="fade-up">
<div class="content p-4" markdown="1">

#### PageRank as a way to account for a lot of confounders at once

We will now dive into a last attempt at accounting for the influence of the graph on our analysis of the players behavior. To do so, we will use the PageRank algorithm. This algorithm simulates a random player that would start on a random article and then randomly click on links. It then outputs a score for each article, which is the probability that this random player clicked on that article at any given time. We will then compare this PageRank probability with the probability that a player from our dataset clicked on that article. For a given article, if the two probabilities are very different, it means that players from our dataset click more often (or less often) on that article than what would be expected from a random player.

#### What confounders do we account for?

By studying the difference between the PageRank probability and the players click probability, we are essentially accounting for all confounding variables coming from the graph structure. Indeed, given that both our players and the PageRank algorithm were given the exact same graph, if they behaved differently, it cannot be explained by variables coming from the graph!

However, it is important to note that we are only accounting for confounders in the structure of the graph, and not in the content of the articles. Variables like categories or titles might have a significant influence on the players behavior, and their distribution might change from one country to another. This is something that we cannot account for with the PageRank algorithm, and that we decided to ignore in this analysis.

[TODO: put some graphs of the top countries with the PageRank metric]()

</div>
</div>
</div>

<div class="col mb-4">
<div class="card shadow" data-aos="fade-up">
<div class="content p-4" markdown="1">

#### Players behavior in the context of publications per country

[TODO: write that]()

</div>
</div>
</div>

</div>
