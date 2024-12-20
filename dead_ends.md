### What do we call a dead-end ?
Dead ends in the context of Wikipedia navigation are articles that players encounter but struggle to move forward from, leading to either backtracking or abandoning the path altogether. Understanding dead ends provides valuable insight into user behavior, article connectivity, and potential biases in navigation patterns. By identifying these points of friction, we can better interpret how graph structures and content influence player decisions.

In this analysis, we will:
1. **Identify countries as potential dead ends based on click counts and mean failure ratio (unique).** Are highly connected countries inherently more prone to becoming dead ends due to visibility and accessibility? Or are less-connected countries genuinely more challenging for navigation?
2. **Examine last articles in unfinished paths.** Which countries frequently appear at the end of failed navigation attempts? What does scaling these occurrences by outgoing links reveal about genuine dead ends versus highly connected hubs?
3. **Analyze backtracking behavior.** What countries or articles trigger backtracking, and how does scaling highlight less obvious dead ends that trap players?
4. **Explore the relationship between start/stop countries and back-click rates.** Do certain countries cause players to abandon paths more frequently, and how does this change depending on their position in the navigation sequence?


### Spotting Dead Ends Through Click Counts and Mean Failure Ratio
In this part, we sort the countries based on their click count and unique mean failure ratio. To calculate the unique failure ratio, we count each occurrence of a country in unfinished paths only once. This approach eliminates circular patterns and repeated entries, ensuring a clearer and more accurate representation of how often each country contributes to navigation failures.

Uh oh, this plot might be biased. Not only has the United States received an overwhelmingly high number of clicks, but it also has significantly more outgoing links (16,338) than other countries. This likely inflates its visibility and accessibility, making it appear more frequently in player paths. Familiarity bias (e.g., cultural or linguistic factors) further skews the data toward countries like the US and UK.
To reduce this bias, we scale the number of clicks by the sum of outgoing links per country. This reveals a more nuanced picture, where less-connected countries such as Greenland, Bolivia, Brazil emerge as significant dead ends. Scaling sheds light on genuine navigation patterns, helping us differentiate between structural biases and true player challenges.

### INSERT PLOT 1 TOP 10 dead end countries based on click count and failure ratio (graphs/topic_2/dead_ends_analysis1)

### 2. **Analyzing Last Article in Unfinished Paths: Which Countries Trap Players?**
What happens when a player’s navigation ends unsuccessfully? By analyzing the last articles in unfinished paths, we identify which countries are the most frequent dead ends. Initially, highly connected countries like the United States dominate this list, reflecting their prominence in raw data.

However, scaling by outgoing links tells a different story. Countries like Country1 and Country2 (doit re-run plot) emerge as true dead ends, suggesting specific navigational patterns or challenges that lead players to abandon these paths. These insights highlight the limitations of raw data in capturing genuine player behavior.

### INSERT PLOT 2 TOP 10 dead end countries based on last article count in unfinished paths (graphs/topic_2/dead_ends_analysis2)

### 3. **Backtracking Behavior: What Leads Players to Retreat?**
Before players give up, they often hit a point where they backtrack. By examining the most common articles preceding the “go back” action, we identify key friction points. Unsurprisingly, highly connected countries like the United States and United Kingdom dominate the raw data.

Scaling by outgoing links, however, reveals less obvious dead ends. Countries like French Polynesia and Vatican City, despite their limited connectivity, frequently prompt backtracking. This suggests players feel stuck due to limited onward options, making these articles true navigation roadblocks.

### INSERT PLOT 2 TOP 10 dead end countries based on last article count in unfinished paths (graphs/topic_2/dead_ends_analysis3)

### 4. **Start/Stop Countries and Back-Click Count Correlation**
Does the starting or stopping country influence back-click rates? By linking back-click occurrences to specific countries, we uncover patterns in player frustration. Highly connected hubs may dominate initial paths but also contribute to abandonment rates, while less-connected countries often create bottlenecks regardless of their position in the sequence. (analyse du graph après)

### INSERT PLOT 4 TOP 10 dead end countries based on Start/Stop Countries and Back-Click Count (graphs/topic_2/dead_ends_analysis4)

From our analysis, we observe that players are slightly biased in their navigation, often favoring culturally or linguistically familiar countries like the United States and the United Kingdom. However, when we scale by the number of outgoing links, we find that less-clicked countries, often representing regions with less content or visibility in Wikipedia, pose unique challenges to players. These countries emerge as significant dead ends, likely due to limited navigational options or insufficiently produced knowledge.

This finding reflects a broader truth: Wikipedia’s structure mirrors the global distribution of knowledge. Regions with richer knowledge production and connectivity are easier to navigate, while underrepresented areas create hurdles for users. By incorporating scaling and PageRank into our analysis, we can separate graph-induced biases from genuine navigational patterns, offering a clearer picture of the interplay between player behavior and the representation of global knowledge.