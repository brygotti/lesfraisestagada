---
layout: default
title: Analysis
---

<div class="row row-cols-1">

<div class="col mb-4">
<div class="card shadow" data-aos="fade-up">
<div class="content p-4" markdown="1">

#### Which countries are most represented in the Wikipedia graph?

[TODO: write that]()

</div>
</div>
</div>


<div id="carouselExample" class="carousel slide">
  <div class="carousel-inner">
    <div class="carousel-item active">
      <div class="col mb-4">
        <div class="card shadow" data-aos="fade-up">
            <div class="content p-4">
                <iframe class="graph" src="{{ '/graphs/topic_1/pie_plot_distribution_of_countries.html' | relative_url }}" ></iframe>
            </div>
        </div>
      </div>
    </div>
    <div class="carousel-item">
      <div class="col mb-4">
        <div class="card shadow" data-aos="fade-up">
            <div class="content p-4">
                <iframe class="graph" src="{{ '/graphs/topic_1/bar_plot_distribution_of_degrees.html' | relative_url }}" ></iframe>
            </div>
        </div>
      </div>
    </div>
    <div class="carousel-item">
      <div class="col mb-4">
        <div class="card shadow" data-aos="fade-up">
            <div class="content p-4">
                <iframe class="graph" src="{{ '/graphs/topic_1/country_graph.html' | relative_url }}" ></iframe>
            </div>
        </div>
      </div>
    </div>
  </div>
  <button class="carousel-control-prev" type="button" data-bs-target="#carouselExample" data-bs-slide="prev">
    <span class="carousel-control-prev-icon" aria-hidden="true"></span>
    <span class="visually-hidden">Previous</span>
  </button>
  <button class="carousel-control-next" type="button" data-bs-target="#carouselExample" data-bs-slide="next">
    <span class="carousel-control-next-icon" aria-hidden="true"></span>
    <span class="visually-hidden">Next</span>
  </button>
</div>




<div class="btn-group">
  <button type="button" class="btn btn-danger dropdown-toggle" data-bs-toggle="dropdown" aria-expanded="false">
    Action
  </button>
  <ul class="dropdown-menu">
    <li><a class="dropdown-item" href="#" id="action1">All</a></li>
    <li><a class="dropdown-item" href="#" id="action2">Switzerland</a></li>
    <li><a class="dropdown-item" href="#" id="action3">France</a></li>
  </ul>
</div>

<!-- Plot 1 -->
<div class="col mb-4" id="plot1">
  <div class="card shadow" data-aos="fade-up">
    <div class="content p-4">
      <iframe class="graph" src="{{ '/graphs/topic_1/country_graph.html' | relative_url }}"></iframe>
    </div>
  </div>
</div>

<!-- Plot 2 -->
<div class="col mb-4" id="plot2" style="display: none;">
  <div class="card shadow" data-aos="fade-up">
    <div class="content p-4">
      <iframe class="graph" src="{{ '/graphs/topic_1/country_graph_switzerland.html' | relative_url }}"></iframe>
    </div>
  </div>
</div>

<!-- Plot 3 -->
<div class="col mb-4" id="plot3" style="display: none;">
  <div class="card shadow" data-aos="fade-up">
    <div class="content p-4">
      <iframe class="graph" src="{{ '/graphs/topic_1/country_graph_france.html' | relative_url }}"></iframe>
    </div>
  </div>
</div>

<script>
  // Function to hide all plots
  function hideAllPlots() {
    document.getElementById("plot1").style.display = "none";
    document.getElementById("plot2").style.display = "none";
    document.getElementById("plot3").style.display = "none";
  }

  // Event listeners for dropdown actions
  document.getElementById("action1").addEventListener("click", function() {
    hideAllPlots();
    document.getElementById("plot1").style.display = "block";  // Show plot 1
  });

  document.getElementById("action2").addEventListener("click", function() {
    hideAllPlots();
    document.getElementById("plot2").style.display = "block";  // Show plot 2
  });

  document.getElementById("action3").addEventListener("click", function() {
    hideAllPlots();
    document.getElementById("plot3").style.display = "block";  // Show plot 3
  });
</script>



<div class="col mb-4">
<div class="card shadow" data-aos="fade-up">
<div class="content p-4" markdown="1">

#### Naive analysis of players click count

