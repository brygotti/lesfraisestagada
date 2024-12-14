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

<div class="alert alert-success">
    <strong>First glance at the distribution of knowledge worldwide :</strong> <br />
    - Assign a country to each article <br />
    - Try different methods and see how many articles can be classified <br />
    - Verify these classification with human annotation <br />
    - Select the best method for further analysis of the dataset <br />
</div>

<div class="alert alert-warning">
  <strong>Countries :</strong>
  In order to classify countries we used the standard ISO list with 249 countries and the following distribution: <br />
  - UN Members: 193 <br />
  - UN Observer States: 2 <br />
  - States With Partial Recognition: 2 <br />
  - Inhabited Dependent Territories: 45 <br />
  - Uninhabited Territories: 6 <br />
  - Antarctica: 1 <br />
</div>

A naïve method was employed to classify articles to specific countries by performing a text search to identify occurrences of country names within the plaintext. This approach utilized basic regular expression matching to analyze the articles. However, it resulted in approximately 31% of the articles (1,412 out of 4,604) remaining unclassified, highlighting significant limitations.

#### Identified Issues with the Approach
1. **Over-classification on mentioned country names**: 
   The presence of a country name in an article does not necessarily imply that the article belongs to that country. This assumption leads to inaccuracies in classification.

2. **Lack of contextual understanding**: 
   The text search method lacks the ability to discern the context in which a country name appears, resulting in potential misclassifications.

3. **Observations**: 
   A review of the articles revealed a lot of incorrect or missing classifications. For example:
   - The article *13th Century* was misclassified under China due to mentions of events occurring there during that period, despite the article lacking any specific association with China.
   - Conversely, the article *4-2-0*, which details a type of railroad in the United States, was left unclassified despite its clear association with that country.

These findings show the limitations of the current text-matching methodology and highlight the need for a more robust, context-aware approach to accurately classify articles.

</div>
</div>
</div>

<div class="col mb-4">
<div class="card shadow" data-aos="fade-up">
<div class="content p-4">
<iframe class="graph" src="{{ '/graphs/proportion_country_assignment.html' | relative_url }}" ></iframe>
</div>
</div>
</div>

<div class="col mb-4">
<div class="card shadow" data-aos="fade-up">
<div class="content p-4">
<iframe class="graph" src="{{ '/graphs/overlap_heatmap.html' | relative_url }}" ></iframe>
</div>
</div>
</div>

<div class="col mb-4">
<div class="card shadow" data-aos="fade-up">
<div class="content p-4" markdown="1">

Given the limitations of the initial text-search-based approach, a decision was made to use Large Language Models (LLMs) to enhance the article classification process. LLMs, with their extensive general knowledge, have the capability to analyze articles and respond to queries with a deeper understanding. 

Unlike simple text searches, LLMs not only utilize the content of the article but also incorporate their pre-existing (trained) knowledge. This contextual understanding should enables more accurate classification.

By employing LLMs, two potential strategies can be pursued:
1. **Targeted classification of previously unclassified articles**: The 1,412 articles that remained unclassified under the initial approach can be reevaluated, allowing for a significant reduction in the unclassified proportion. After this step only 6% (283 out of 4604) were not classified.

