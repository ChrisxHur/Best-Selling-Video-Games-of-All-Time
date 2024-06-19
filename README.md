# Best Selling Video Games of All Time Analysis

This data analysis projects aims at looking at historical video game sales data over 
the years. By analyzing this dataset, we hope to seek patterns and trends within 
sales data over time, make data-driven decisions, and gain a deeper understanding of
the video games market.

### Data Source
The data source has been taken from kaggle. It is the "best-selling videos of all time.csv" file.
The dataset shows all time video game sales from various platforms and publishers.

### Tools
- excel (original file)
- BigQuery SQL (data analysis)
- Tableau (create visualizations)

### Data Cleaning and Preperation
In preparing for data for analysis, these are the preparations to get the data ready:
- Data loading and inspection
- Check for duplicate entries using a CTE SQL query:

WITH duplicate_CTE AS
(
SELECT *,
ROW_NUMBER() OVER(
PARTITION BY 'rank', title, sales, series, platform, 'initial release date', developer, publisher) AS row_num
FROM best_selling_video_games.game_data
)

SELECT *
FROM duplicate_CTE
WHERE row_num > 1;

This resulted in finding 0 duplicate entries. Considering this was from kaggle, the data set was probably already cleaned.
But it is always good to make sure.
