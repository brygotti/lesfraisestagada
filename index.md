---
layout: default
title: Introduction
---

<div class="row row-cols-1">

<div class="col mb-4">
<div class="card shadow" data-aos="fade-up">
<div class="content p-4" markdown="1">
#### A story about biases

Today, content on the internet is still mostly produced by Western societies [[1]](https://upload.wikimedia.org/wikipedia/commons/4/4a/Decolonizing_Wikipedia.pdf) [[2]](https://www.theguardian.com/commentisfree/2017/oct/05/internet-white-western-google-wikipedia-skewed#:~:text=of%20the%20world.-,For%20the%20first%20time%20in%20history%2C%20we%20are%20creating%20a,skewed%20towards%20rich%2C%20western%20countries.). Interestingly, those same societies also produce most of the human knowledge, which we proxy as the number of citable publications [[3]](https://www.scimagojr.com/countryrank.php?year=2007&order=it&ord=desc#google_vignette). [Wikispeedia](https://dlab.epfl.ch/wikispeedia/play/) is an online game built on 4604 Wikipedia articles from 2007 during which players are navigating from a given start to a target end article through the links contained in the articles. In this project we intend to investigate how players navigate through the game and how this navigation is influenced by the production of scientific knowledge in the world. More precisely, we are interested in understanding whether players are attracted towards articles linked to countries producing a lot of scientific knowledge.

#### Why does this make sense?
As a small appetizer, let us throw a quick look at <a href="#carouselIntro" data-bs-toggle="tooltip" data-bs-title="Details on the data used to create these figures will be presented in the next section">figure 1 and 2</a>. We can already see the link between the two issues at hand: the distribution of articles per country in the Wikispeedia graph seems very closely related to the distribution of scientific knowledge production in the world. But how strong is this link? And how does it impact the players’ behavior in the game? Let's dive into the details to find out.

</div>
</div>
</div>

<div class="col mb-4">
<div class="card shadow" data-aos="fade-up">
<div class="content">
<div id="carouselIntro" class="carousel slide" data-bs-theme="dark">
  <div class="carousel-inner">
    <div class="carousel-item active">
      <div class="graph-title"> Figure 1: Number of publications per country (2007) </div>
      <iframe class="graph" src="{{ 'graphs/intro/publications_intro_map.html' | relative_url }}" ></iframe>
    </div>
    <div class="carousel-item">
      <div class="graph-title"> Figure 2: Number of articles per country in Wikispeedia (2007) </div>
      <iframe class="graph" src="{{ 'graphs/intro/articles_intro_map.html' | relative_url }}" ></iframe>
    </div>
  </div>
  <button class="carousel-control-prev" type="button" data-bs-target="#carouselIntro" data-bs-slide="prev">
    <span class="carousel-control-prev-icon" aria-hidden="true"></span>
    <span class="visually-hidden">Previous</span>
  </button>
  <button class="carousel-control-next" type="button" data-bs-target="#carouselIntro" data-bs-slide="next">
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
#### What is the plan?
The first step will be to understand the navigation patterns of players in the game. For this, we will compare two hypotheses, namely the “passive” and the “active” hypothesis.

In the “passive” hypothesis, we assume that players “passively” play on a graph that over-represents countries producing a lot of scientific knowledge. The players are not biased in themselves, they are only influenced by the graph. Thus, by removing the bias of the graph (i.e. by controlling as much as possible for the confounders of the graph), there should be no way to detect any bias in the players’ behavior.

On the other hand, the “active” hypothesis states that players “actively” add their own intrinsic biases when playing on that graph. That is, players are inherently attracted towards some countries, while disregarding others. By removing the graph bias, the player’s preference for some countries would in this hypothesis still be visible.

Once this first analysis is done, we will be in a good position to investigate what is the players' intrinsic bias, and whether it is related in any way to the production of scientific knowledge in the world.

Now, to succeed in this quest we are obliged to meet certain requirements. First, as we are working with a global database and as we intend to investigate worldwide geographical biases, we need to associate each article with a country. Next, to quantify the players’ behavior in the game we will use their clicking patterns, more precisely the number of times each article is clicked. Finally, as we are interested in showing how the production of scientific knowledge impacts players’ behavior, we need to match each of the previously defined countries to the number of publications produced within those countries during the year 2007. For precision on how exactly we implemented those methods, see the next section.
</div>
</div>
</div>

</div>