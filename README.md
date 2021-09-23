# etl-reddit-finance

Extract, Transform, Load (ETL): This repository is my ETL process for extracting data from Reddit's API and combining it with the Python library yfinance (Yahoo Finance Stock Data). The goal is to automate the extraction process, the cleaning/transformation circumstances that may arise, and 

# Repository Structure

### Notebooks:

1.) [Main ETL Notebook](/assets/etl-reddit-finance.ipynb)

2.) [Markdown Report](/report/markdwon-report.ipynb)

3.) [Reddit API Practice](/assets/api_practice_notebook/etl-api-check.ipynb)

### Images (used in this README.md):

1.) [Images](/images)

# Extraction 

To navigate through the Reddit API and extract data I used the PRAW API wrapper. I put my API credentials into the object I had created (reddit_request), and this satisfied OAuth authentication. From there, I was able to pass through the subreddit of my choice. 

The subreddit variable can be changed to a different subreddit and will extract data. Thus, this system has some modularity and has the potential to become a standalone application for data collection.

![PRAW_Wrapper_Image](/images/PRAW_Subreddit_established.png)

# Transformation

# Load (SQL)

# Conclusion
