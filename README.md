# DATA 512 A2: Bias in Data

## Project Goal

The goal of this project is to look at possible biases in data. This notebook analyzes data from world population data in 2018, and wikipedia English article page on politicians. Check out the [ipynb file](https://github.com/apoorva-sh/data-512-a2/blob/master/hcds-a2-bias.ipynb) to see how the final data was generated, and the conclusions in the last section of the Readme were reached.

## Running the code

To run this code, clone the repository and in the project directory run the command `jupyter notebook`. Navigate to the .ipynb file in the jupyter console, and run the notebook to reproduce the results. 

## API Documentation
One API has been used in this project:

- [ORES](https://ores.wikimedia.org/v3/#!/scoring/get_v3_scores_context_revid_model) | This API categorizes articles as high quality or not using the wikipedia article ID

## Data Source
The Data used in this project is:

- Wikipedia English article information on politicians, found [here](https://figshare.com/articles/Untitled_Item/5513449)
- World population data as of mid - 2018, found [here](https://www.prb.org/international/indicator/population/table/)

## Data Description

### Raw Data
The raw data files [WPDS_2018_data](https://github.com/apoorva-sh/data-512-a2/blob/master/data/raw_data/WPDS_2018_data.csv) and [page_data](https://github.com/apoorva-sh/data-512-a2/blob/master/data/raw_data/page_data.csv) have the following data:

1) WPDS_2018_data : Population data by country in millions

| Column Name | Description | Data type|
|-------------|-------------|------------|
| Geography | Country name | object |
| Population mid-2018 (millions) | Population for that country in millions | object|

2) page_data : political article data in English

| Column Name | Description | Data type|
|-------------|-------------|------------|
| country | Country name | object |
| page | Article name | object|
| rev_id | Article ID | int |

### Generated Data
During the data cleaning and consolidation step, 6 data files were generated:

1) [clean_politicle_article_data](https://github.com/apoorva-sh/data-512-a2/blob/master/data/raw_data/clean_politicle_article_data.csv) : No template data is included in this cleaned version of page_data

| Column Name | Description | Data type|
|-------------|-------------|------------|
| country | Country name | object |
| page | Article name | object|
| rev_id | Article ID | int |

2) [clean_population_data](https://github.com/apoorva-sh/data-512-a2/blob/master/data/raw_data/clean_population_data.csv) : No cumulative data is included in this version of population data

| Column Name | Description | Data type|
|-------------|-------------|------------|
| Geography | Country name | object |
| Population mid-2018 (millions) | Population for that country in millions | object|

3) [cumulative_population](https://github.com/apoorva-sh/data-512-a2/blob/master/data/raw_data/cumulative_population.csv) : This csv only contains region specific population data for each country.

| Column Name | Description | Data type|
|-------------|-------------|------------|
| Geography | Country name | object |
| Population mid-2018 (millions) | Population in a region of that country in millions | object|

4) [quality_prediction](https://github.com/apoorva-sh/data-512-a2/blob/master/data/raw_data/quality_prediction.csv) :
This csv contains the ORES quality categorization for an article

| Column Name | Description | Data type|
|-------------|-------------|------------|
| rev_id | Article ID | int |
| prediction | ORES quality categorization | object|

5) [wp_wpds_countries-no_match](https://github.com/apoorva-sh/data-512-a2/blob/master/data/raw_data/wp_wpds_countries-no_match.csv) : All countries that either belonged to the population data or the political article data but not in both are stored in this csv (All countried excluded from the Analysis)

| Column Name | Description | Data type|
|-------------|-------------|------------|
| countries | Country name | object |

6) [wp_wpds_politicians_by_country](https://github.com/apoorva-sh/data-512-a2/blob/master/data/raw_data/wp_wpds_politicians_by_country.csv) : This csv contains the final merged data that is used for analysis in the jupyter notebook

| Column Name | Description | Data type|
|-------------|-------------|------------|
| country | Country name | object |
| page | Article name | object|
| rev_id | Article ID | int |
| Population mid-2018 (millions) | Population for that country in millions | object|
| prediction | ORES quality categorization | object|


## Conclusion and Reflections
### Take away from this project
- Data overlaps in a multitude of ways, and looking at your data from a singular point of view can hide the overall picture the data can draw.  
- Documenting your thought process can be more difficult than it seems. Some workflows seem natural to me, but I found myself over-explaining simple steps, which probably isn't the greatest approach but maybe better than just code without explanation

### Analysis conclusions
- On reading the problem statement, the idea of looking at population proportion to wikipedia articles seemed interesting to me, the idea that having a large populous could affect the number of political articles generated from that area seemed implausible to me. On looking at the lowest ranked countries by article to population ratio, I did find that incredibly higher populated countries did skew this data, countries like China, India and Indonesia both had an incredibly high population and as a function of that had very low article to population percentage. A future researcher could maybe filter out the heavy hitters in terms of population to get a better understanding of article to population ratio.
- Looking at the overall number of high quality articles, it is seen that countries with English as their native langauge did rank high in that department alone, however looking at the percentages these countries don't even appear in the top ten which was interesting to me, I guess countries with politically heavy climates with few articles (WELL WRITTEN HOWEVER) ranked higher when looking at the percentages.

### Other possible sources of bias
- Reading into the [ORES documentation](https://www.mediawiki.org/wiki/ORES), an interesting point in how an article is categorized as "good quality" is mentioned [here](https://www.mediawiki.org/wiki/ORES#Assessment_scale_support), this model seems more concerned about the structural soundness of an article in contrast to it's tone or vocabulary, which seemed a little problematic to me. A high quality article need not just be well cited, there is scope for a lot of false positives in such a situation.
- Finally, the political article data is just taken from English articles which may reduce the overall article count and miss out on other "high quality" non-english articles. (This could affect non-English speaking countries' score for high quality article ratio.

## Licenses

- The Source Code is under the [MIT License](https://github.com/apoorva-sh/data-512-a2/blob/master/LICENSE)
- Wikipedia English-language political data is under the [CC BY 4.0 LICENSE](https://creativecommons.org/licenses/by/4.0/)

