# DATA 512 A2: Bias in Data

## Project Goal

The goal of this project is to look at possible biases in data. This notebook analyzes data from world population data in 2018, and wikipedia English article page on politicians. Check out the [ipynb file](https://github.com/apoorva-sh/data-512-a2/blob/master/hcds-a2-bias.ipynb) to run this project/ see how the data was generated.

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

## License

- The Source Code is under the [MIT License](https://github.com/apoorva-sh/data-512-a2/blob/master/LICENSE)
- Wikipedia English-language political data is under the [CC BY 4.0 LICENSE](https://creativecommons.org/licenses/by/4.0/)

