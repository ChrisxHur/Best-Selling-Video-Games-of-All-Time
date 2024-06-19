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

```
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
```

This resulted in finding 0 duplicate entries. Considering this was from kaggle, the data set was probably already cleaned.
But it is always good to make sure.

- Data cleaning and formatting
  formatting and spacing seems to be good using SELECT DISTINCT queries and observing the dataset
- handling missing values
  There are some missing values; however, we will not be using those specific values for this analysis

### Exploratory Data Analysis
Exploring the data to answer a few key questions:
- What are the most sold video games of all time
- What platform has to most sales? Does multi-platform contribute to higher sales?
- Which publisher has the most success in video games sales?
- over time, which publisher has had the most success?

### Data Analysis

To find the top 10 highest sold video games by copies sold:

```
SELECT *
FROM best_selling_video_games.game_data
ORDER BY sales DESC
LIMIT 10;
```

Results are shown here:

![top10_games_sold](https://github.com/ChrisxHur/Best-Selling-Video-Games-of-All-Time/assets/173302585/daf40832-5a62-4b90-9921-3b816c5633cf)

To find the top platforms by total sales:

```
SELECT 
  platform,
  sum(sales) AS total_sales
FROM best_selling_video_games.game_data
GROUP BY platform
ORDER BY total_sales DESC;
```

Results are shown here:

![top_platform_sales](https://github.com/ChrisxHur/Best-Selling-Video-Games-of-All-Time/assets/173302585/f8657c2c-981f-4a21-b778-3eabf44a59cc)

Lastly, we find the top publishers by total sales:

```
SELECT
  publisher,
  SUM(sales) AS total_sales
FROM best_selling_video_games.game_data
GROUP BY publisher
ORDER BY total_sales DESC;
```

Results are shown here:

![top_publishers](https://github.com/ChrisxHur/Best-Selling-Video-Games-of-All-Time/assets/173302585/8d2750ee-4ec5-482f-b380-3e3229e87d6b)


### Results and Findings
1. Minecraft remains the top selling video game of all time, far exceding the previous title (GTA 5) by over 60 million copies sold
2. Titles released in multi-platforms generally see the most success in video game copies sold. When it comes to indivdual platforms,
wii seems to have the most games sold. If you want to maximize the amount of sales, it is best to release titles for multiple platforms.
3. Nintendo is by far the publisher with the highest amount of total sales, followed by Rockstar Games, and then Xbox Game Studios.
