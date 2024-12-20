---
layout: default
title: Data & Preprocessing
---
<div class="row row-cols-1">

<!-- # Anatomy of the data
https://github.com/Jeremmmyyyyy/ADA-Project-M1 → data description and structure -->



<div class="col mb-4">
<div class="card shadow" data-aos="fade-up">
<div class="content p-4" markdown="1">

#### Country assignment

Let us start by talking about how we assigned countries to the articles of the Wikispeedia game.

<div class="alert alert-success" markdown="1">
**The plan**:

- Assign a country to each article
- Try different methods and see how many articles can be classified
- Verify these classification with human annotation
- Select the best method for further analysis of the dataset
</div>

<div class="alert alert-warning" markdown="1">
**Countries**:

In order to classify countries we used the standard ISO list with 249 countries and the following distribution: 

- UN Members: 193
- UN Observer States: 2
- States With Partial Recognition: 2
- Inhabited Dependent Territories: 45
- Uninhabited Territories: 6
- Antarctica: 1
</div>

A naïve method was employed to classify articles to specific countries by performing a text search to identify occurrences of country names within the plaintext. This approach utilized basic regular expression matching to analyze the articles. However, it resulted in approximately 31% of the articles (1,412 out of 4,604) remaining unclassified, highlighting significant limitations.

#### Identified issues with the approach
1. **Over-classification on mentioned country names**: 
   The presence of a country name in an article does not necessarily imply that the article belongs to that country. This assumption leads to inaccuracies in classification.

2. **Lack of contextual understanding**: 
   The text search method lacks the ability to discern the context in which a country name appears, resulting in potential misclassifications.

3. **Observations**: 
   A review of the articles revealed a lot of incorrect or missing classifications. For example:
   - The article *13th Century* was missclassified under China due to mentions of events occurring there during that period, despite the article lacking any specific association with China.
   - Conversely, the article *4-2-0*, which details a type of railroad in the United States, was left unclassified despite its clear appartenance to that country.

These findings show the limitations of the current text-matching methodology and highlight the need for a more robust, context-aware approach to accurately classify articles.

</div>
</div>
</div>


<div class="col mb-4">
<div class="card shadow" data-aos="fade-up">
<div class="content p-4" markdown="1">
#### Classification using LLMs

Given the limitations of the initial text-search-based approach, a decision was made to use Large Language Models (LLMs) to enhance the article classification process. LLMs, with their extensive general knowledge, have the capability to analyze articles and respond to queries with a deeper understanding. 

Unlike simple text searches, LLMs not only utilize the content of the article but also incorporate their pre-existing (trained) knowledge. This contextual understanding should enables more accurate classification.

By employing LLMs, two potential strategies can be pursued:
1. **Targeted classification of previously unclassified articles**: The 1,412 articles that remained unclassified under the initial approach can be reevaluated, allowing for a significant reduction in the unclassified proportion. After this step only 6% (283 out of 4604) were not classified.

