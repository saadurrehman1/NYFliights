# New York Fliights' Analysis

## Summary
For this project I acquired 10 years of data of flights operating out of New York state. The aim of this project was to analyze the historical data to uncover any trends and patterns that would help optimize airlines operations. 10 years of weather data of New York state was also acquired and analyzed to find any correlation between weather conditions and flights cancellations and delays. Different data analytical tools which include **R, Ms Azure, HDFS, Hive, and Tableau** were utilized for the completion of this project. The analysis revealed significant correlations between adverse weather conditions and increased flight delays, highlighted peak times and seasons with higher delay occurrences, and compared the performance of different airlines and airports. Based on these insights, I recommended implementing targeted operational strategies during peak seasons and adverse weather, enhancing passenger communication, investing in advanced weather forecasting tools, and standardizing delay management protocols across airlines and airports.

## Data Extraction
- Collected flight data of the past 10 years (2014-2023) from the Bureau of Transportation Statistics (BTS) as primary data. The data was obtained in the csv format.
  https://www.transtats.bts.gov/PREZIP/
  
  ![Picture1](https://github.com/saadurrehman1/NYFliights/assets/170811931/03672a96-2006-452e-82ff-adbf8274f0e5)


- Collected weather data of New York state over the same corresponding period from Mesonet as secondary data. This weather data was obtained in csv format as well.
  https://mesonet.agron.iastate.edu/request/download.phtml

## Data Transformation
- For cleaning and merging of the two datasets **R** was used.
- Given the sheer volume and size of the flights data, it was decided to use sparklyr. Sparklyr was used to create a cluster on the local machine which allowed for fast parallel processing of the data.
- Dplyr was used to read the two datasets into the program and perform data quality checks.

### Missing records
- Only variables which were important for the analysis were checked for missing values.
- It was found that the variable **DepTime** had missing values, but these missing values were less that the count of **cancelled flight**. This was not a cause of concern as flights which got cancelled would obviously have missing observations in **DepTime**.

  
