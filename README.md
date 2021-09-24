# etl-reddit-finance - Introduction

Extract, Transform, Load (ETL): This repository is my ETL process for extracting data from Reddit's API and combining it with the Python library yfinance (Yahoo Finance Stock Data). The goal is to automate the extraction process, the cleaning/transformation issues that may arise, and load the data into an SQL database (pgAdmin).

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

![Reddit_Raw_DataFrame](/images/subreddit_dataframe.png)

Here we see the DataFrame extracted from the Reddit API. I chose to only extract the title, date, upvote ratio, and total comments. 

Now we use the yfinance library to pull historical stock data. I wanted to keep this script modular, so the cell will grab the current date and get a year's worth of stock data. This can easily be change to a daily process, and thus this script can be ran daily to grab new posts from the subreddit as well as daily stock open/close/high/lows. Fantastic!

There are also some added checks to ensure the title has the requested keyword included. Sometimes the PRAW search results will grab relevant posts. However, we want posts that include GME in the title only. Thus, the script will drop those outliers. 


# Transformation

To make the data clean and database ready I will need to clean up the date time, and merge the two datasets together. The yfinance dataframe needed some work after being extracted. See below!

![yfinance_DataFrame](/images/yahoo_finance_extraction.png)

I had to .reset_index() for the yfinance DataFrame because there are multiple posts on a given day. Meaning, if 'Date' was the index there would be many posts that fall on one day sharing the same index. That's just messy, it's best to rest the index and create a unique number for each post. This is what I had done in the image above. 

![datetime_reddit](/images/dataframe_datetime.png)

Next I converted the 'Date' column to datetime. Now the two dataframes are ready to be merged. 

![merged_data](/images/final_merge.png)

Here is the final merged dataset. Now we can push to pgAdmin with SQLalchemy. 

# Load (SQL)

To load the data, I used SQLalchemy. I did this because the data was rather tabular and I had added cells beforehand that dropped null values and checked for compliant dataframe formatting. 

![sql_connection](/images/to_sql_database_complete.png)

![sql_connection](/images/pgadmin_test_query.png)

# Conclusion

My goal was to practice ETL, and I feel I have achieved that. The script is very modular and can easily pull more data to store it in differing tables within pgAdmin. The flexability and scalability is something I may explore in the future. 