2. **Full Reclassification**: LLMs can be used to perform a complete reclassification of all articles, eliminating the biases and limitations inherent in the original text-search methodology. In order to test this two existing LLMs were used : [LLaMa](https://www.llama.com/) and [Qwen](https://qwen-ai.com/). These powerful models, with less than 8 billion parameters, offer significant computational efficiency and can be run locally on consumer hardware, making them accessible and cost-effective solutions compared to bigger models like ChatGPT and their paid API.

This transition to LLM-based classification is expected to significantly improve the accuracy and reliability of the country assignment process.

The prompt used in order to make the models classify the articles was the following : 

<blockquote class="blockquote-content">
You will be given textual articles. For each article provide a single and unique country to which the article is related and should be classified to. Provide the answer in the form : country.<br/>
If there is no country related to the article, please write 'None'.<br/>
If the location is not on earth, please write 'None'.<br/>
If the article is a general article where the content is not specifically related to a country, please write 'None'.<br/>
You must be 100% sure this is a question of life.<br/>
This is the list of coutnries that you are allowed to output don't output anything that is not in this list: {countries}
</blockquote>

</div>
</div>
</div>


<div class="col mb-4">
  <div class="card shadow" data-aos="fade-up">
    <div class="content p-4" style="height: 70vh">
          <div class="graph-title"> Figure 1: Proportion of articles assigned to a country</div>
          <iframe class="graph" src="{{ '/graphs/preprocessing/proportion_country_assignment.html' | relative_url }}" ></iframe>
    </div>
  </div>
</div>
<!-- Keep previous heatmap carousel implementation in case -->
<!-- <div class="col mb-4">
<div class="card shadow" data-aos="fade-up">
<div class="content">
<div id="carouselCountry" class="carousel slide" data-bs-theme="dark">
  <div class="carousel-inner">
    <div class="carousel-item active" style="height: 75vh">
      <div class="graph-title"> Figure 1: Proportion of articles assigned to a country</div>
      <iframe class="graph" src="{{ '/graphs/preprocessing/proportion_country_assignment.html' | relative_url }}" ></iframe>
    </div>
    <div class="carousel-item" style="min-height: 75vh; overflow: auto;">
      <div class="graph-title"> Figure 2: Overlap Between Classification Methods</div>
      <iframe class="graph" src="{{ '/graphs/preprocessing/overlap_heatmap.html' | relative_url }}" style="flex: 1;"></iframe>
      <div style="padding: 10px;">
        Legend: <br/>
        0: Text search <br/>
        1: Text search + missing entries with LLaMa <br/>
        2: Full classification with Qwen <br/>
        3: Full classification with LLaMa <br/>
        4: Improved classification with LLaMa
      </div>
    </div>
  </div>
  <button class="carousel-control-prev" type="button" data-bs-target="#carouselCountry" data-bs-slide="prev">
    <span class="carousel-control-prev-icon" aria-hidden="true"></span>
    <span class="visually-hidden">Previous</span>
  </button>
  <button class="carousel-control-next" type="button" data-bs-target="#carouselCountry" data-bs-slide="next">
    <span class="carousel-control-next-icon" aria-hidden="true"></span>
    <span class="visually-hidden">Next</span>
  </button>
</div>
</div>
</div>
</div> -->


<div class="col mb-4">
<div class="card shadow" data-aos="fade-up">
<div class="content p-4" markdown="1">
#### Assessing classification accuracy

To test the accuracy of the model’s predictions compared to human judgment, each member of the group manually annotated 20 articles, with a 10-article overlap between annotators. As a result, each article was annotated by two members, yielding a total of 50 annotations. Among these, 36 annotations matched, resulting in an inter-annotator agreement of 72%. This annotated subset was used as a benchmark to evaluate various classification methods and establish an agreement metric.

The highest agreement with human annotations (72%) was achieved using the "Full Classification with LLaMa." However, a review of the assignments revealed that an excessively high number of articles (90%) were being classified, leading to potential overclassification. Some articles were misclassified because the system prompt provided the model with a list of all countries. This introduced a bias, leading the model to disproportionately classify articles under Afghanistan, as it appears first alphabetically in the list.

To address this, the system prompt was iteratively refined to enhance agreement accuracy. After achieving improved agreement values, the refined prompt was used to reclassify the entire dataset. In order to remove the biases due to the ordering of countries in the list the classification was run 2 times with two different orders and then only the matching assignments were kept.

The improved prompt is : 

<blockquote class="blockquote-content">
You will be given textual articles. For each article provide a single and unique country to which the article is related and should be classified to. Provide the answer in the form : country.<br/>
If the article is related to an object, a place, a monument related to a country, please write the country.<br/>
if the article is about a spieces, that lives in multiple countries, please write 'None'.<br/>
If there is no country related to the article, please write 'None'.<br/>
If the location is not on earth, please write 'None'.<br/>
If the article is a general article where the content is not specifically related to a country, please write 'None'.<br/>
You are allowed to use the article name to help you find the country.<br/>
This is the list of coutnries that you are allowed to output don't output anything that is not in this list: {countries}
</blockquote>

This refinement resulted in an improved agreement value of 78% while reducing the proportion of classified articles to 56%, addressing the issue of overclassification. This proportion of classified articles matches our expectations and is possibly still a bit high since in our annotation 41% of articles were not classified.
This final classification is then used for the whole project.

#### Downsides and limitations
- **Limited number of annotated articles** : The analysis was based on a relatively small sample of 36 annotated articles, which may result in imprecise agreement values. To improve the accuracy and reliability of the findings, a larger dataset of annotated articles would be necessary. However, due to time constraints, expanding the dataset or engaging additional human annotators was not feasible.
- **Small size of LLM** : The model used in this study was relatively small, which inherently limits its knowledge and performance. While larger language models are expected to perform better on such tasks, the decision to prioritize local execution and cost-effectiveness constrained the use of more powerful models.

</div>
</div>
</div>

<div class="col mb-4">
  <div class="card shadow" data-aos="fade-up">
    <div class="content p-4" style="height: 70vh">
          <div class="graph-title"> Figure 3: Agreement between annotators and classification method in %</div>
          <iframe class="graph" src="{{ '/graphs/preprocessing/agreement_bar_plot.html' | relative_url }}" ></iframe>
    </div>
  </div>
</div>

<div class="col mb-4">
<div class="card shadow" data-aos="fade-up">
<div class="content p-4" markdown="1">

#### Quantification of players’ behavior
To quantify the player’s behavior in the Wikispeedia game, we are interested in the way they *use* articles, meaning that we want to see if some articles are more *used* in the process of retrieving a target article from a source article. To quantify the *usage* of an article, we utilize the number of times an article is clicked (referred to as *click count* in our work). To calculate the *click count* per article we count the number of occurrences of an article in both finished and unfinished paths. 

\\[Click Count_{article} = \sum_{p=1}^{P} Occurrences_{article, p}\\]

As a reminder, a *path* corresponds to the sequence of articles that a player clicks in order to go from a given source article to a set target article. With our *click count* metric we can proxy article usage quite accurately. The higher the *click count* of an article, the more players used it and the bigger is the importance of this article (which importance does this correspond to? This we will find out!).

</div>
</div>
</div>

<div class="col mb-4">
<div class="card shadow" data-aos="fade-up">
<div class="content p-4" markdown="1">

#### Quantification of knowledge production 
We are using an external dataset from [Scimago Journal and Country Rank (SJR)](https://www.scimagojr.com/countryrank.php?year=2007) to approximate the worldwide knowledge production. SJR provides various rankings of journals or countries based on Scopus data [[4]](https://www.elsevier.com/products/scopus?dgcid=RN_AGCM_Sourced_300005030). For example, it contains the number of documents, the number of citable documents, or the number of citations per country and per year. In this project, we focus on the data from 2007 as the Wikispeedia game based on the Wikipedia data from that year. And, we keep exclusively the number of citable documents per country as it seems like the best proxy for knowledge production. 

</div>
</div>
</div>

</div>
