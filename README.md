# Home_Sales
While dealing with relatively large dataset to receive some insights about home sales, SparkSQL was used to optimize data processing. Three experiments were made to see if caching the data or using a columnar storage format (parquet) could improve processing time.
## Summary
#### Data analysis
Having data for homes sold in 2019-2022 years, 4 bedrooms homes have pretty similar average price per year sold, which is close to 300K. It does not seem there is a correlation between average price and the year it was sold.<br>
Homes with 3 bed/bathrooms:
 - we only have data for homes built in 2010-2017,
 - average price is around 289K-296K, and 277K-308K if filtered by 2 floors and more than 2K square feet,
  - homes built in 2012-2013, with or without filtering by floors and square feet, have the highest prices in average.

Homes with highest views count are those groups with average price around 1M.

#### Runtime comparison
Running the same query, which looks for home prices grouped by views count, with average home price within the group greater then or equal to 350K, three data storage approaches were used:
 - temporary table of the original DataFrame created reading csv file,
 - cached data,
 - data partition by the field, which represents built date, and stored in parquet format.
   
The following output was received:

<p align="center">
<img src="https://github.com/ValentynaK17/Home_Sales/blob/main/Runtime_Comparison.png" width=“275">
</p>

The best runtime we received using cached data. However parquet format also showed improved runtime, comparing to one from temporary table of the original DataFrame. The reason experiment with parquet format didn’t show the runtime which stands out, can be related to the data being partitioned by the field which wasn't really used in data filtering.

## Installation
 Having Jupyter Notebook available, clone this repository to your local machine
 
## Usage
 Run the **Home_Sales_colab.ipynb** scripts using Jupyter Notebook

