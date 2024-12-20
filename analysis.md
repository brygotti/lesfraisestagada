---
layout: default
title: Analysis
---

<div class="row row-cols-1">

<div class="col mb-4">
<div class="card shadow" data-aos="fade-up">
<div class="content p-4" markdown="1">

#### A quick word about articles!

As we said in the introduction, we want to associate each article to a country. But why does this actually make sense? Well, if we hover our mouse over the nodes in <a href="#carouselGraphArticles" data-bs-toggle="tooltip">figure 1 and 2</a> below, we can see that almost all atricles among the top 20 can be associated to a country (*e.g. English_language to England*). The same is true for the bottom 20 articles (*e.g. Afghan hound to Afghanistan*). But we see that the most clicked articles are densely connected with each other, whereas the least clicked articles are not.  

This motivates our decision to analyze the Wikispeedia game in terms of countries. In the end, we are interested in whether players of the Wikispeedia game really tend to click more on articles that are associated with western countries or if this feature is due to the properties of the Wikipedia graph itself. Let's dive into the analysis and see if we can conclude anything! 

</div>
</div>
</div>

<div class="col mb-4">
<div class="card shadow" data-aos="fade-up">
<div class="content">
<div id="carouselGraphArticles" class="carousel slide" data-bs-theme="dark">
  <div class="carousel-inner">
    <div class="carousel-item active">
      <div class="graph-title"> Figure 1: Connectivity of most clicked articles </div>
      <iframe class="graph" src="{{ 'graphs/topic_1/most_used_articles_graph.html' | relative_url }}"></iframe>
      <div style="padding: 10px;">
        Legend: Each node represents an article <br/>
        <strong>Node color</strong>: darker if the article is clicked more often in Wikispeedia <br/>
        <strong>Edges</strong>: represent outgoing links found in the articles <br/>
        <strong>In degree and out degree</strong>: see <a href="https://en.wikipedia.org/wiki/Directed_graph#Indegree_and_outdegree">here</a>
      </div>
    </div>
    <div class="carousel-item">
      <div class="graph-title"> Figure 2: Connectivity of least clicked articles </div>
      <iframe class="graph" src="{{ 'graphs/topic_1/least_used_articles_graph.html' | relative_url }}" id="connectivity_plot"></iframe>
      <div style="padding: 10px;">
        Legend: Each node represents an article<br/>
        <strong>Node color</strong>: darker if the article is clicked more often in Wikispeedia <br/>
        <strong>Edges</strong>: represent outgoing links found in the articles <br/>
        <strong>In degree and out degree</strong>: see <a href="https://en.wikipedia.org/wiki/Directed_graph#Indegree_and_outdegree">here</a>
      </div>
    </div>
  </div>
  <button class="carousel-control-prev refresher" type="button" data-bs-target="#carouselGraphArticles" data-bs-slide="prev">
    <span class="carousel-control-prev-icon" aria-hidden="true"></span>
    <span class="visually-hidden">Previous</span>
  </button>
  <button class="carousel-control-next refresher" type="button" data-bs-target="#carouselGraphArticles" data-bs-slide="next">
    <span class="carousel-control-next-icon" aria-hidden="true"></span>
    <span class="visually-hidden">Next</span>
  </button>
  <script>
    document.querySelectorAll('.refresher').forEach((el) => {
      el.addEventListener('click', () => {
        document.getElementById('connectivity_plot').src = document.getElementById('connectivity_plot').src
      });
    });
  </script>
</div>
</div>
</div>
</div>

<div class="col mb-4">
<div class="card shadow" data-aos="fade-up">
<div class="content p-4" markdown="1">

#### Which countries are most represented in the Wikipedia graph?

