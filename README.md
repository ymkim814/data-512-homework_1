# DATA512HW1

## The Goal of the project
The goal of this project is to understand how to call API and the trend of the view for different kinds of diseases depending on the different access methods. The project consists of API calling and saving, understanding JSON data format with a descriptive explanation of the data and process, analyzing the data to understand trends, and answering the questions relevant to disease pageviews in time series. This is also an exercise for assessing and carrying out reproducibility of the code based on the API calling framework code.

According to [Wikipedia Terms of Use](https://foundation.wikimedia.org/wiki/Policy:Terms_of_Use), this homework follows their rules because it engages Wikimedia's informational pieces to understand and apply our academic learnings, not using any of the results or procedure to create harm for someone else and utilize the data responsibility while Wikimedia hosts them as API. Lastly, we are committing lawful behavior by putting appropriate licenses and not commercializing any of this.  

The documentation of API is in [Wikimedia Pageviews](https://wikimedia.org/api/rest_v1/#/Pageviews%20data) and the methods of accessing API in Wikimedia are located [Wikimedia REST API](https://www.mediawiki.org/wiki/Wikimedia_REST_API). Information about customizing pageview using URL and API is located [here](https://doc.wikimedia.org/generated-data-platform/aqs/analytics-api/reference/page-views.html). The framework of wp_article_views_example was developed by Dr. David W. McDonald for use in DATA 512, a course in the UW MS Data Science degree program. This code is provided under the [Creative Commons](https://creativecommons.org) [CC-BY license](https://creativecommons.org/licenses/by/4.0/). Revision 1.3 - August 16, 2024.

## Setting
Regarding the setting, one can use requirement.yaml in this repository with this code
`````
conda env create -f my_conda.yaml
`````
Note: The 'requests' module is not a standard Python module. You will need to install this with pip/pip3 if you do not already have it.

## Data Used and Created 
The data we used is named rare-disease_cleaned.AUG.2024.csv, which contains the article (name of the disease) and URL of the WikiMedia Page and came from the [National Organization for Rare Disease](https://rarediseases.org/). It narrows down the list of API calls. Based on the article list, we called API to collect 3 different JSON files of pageviews which consist of 
`````
'project', 'article', 'granularity', 'timestamp', 'agent', and 'views.
`````
Note: We collected data where the agent = user.

**rare-disease_monthly_desktop_201507-202409** collected the pageviews of articles that used desktop access from 2015, July to 2024, September. 
**rare-disease_monthly_mobile_201507-202409** collected the pageviews of articles that used either web-mobile or app-mobile access from 2015, July to 2024, September. 
**rare-disease_monthly_cumulative_201507-202409** collected the pageviews of articles that used either desktop, web-mobile, or app-mobile access access from 2015, July to 2024, September. This is the sum of the views of desktop and mobile JSON files.

Then we read those files to make them into a pandas data frame. This is an important intermediate procedure since we call the created JSON files instead of calling API for every time to save time and efficiency. First, we use 
`````
# Load the JSON data from both desktop and mobile views
with open('rare-disease_monthly_desktop_201507-202409.json', 'r') as desktop_file:
    desktop_data = json.load(desktop_file)

with open('rare-disease_monthly_mobile_201507-202409.json', 'r') as mobile_file:
    mobile_data = json.load(mobile_file)
`````
In the processing procedure, we added a 'month' column to make labeling easier for visualization.

`````
def process_data(json_data):
    df_list = []
    for disease, entries in json_data.items():
        temp_df = pd.json_normalize(entries)
        df_list.append(temp_df)
    df = pd.concat(df_list, ignore_index=True)
    df['timestamp'] = pd.to_datetime(df['timestamp'], format='%Y%m%d%H')
    df['month'] = df['timestamp'].dt.to_period('M')
    return df

# Process desktop and mobile data
desktop_df = process_data(desktop_data)
mobile_df = process_data(mobile_data)
`````
With **desktop_df**a nd **mobile_df**, we created three different visualizations. Each visualization distinguishes desktop and mobile access by having different styles of line - straight and dotted lines. Matplotlib library is used.
1) Maximum Average and Minimum Average - Plots articles with maximum and minimum average page views for desktop and mobile access, having 4 different time series. 
2) Top 10 Peak Page Views - Plots articles with top 10 Peak page views for desktop and mobile access, having 20 different time series.
3) Fewest Months of Data - Plots articles with the top 10 fewest months of available data, for desktop and mobile access, having 20 different time series.
 
All plots were saved as .png file in the same folder of notebook file using the code below and can be viewed in the **PageView Visualization** folder in this repository.
`````
plt.savefig('highest_lowest_average_page_requests.png')
`````

## Note
Since we use a subset of the disease using rare-disease_cleaned.AUG.2024.csv, the list of 1773 diseases might not be a comprehensive list of the whole data and biased. Also, there are some diseases that contain \ in it, making it hard to transform into clean text. Also, the time frame of the data is 20150701 - 20240930.

## The MIT License
License: MIT
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
