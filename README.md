# New York Flights' Analysis

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

### 1. Missing records
- Only variables which were important for the analysis were checked for missing values.
- It was found that the variable **DepTime** had missing values, but these missing values were less that the count of **cancelled flight**. This was not a cause of concern as flights which got cancelled would obviously have missing observations in **DepTime**.

![Picture5](https://github.com/saadurrehman1/NYFliights/assets/170811931/7f58a75b-cd09-4676-992e-e29cde1f89e9)
![Picture3](https://github.com/saadurrehman1/NYFliights/assets/170811931/0ba0270c-bad2-40e9-8394-293fc410261d)

### 2. Out of range values

![Picture4](https://github.com/saadurrehman1/NYFliights/assets/170811931/717482ed-824d-4a35-a410-5d5b2325b7aa)

### 3. Multiple Fields within a field
- It was found that there was one variable each in flights and weather dataset which had multiple fields within a field. It was important to address this issue here because it would have caused problems later on when hive tables would be populated using comma delimitation.
- For flights data, I only extracted the city name to overwrite this variable.
  
![Picture6](https://github.com/saadurrehman1/NYFliights/assets/170811931/400a94d7-4021-4093-b9c6-5a407fb6db1e)
![Picture7](https://github.com/saadurrehman1/NYFliights/assets/170811931/b8a06551-06eb-48d7-9b7b-cf708ce9cbf7)

- For weather data, the **valid** timestamp variable was aplit into **date** and **time** variable which qould later be used for merging the two datasets.
  
![Picture8](https://github.com/saadurrehman1/NYFliights/assets/170811931/b6bb4605-8401-401f-85da-ef5078bafd60)
![Picture9](https://github.com/saadurrehman1/NYFliights/assets/170811931/4a1cf426-540d-4359-a5e9-e0929ec98831)

### 4. Data Merging
- Three variables were identified to merge the two datasets, flight and weather. By using type casting, it was ensured that the three variables were of the same data type, and they were then used to perform a left join of the weather data on the flights data.
- **Origin** variable in the flights data is the same variable as **station** variable in the weather data, it represents the location.
- Common identifiers:

![Picture10](https://github.com/saadurrehman1/NYFliights/assets/170811931/a7d9ed12-c4f2-4938-a148-05186fdc7118)
![Picture11](https://github.com/saadurrehman1/NYFliights/assets/170811931/3758a5a4-3980-4e12-9b05-3915c6ac6a1b)

## Data Storage
- Stored the cleaned and merged dataset in HDFS on Microsoft Azure for scalability and accessibility
- Created a data mart using Hive to organize and manage the big data, utilizing HiveQL to make the process of querying the data time efficient.

![Picture12](https://github.com/saadurrehman1/NYFliights/assets/170811931/974576f8-f68f-40bb-80d8-9c2d2179236f)

## Data Visualization
- Connected Hive to Tableau to perform the visualizations and analysis using hive tables.
  