Now that all (most) articles are associated to a country, we can look at the distribution of those countries. Is there a country that is associated to more articles? (we have our little idea, but let's check). 

We see that 8 countries make up for <sup>1</sup>/<sub>2</sub> of the articles in Wikipedia, namely the **US**, **UK**, **Australia**, **France**, **Germany**, **Italy**, **India** and **China**. Those are all in the top 10 of countries that publish the most (see [here](https://www.scimagojr.com/countryrank.php?year=2007)!)!

With <a href="#pie" data-bs-toggle="tooltip">figure 3</a>, we get a first intuition of the cultural bias that is present in the Wikipeedia graph: countries that publish most are also represented by more articles. When players play on this already biased graph, they will obviously click most on articles from those countries. So, later, when we analyze the behavior of the players, we will have to keep this in mind and normalize the click counts of the players by the number of articles per country! But this is for later, let's go on here!

</div>
</div>
</div>


<div class="col mb-4" id="pie">
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

We contruct a graph of the Wikispeedia network overlayed with a world map for better visualization of the countries' importance. On this graph (<a href="#world-map-wikipedia" data-bs-toggle="tooltip">figure 4</a>), we have: 
- each node is a country 
- the size and color of a node is proportional to the number of articles associtated to that node
- edges represent connnections between countries in the Wikipedia graph

With the slider on the top left part of the map we can select edges that occur more than a certain amount of times. We can see that edges that appear most (above 130 times) are those connecting countries that are associated to the most articles (e.g. USA, UK, France, Germany, Italy, India, Australia, China and Russia).

We also see that those same countries are central hubs of the network. They are part of most edges and are also connected to most other countries. This makes sense since the more articles there are, the more out-links there are and ultimately the higher the chance to be referenced by other articles. 

</div>
</div>
</div>

<div class="col mb-4" id="world-map-wikipedia">
  <div class="card shadow" data-aos="fade-up">
    <div class="content p-4">
      <div class="graph-title"> Figure 4: World map of connections between countries </div>
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


<div class="col mb-4" id="node-degrees">
  <div class="card shadow" data-aos="fade-up">
    <div class="content p-4">
      <div class="graph-title"> Figure 5: Node degree of countries </div>
      <iframe class="graph" src="{{ '/graphs/topic_1/bar_plot_distribution_of_degrees.html' | relative_url }}"></iframe>
    </div>
  </div>
</div>


<div class="col mb-4">
<div class="card shadow" data-aos="fade-up">
<div class="content p-4" markdown="1">

#### Distribution of countries among source and target articles
This is a crucial analysis. Indeed, both the source and the target articles are not chosen by the player but are still counted as clicks in the way we calculated the click count variable. It is thus important to get an idea of the distribution of the countries among those pseudo-clicks to then take the decision of removing them in case the distribution of not uniform. 

To investigate this we need to look at the finished paths in order to extract source and target articles. 

<blockquote class="blockquote-content" markdown="1"> 
<strong> In the following steps of the analysis the Start and Stop articles will be discarded from the click counts. </strong>
</blockquote>

</div>
</div>
</div>

<div class="col mb-4" id="plot1">
  <div class="card shadow" data-aos="fade-up">
    <div class="content p-4">
      <div class="graph-title"> Figure 6: Dead end countries </div>
      <iframe class="graph" src="{{ '/graphs/topic_2/start_stop_count.html' | relative_url }}"></iframe>
    </div>
  </div>
</div>


<div class="col mb-4">
<div class="card shadow" data-aos="fade-up">
<div class="content p-4" markdown="1">


#### Naive analysis of players click count

Now, let us analyze the players' clicking behavior in the Wikispeedia game.

As seen previously, there is a unequal distribution of articles in Wikipedia, some countries are more represented than others. But, are those countries clicked more often by players within the Wikispeedia game? Or are there other countries that are clicked more often? We will now investigate if we see a bias independent from the countries distribution and whether the click count can be a good approximation of player's intention. 

To do so, a first naïve approach is simply to detect countries with higher click counts (<a href="#World_click_count" data-bs-toggle="tooltip">see figure 8</a>). With this approach, it seems that players are highly biased in their way to play Wikispeedia as some countries like United States, United Kingdom, and Australia are represented by enormous dots due to their higher click count while other are almost not visible on the map. Edges between countries represent game paths. Darker paths are the most used ones, among those we can see that paths linking United States to United Kingdom, Australia, France, China, Germany or Japan dominate. There also seems to be commonly used paths between different countries in Europe. 

However, a high click count can simply be due to the high number of articles associated to a particular country within the game. This does not necessarily tell us something about player's biases. Therefore, we rather focus on the ratio of click count divided by the number of articles to get a result closer to reality. On <a href="#World_click_count" data-bs-toggle="tooltip">figure 9</a>, we see an overrepresentation of some countries like Vatican city, Brazil, or South Africa which are different from the previous ones. Vatican city is a particular case in this dataset as there is only one article associated with this country so the click count is not influenced by the scaling. It could be considered as an outlier, not necesarilly indicating something about player's biases. Therefore, the scaled click count map indicates that part of a high click count can simply be explained by the high number of articles associated to a particular country. But scaling creates some artefacts like Vatican city so it does not seem to be the best approach. There appear to be another factor influencing the click count per country as some countries remain more represented than other even when considering a scaled version of the click count.

But, can we rationally explain a differentially distributed click count? Are there other factors influcing the click count of player's? Onto the next topic to figure it out!

</div>
</div>
</div>

<div class="col mb-4">
<div class="card shadow" data-aos="fade-up">
<div class="content">
<div id="World_click_count" class="carousel slide" data-bs-theme="dark">
  <div class="carousel-inner">
    <div class="carousel-item active">
      <div class="graph-title"> Figure 8: World map of the click count per country and game path between countries before scaling </div>
      <iframe class="graph" src="{{ '/graphs/topic_2/world_click_counts_before_scaling.html' | relative_url }}" ></iframe>
    </div>
    <div class="carousel-item">
      <div class="graph-title"> Figure 9: World map of the click count per country and game path between countries after scaling </div>
      <iframe class="graph" src="{{ '/graphs/topic_2/world_click_counts_after_scaling.html' | relative_url }}" ></iframe>
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


### What do we call a dead-end ?

Dead ends in the context of Wikipedia navigation are articles that players encounter but struggle to move forward from, leading to either backtracking or abandoning the path altogether. Understanding dead ends provides valuable insight into user behavior, article connectivity, and potential biases in navigation patterns. By identifying these points of friction, we can better interpret how graph structures and content influence player decisions.

In this analysis, we will:
1. **Identify countries as potential dead ends based on click counts and mean failure ratio (unique).** Are highly connected countries inherently more prone to becoming dead ends due to visibility and accessibility? Or are less-connected countries genuinely more challenging for navigation?
2. **Examine last articles in unfinished paths.** Which countries frequently appear at the end of failed navigation attempts? What does scaling these occurrences by outgoing links reveal about genuine dead ends versus highly connected hubs?
3. **Analyze backtracking behavior.** What countries or articles trigger backtracking, and how does scaling highlight less obvious dead ends that trap players?
<!-- 4. **Explore the relationship between start/stop countries and back-click rates.** Do certain countries cause players to abandon paths more frequently, and how does this change depending on their position in the navigation sequence? -->


#### 1. Spotting Dead Ends Through Click Counts and Mean Failure Ratio
In this part, we sort the countries based on their click count and unique mean failure ratio. To calculate the unique failure ratio, we count each occurrence of a country in unfinished paths only once. This approach eliminates circular patterns and repeated entries, ensuring a clearer and more accurate representation of how often each country contributes to navigation failures.

Uh oh, this plot might be biased. Not only has the United States received an overwhelmingly high number of clicks, but it also has significantly more outgoing links (16,338) than other countries. This likely inflates its visibility and accessibility, making it appear more frequently in player paths. Familiarity bias (e.g., cultural or linguistic factors) further skews the data toward countries like the US and UK.
To reduce this bias, we scale the number of clicks by the sum of outgoing links per country. This reveals a more nuanced picture, where less-connected countries such as Greenland, Bolivia, Brazil emerge as significant dead ends. Scaling sheds light on genuine navigation patterns, helping us differentiate between structural biases and true player challenges.

</div>
</div>
</div>

<div class="col mb-4" id="plot1">
  <div class="card shadow" data-aos="fade-up">
    <div class="content p-4">
      <div class="graph-title"> Figure 9: Top 10 Countries by Click Count and Mean Failure Ratio (Scaled vs. Unscaled) </div>
      <iframe class="graph" src="{{ '/graphs/topic_2/dead_ends_analysis1.html' | relative_url }}"></iframe>
    </div>
  </div>
</div>

<div class="col mb-4">
<div class="card shadow" data-aos="fade-up">
<div class="content p-4" markdown="1">

#### 2. **Analyzing Last Article in Unfinished Paths: Which Countries Trap Players?**
What happens when a player’s navigation ends unsuccessfully? By analyzing the last articles in unfinished paths, we identify which countries are the most frequent dead ends. Initially, highly connected countries like the United States dominate this list, reflecting their prominence in raw data.

However, scaling by outgoing links tells a different story. Countries like Greenland, Bolivia, and South Africa emerge as true dead ends, suggesting specific navigational patterns or challenges that lead players to abandon these paths. These insights highlight the limitations of raw data in capturing genuine player behavior.


</div>
</div>
</div>

<div class="col mb-4" id="plot1">
  <div class="card shadow" data-aos="fade-up">
    <div class="content p-4">
      <div class="graph-title"> Figure 10 : Top 10 Last Articles in Unfinished Paths: Raw vs. Scaled Occurrences by Outgoing Links </div>
      <iframe class="graph" src="{{ '/graphs/topic_2/dead_ends_analysis2.html' | relative_url }}"></iframe>
    </div>
  </div>
</div>

<div class="col mb-4">
<div class="card shadow" data-aos="fade-up">
<div class="content p-4" markdown="1">

#### 3. **Backtracking Behavior: What Leads Players to Retreat?**
Before players give up, they often hit a point where they backtrack. By examining the most common articles preceding the “go back” action, we identify key friction points. Unsurprisingly, highly connected countries like the United States and United Kingdom dominate the raw data.

Scaling by outgoing links, however, reveals less obvious dead ends. Countries like French Polynesia and Vatican City, despite their limited connectivity, frequently prompt backtracking. This suggests players feel stuck due to limited onward options, making these articles true navigation roadblocks.
</div>
</div>
</div>

<div class="col mb-4" id="plot1">
  <div class="card shadow" data-aos="fade-up">
    <div class="content p-4">
      <div class="graph-title"> TITLEEE </div>
      <iframe class="graph" src="{{ '/graphs/topic_1/dead_ends_analysis3.html' | relative_url }}"></iframe>
    </div>
  </div>
</div>



<div class="col mb-4">
<div class="card shadow" data-aos="fade-up">
<div class="content p-4" markdown="1">


#### Accounting for the influence of the graph

As we saw in the two parts above, the click count metric, even when scaled by the number of articles per country or by the number of outgoing links, is still not a good enough proxy for analyzing the players intentions. Indeed, it seems to be heavily influenced by the graph's structure. We need something more advanced to account for this influence. So now let's jump into the next section !

#### What variables influence the click count?

As seen before, countries with more articles have more clicks. This is very much expected, as the more articles a country has, the more likely it is that a user will encounter an article of that country. This is the most obvious example of a confounding variable that influences the click count. But this is not necessarily the only one. Indeed, it could be that other variables like the in-degree, out-degree, or even the categories of the articles have an influence on the click count. For example, for a given country, if the distribution of in-degrees is higher than the average, it means that players will see more links to that country, and thus might click more often on it.

</div>
</div>
</div>

<div class="col mb-4">
<div class="card shadow" data-aos="fade-up">
<div class="content p-4" markdown="1">

#### Ideal rebalancing

To make sure we account for as much confounders as possible, the ideal thing to do would be to set up some kind of propensity score matching. But how? Usually, propensity score matching is done between two groups that are compared in the experiment: a treatment group and a control group. However, in our case, we are comparing click counts across countries, meaning we do not have 2, but rather a maximum of 195 groups that are compared with one another (one group per country, indeed, only 195 out of the 249 llm classified countries actually have articles associated to them).

The natural thing to do would then be to simply extend the propensity score matching to the 195 groups! Instead of looking for pairs of articles that have a similar propensity score, we would look for k-tuples, with k being the number of countries. But there are two issues with this approach:
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

</div>
</div>
</div>

<div class="col mb-4">
<div class="card shadow" data-aos="fade-up">
<div class="content p-4" markdown="1">

#### Normalizing the click count

By doing a regression analysis, we found that the number of links leading into an article is highly positively correlated with the player's click counts (rho=0.78, R2=0.63), we will thus only consider two confounders, which seem to have the most influence on the click count: the number of articles per country and the in-degree of each article. We will define a new metric, the normalized click count: for each country, we will divide the total number of clicks made to articles of that country by the total in-degree of that country. Note that given the high correlation between the in-degree of a country and the number of articles in that country (the more articles, the more links to those articles), this new metric is essentially accounting for both confounders at once.

Although it might seem like the way we computed this new metric is quite arbitrary, it actually still makes a lot of sense: we are essentially counting, for a given country, the average number of clicks that a single link to that country receives.

As we can see in the graph below, this already looks a lot more interesting. The top countries are no longer dominated by Western countries. We see countries like South Africa, Jordan or Mexico among the top. The USA is still pretty high (ending up at the second position), but it is now with Canada the only two Western countries left in the top 10.

</div>
</div>
</div>

<div class="col mb-4">
  <div class="card shadow" data-aos="fade-up">
    <div class="content p-4">
      <div class="graph-title"> Figure 10: World map of the normalized click count per country </div>
      <iframe class="graph" src="{{ '/graphs/topic_3/normalized_click_counts.html' | relative_url }}" ></iframe>
    </div>
  </div>
</div>

<div class="col mb-4">
<div class="card shadow" data-aos="fade-up">
<div class="content p-4" markdown="1">

#### PageRank as a way to account for a lot of confounders at once

We will now dive into a last attempt at accounting for the influence of the graph on our analysis of the players behavior. To do so, we will use the PageRank algorithm. This algorithm simulates a random player that would start on a random article and then randomly click on links. It then outputs a score for each article, which is the probability that this random player clicked on that article at any given time. We will then compare this PageRank probability with the probability that a player from our dataset clicked on that article (we call this second probability the player rank). For a given article, if the two probabilities are very different, it means that players from our dataset click more often (or less often) on that article than what would be expected from a random player.

#### What confounders do we account for?

By studying the difference between the PageRank probability and the player rank probability, we are essentially accounting for all confounding variables coming from the graph structure. Indeed, given that both our players and the PageRank algorithm were given the exact same graph, if they behaved differently, it cannot be explained by variables coming from the graph!

However, it is important to note that we are only accounting for confounders in the structure of the graph, and not in the content of the articles. Variables like categories or titles might have a significant influence on the players behavior, and their distribution might change from one country to another. This is something that we cannot account for with the PageRank algorithm, and that we decided to ignore in this analysis.

</div>
</div>
</div>

<div class="col mb-4">
<div class="card shadow" data-aos="fade-up">
<div class="content">
<div id="pagerank" class="carousel slide" data-bs-theme="dark">
  <div class="carousel-inner">
    <div class="carousel-item active">
      <div class="graph-title"> Figure 11: PageRank vs players comparison </div>
      <iframe class="graph" src="{{ '/graphs/topic_3/player_vs_pagerank.html' | relative_url }}" ></iframe>
    </div>
    <div class="carousel-item">
      <div class="graph-title"> Figure 12: PageRank difference (Player rank minus PageRank) </div>
      <iframe class="graph" src="{{ '/graphs/topic_3/rank_diff.html' | relative_url }}" id="rank_diff"></iframe>
    </div>
  </div>
  <button class="carousel-control-prev refresher2" type="button" data-bs-target="#pagerank" data-bs-slide="prev">
    <span class="carousel-control-prev-icon" aria-hidden="true"></span>
    <span class="visually-hidden">Previous</span>
  </button>
  <button class="carousel-control-next refresher2" type="button" data-bs-target="#pagerank" data-bs-slide="next">
    <span class="carousel-control-next-icon" aria-hidden="true"></span>
    <span class="visually-hidden">Next</span>
  </button>
  <script>
    document.querySelectorAll('.refresher2').forEach((el) => {
      el.addEventListener('click', () => {
        document.getElementById('rank_diff').src = document.getElementById('rank_diff').src
      });
    });
  </script>
</div>
</div>
</div>
</div>

<div class="col mb-4">
<div class="card shadow" data-aos="fade-up">
<div class="content p-4" markdown="1">

#### PageRank analysis

As we can see in the plot in figure 11, the player rank is very similar to the PageRank for the top 10 countries. This shows a strong influence from the graph structure on the players behavior. In figure 12, we subtract the PageRank from the player rank. With that, we are essentially doing a change of reference frame, now computing how much more (or less) often a player clicked on an article compared to a random player. The differences seem very small, but it is good to remember that they must be interpreted as probabilities. To make sure the difference is significant, we computed a chi-square test (the null hypothesis being that the player behaves exactly like a random walker), and the p-value was found to be very close to 0 (\\(p \ll 0.05\\)). This proves that although the players are highly influenced by the graph, they still have some intrinsic biases.

Looking at the top 10 countries in term of rank difference (figure 12), we see that a lot of them were already present in the top 10 of the normalized click count: USA, South Africa, Greece or UK. This confirms the soundness of our earlier analysis. But given how the PageRank analysis accounts for a lot more confounders than the normalized click count, we will focus for the next part on countries that have a high enough rank difference to be considered as significant, that is: USA, South Africa, UK, Greece, Brazil, Mexico and Canada Interestingly, the bottom 10 countries in term of rank difference (figure 12) seem to be made up of some pretty big players in the scientific world like France, China or India.
</div>
</div>
</div>


</div>


<div class="col mb-4">
<div class="card shadow" data-aos="fade-up">
<div class="content p-4" markdown="1">

#### Let's wrap up! 

We were able to show that the Wikipedia graph is accurately representing the world knowledge, and that the countries dominating the web are also the major world powers (i.e. USA, UK, China). Since, the Wikispeedia game is built on Wikipedia, it is biased toward countries producing the most publications. 

Then, we focused on the behavior of players and tried to show that they are intrinsically biased toward some countries. A first naive analysis showed that the player's clicks are strikingly skewed towards the major world. But after scaling and accounting for multiple factors influencing players' behaviors all countries seem to be approximately equally represented in terms of clicks of players. We observe small preferences towards some countries but they are too small to be significant. This indicates that players are mostly biased due to the graph structure but do not have additional intrisic biases. 

📢📢📢📢📢 The take home message here is: **a biased web makes you biased** !! 
</div>
</div>
</div>