2. **Full Reclassification**: LLMs can be used to perform a complete reclassification of all articles, eliminating the biases and limitations inherent in the original text-search methodology. In order to test this two existing LLMs were used : [LLaMa](https://www.llama.com/) and [Qwen](https://qwen-ai.com/). These powerful models, with less than 8 billion parameters, offer significant computational efficiency and can be run locally on consumer hardware, making them accessible and cost-effective solutions compared to bigger models like ChatGPT and their paid API.

This transition to LLM-based classification is expected to significantly improve the accuracy and reliability of the country assignment process.

The prompt used in order to make the models classify the articles was the following : 

```
You will be given textual articles. For each article provide a single and unique country to which the article is related and should be classified to. Provide the answer in the form : country.
If there is no country related to the article, please write 'None'. 
If the location is not on earth, please write 'None'. 
If the article is a general article where the content is not specifically related to a country, please write 'None'.
You must be 100\% sure this is a question of life.
This is the list of coutnries that you are allowed to output don't output anything that is not in this list: {countries}
```
</div>
</div>
</div>


<div class="col mb-4">
<div class="card shadow" data-aos="fade-up">
<div class="content p-4" markdown="1">

To test the accuracy of the model’s predictions compared to human judgment, each member of the group manually annotated 20 articles, with a 10-article overlap between annotators. As a result, each article was annotated by two members, yielding a total of 50 annotations. Among these, 36 annotations matched, resulting in an inter-annotator agreement of 72%. This annotated subset was used as a benchmark to evaluate various classification methods and establish an agreement metric.

The highest agreement with human annotations (72%) was achieved using the "Full Classification with LLaMa." However, a review of the assignments revealed that an excessively high number of articles (90%) were being classified, leading to potential overclassification.

To address this, the system prompt was iteratively refined to enhance agreement accuracy. After achieving improved agreement values, the refined prompt was used to reclassify the entire dataset.

The improved prompt is : 

```
You will be given textual articles. For each article provide a single and unique country to which the article is related and should be classified to. Provide the answer in the form : country. 
If the article is related to an object, a place, a monument related to a country, please write the country.
if the article is about a spieces, that lives in multiple countries, please write 'None'.
If there is no country related to the article, please write 'None'. 
If the location is not on earth, please write 'None'. 
If the article is a general article where the content is not specifically related to a country, please write 'None'.
You are allowed to use the article name to help you find the country.
This is the list of coutnries that you are allowed to output don't output anything that is not in this list: {countries}
```

This refinement resulted in an improved agreement value of 86% while reducing the proportion of classified articles to 71%, addressing the issue of overclassification.
This final classification is then used for the whole project.

#### Downsides and limitations
- **Limited number of annotated articles** : The analysis was based on a relatively small sample of 36 annotated articles, which may result in imprecise agreement values. To improve the accuracy and reliability of the findings, a larger dataset of annotated articles would be necessary. However, due to time constraints, expanding the dataset or engaging additional human annotators was not feasible.
- **Small size of LLM** : The model used in this study was relatively small, which inherently limits its knowledge and performance. While larger language models are expected to perform better on such tasks, the decision to prioritize local execution and cost-effectiveness constrained the use of more powerful models.

</div>
</div>
</div>

<div class="col mb-4">
<div class="card shadow" data-aos="fade-up">
<div class="content p-4">
<iframe class="graph" src="{{ '/graphs/agreement_bar_plot.html' | relative_url }}" ></iframe>
</div>
</div>
</div>

<div class="col mb-4">
<div class="card shadow" data-aos="fade-up">
<div class="content p-4" markdown="1">

#### Assessment of article connectivity
Articles do not exist alone in Wikipedia. Indeed, they are all, to a certain extent, connected to each other through the links that they contain. To assess an article’s connectivity we calculated the number of links that lead in and out of it, respectively referred to as *num_links_in* and *num_links_out*. To find the number of links out of an article we simply counted the number of links contained in that article (24 in the example below). To find to number of links that lead into an article, we counted the number of times that article occurs in other articles (for example, North America appears in the example article below so this makes +1 to the *num_links_in count* of the North America article). 


#### Quantification of players’ behavior
To quantify the player’s behavior in the Wikispeedia game, we are interested in the way they *use* articles, meaning that we want to see if some articles are more *used* in the process of retrieving a target article from a source article. To quantify the *usage* of an article, we utilize the number of times an article is clicked (referred to as *click count* in our work). To calculate the *click count* per article we count the number of occurrences of an article in both finished and unfinished paths. 

$$Click Count_{article} = \sum_{p=1}^{P} Occurrences_{article, p}$$

As a reminder, a *path* corresponds to the sequence of articles that a player clicks in order to go from a given source article to a set target article. With our *click count* metric we can proxy article usage quite accurately. The higher the *click count* of an article, the more players used it and the bigger is the importance of this article (which importance does this correspond to? This we will find out!). 


#### Quantification of knowledge production 
</div>
</div>
</div>

</div>
