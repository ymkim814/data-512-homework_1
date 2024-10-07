# DATA512HW1

## The Goal of the project
The goal of this project is to understand how to call API and the trend of the view for different kinds of diseases depending on the different access methods. The project consists of API calling and saving, understanding JSON data format with a descriptive explanation of the data and process, analyzing the data to understand trends, and answering the questions relevant to disease pageviews in time series.

According to [Wikipedia Tou](https://foundation.wikimedia.org/wiki/Policy:Terms_of_Use), this homework follows their rules because it engages Wikimedia's informational pieces to understand and apply our academic learnings, not using any of the results or procedure to create harm for someone else and utilize the data responsibility while Wikimedia hosts them as API. Lastly, we are committing lawful behavior by putting appropriate licenses and not commercializing any of this.  

The documentation of API is in [Wikimedia Pageviews](https://wikimedia.org/api/rest_v1/#/Pageviews%20data) and the methods of accessing API in Wikimedia are located [Wikimedia REST API](https://www.mediawiki.org/wiki/Wikimedia_REST_API). The framework of wp_article_views_example was developed by Dr. David W. McDonald for use in DATA 512, a course in the UW MS Data Science degree program. This code is provided under the [Creative Commons](https://creativecommons.org) [CC-BY license](https://creativecommons.org/licenses/by/4.0/). Revision 1.3 - August 16, 2024.

## Setting
Regarding the setting, one can use requirement.yaml in this repository with this code
`````
conda env create -f my_conda.yaml
`````
Note: The 'requests' module is not a standard Python module. You will need to install this with pip/pip3 if you do not already have it.

## Data Used and Created 
rare-disease_monthly_desktop_201507-202409
Clearly name any intermediary data files and any final output files that your code creates. 
Json file and png files

For any files that your code creates you should provide a data schema and brief description

## Note
Since we use a subset of the disease using rare-disease_cleaned.AUG.2024.csv, the list of 1773 diseases might not be a comprehensive list of the whole data and biased. Also, there are some diseases that contain \ in it, making it hard to transform into clean text. Also, the time frame of the data is 20150701 - 20240930.