As seen previously, there is a unequal distribution of articles in Wikipedia, some countries are more represented than others. But, are those countries clicked more often by players within the Wikispeedia game? Or is there other countries that are clicked more often? We will now investigate if we see a bias independent from the coutries distribution and whether the click count can be a good approximation of player's intention. 

To do so, a first naïve approach is simply to detect countries with higher click counts (see Figure 1). With this approach, it seems that players are highly biased in their way to play Wikispeedia as some countries like United States, United Kingdom, and Australia are represented by enormous dots due to their higher click count while other are almost not visible on the map.

However, a high click count can simply be due to the high number of articles associated to a particular country within the game. This does not necessarily tell us something about player's biases. Therefore, we rather focus on the ratio of click count divided by the number of articles to get a result closer to reality. On Figure 2, we see a overrepresentation of some countries like Vatican city, Brazil, or South Africa which are different from the previous ones. Therefore, part of the high click count can simply be explained by the high number of articles associated to a particular country. But there appear to be another factor influencing the click count per country as some countries remain more represented than other even when considering a scaled version of the click count.

But, can we rationally explain a differentially distributed click count? Is there other factors influcing the click count that simply player's biases? Onto the next topic to figure it out!

</div>
</div>
</div>

<div id="carouselExample" class="carousel slide">
  <div class="carousel-inner">
    <div class="carousel-item active">
      <div class="col mb-4">
      <div class="card shadow" data-aos="fade-up">
      <div class="content p-4">
      <iframe class="graph" src="{{ '/graphs/world_counts_and_articles_after_scaling.html' | relative_url }}" ></iframe>
      </div>
      </div>
      </div>
    </div>
    <div class="carousel-item">
      <div class="col mb-4">
      <div class="card shadow" data-aos="fade-up">
      <div class="content p-4">
      <iframe class="graph" src="{{ '/graphs/world_counts_and_articles_before_scaling.html' | relative_url }}" ></iframe>
      </div>
      </div>
      </div>
    </div>
  </div>
  <button class="carousel-control-prev" type="button" data-bs-target="#carouselExample" data-bs-slide="prev">
    <span class="carousel-control-prev-icon" aria-hidden="true"></span>
    <span class="visually-hidden">Previous</span>
  </button>
  <button class="carousel-control-next" type="button" data-bs-target="#carouselExample" data-bs-slide="next">
    <span class="carousel-control-next-icon" aria-hidden="true"></span>
    <span class="visually-hidden">Next</span>
  </button>
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

As we saw in our first naive analysis, the click count metric is not a good proxy for analyzing the players intentions. Indeed, it seems to be heavily influenced by the graph's structure. We will now explore how we can account for this influence and remove it as much as possible.

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
1. Propensity score matching requires an algorithm that finds maximum cardinality matchings. Although there exists such algorithms that run in polynomial time when k=2, when k>2 the problem is NP-hard, meaning all currently known algorithms for this problem run in exponential time (pretty bad).
2. Alright, but our dataset is not that big! Couldn't we just use an exponential time algorithm and be done with it? Well, another problem would then arise: for a lot of countries, the number of articles assigned to them is 1. This means that we would only be able to create a single k-tuple, and then we would already have exhausted all articles for a lot of countries. That would mean that our rebalanced dataset would contain only one article per country, which of course is not enough to make any kind of analysis.

[TODO: put some graph from this page for example ?](https://en.wikipedia.org/wiki/3-dimensional_matching)

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

Given the results of the regression analysis, we will only consider two confounders, which seem to have the most influence on the click count: the number of articles per country and the in-degree of each article. We will define a new metric, the normalized click count: for each country, we will divide the total number of clicks made to articles of that country by the total number of links-in from articles of that country. This will give us a metric that accounts for the influence of the number of articles and the in-degree of each country.

Of course, the way we computed this new metric is quite arbitrary, and there might be many other ways to do it. For example, if the relationship between the in-degree and the click count was quadratic, it would make more sense to divide the click count by the square of the in-degree. But given that it is very hard to know for sure what the relationship between our confounders and the click count is, we will stick to this simple approach. This actually still makes quite a bit of sense: we are essentially counting, for a given country, the average number of clicks that a single link to that country receives.

[TODO: put some graphs of the top countries with the normalized click count]()

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
