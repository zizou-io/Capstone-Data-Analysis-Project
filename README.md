# Data-Analysis-Project

<img src="https://imgur.com/d3mpvsy.png">

## Introduction 

As part of the ```Google Data Analytics Professional Certificate Course```, I am required to act as a ***marketing analyst*** at Cyclistic, a bike-sharing company in Chicago.

## About Cyclistics  
Cyclistic is a ***bike-share company*** in Chicago which offers reclining bikes, hand tricycles, and cargo bikes, making bike-share more inclusive to cater for people from all walks of life. The company believes the company's future success depends on maximizing the number of annual memberships. Therefore, they want to ***understand how ```casual riders``` and ```annual members``` use Cyclistic bikes differently***, and use this insight to guide their coming ***marketing strategy.***

## Method Approach    
1. Ask - formulating business question 
2. Prepare - choosing the suitable datasets 
3. Process - ensuring the quality of datasets 
4. Analyze - extracting insights from cleaned datasets 
5. Share - transforming it into interactive formats 
6. Act - suggesting actionable ideas that help to solve business problems

## Phase 1: Ask    
#### 1.1: Business Task:    

1. How do casual users and annual subscribed members use Cyclistic Bikes differently?
2. How can we design new marketing strategies to help convert casual members into annual members?

## Phase 2: Prepare   
#### 2.1: Dataset Summary

These 12 datasets are the bike user historical trip data in 2021. Each dataset contains the number of cyclistic bike user and their riding distance and places.Each file represents different month of rider data.
|Dataset Table|Information|
|------------:|-----------|
|tripdata_202101|Rider Information of 96,831 users in January, contains rider_id, rideable_type, started_at, ended_at, start_station, end_station,start_station_id, end_station_id, member_casual, ride_length|
|tripdata_202102|Rider Information of 96,831 users in February|
|tripdata_202103|Rider Information of 96,831 users in March|
|tripdata_202104|Rider Information of 96,831 users in April|
|tripdata_202105|Rider Information of 96,831 users in May|
|tripdata_202106|Rider Information of 96,831 users in June|
|tripdata_202107|Rider Information of 96,831 users in July|
|tripdata_202108|Rider Information of 96,831 users in August|
|tripdata_202109|Rider Information of 96,831 users in September|
|tripdata_202110|Rider Information of 96,831 users in October|
|tripdata_202111|Rider Information of 96,831 users in November|
|tripdata_202112|Rider Information of 96,831 users in December| 

<sub> The cyclistic user's datasets are published by  Motivate International Inc. </sub>

#### 2.2: Dataset Limitations and Integrity    
<sub> The collected data has 12 months (January 2021 - December 2021) and a large number of user data are collected in this study.</sub>

## Phase 3. Process 
   
In this project, I choose ```MySQL``` database as a storage to process datasets, and ```Tableau``` as a data visualization tool. To begin with the data cleaning process, I load twelve datasets into a database server. 

I observed that each table has the same type of columns across twelve datasets so I have to merge all 12 tables into one and convert date format. 

<sub> NOTE: the start_station_id column of the dataset from Dec 2020 to April 2020 contains string values </sub>

#### 3.1 Importing Datasets 

Due to the large file size (1 million data points), I use the ```Load Data Infile `` command to load all datasets into MySQL database.

```SQL   
--- January---
CREATE TABLE tripdata_202101 (ride_id VARCHAR(225) ,rideable_type TEXT, started_at VARCHAR(225),ended_at VARCHAR(225),start_station_name VARCHAR(225),start_station_id VARCHAR(225),end_station_name VARCHAR(225),
end_station_id TEXT,start_lat VARCHAR(225),start_lng VARCHAR(225),end_lat VARCHAR(225), end_lng VARCHAR(225),member_casual TEXT ,ride_length VARCHAR(225),day_of_week INT);
LOAD DATA INFILE 'C:\\ProgramData\\MySQL\\MySQL Server 8.0\\Uploads\\Cyclistic.XLS\\202101-divvy-tripdata.csv'
INTO TABLE tripdata_202101
FIELDS TERMINATED BY ','
ENCLOSED BY ""
LINES TERMINATED BY '\n'
IGNORE 1 ROW; 

---February---
CREATE TABLE tripdata_202102 (ride_id VARCHAR(225) ,rideable_type TEXT, started_at VARCHAR(225),ended_at VARCHAR(225),start_station_name VARCHAR(225),start_station_id VARCHAR(225),end_station_name VARCHAR(225),
end_station_id TEXT,start_lat VARCHAR(225),start_lng VARCHAR(225),end_lat VARCHAR(225), end_lng VARCHAR(225),member_casual TEXT ,ride_length VARCHAR(225),day_of_week INT);

LOAD DATA INFILE 'C:\\ProgramData\\MySQL\\MySQL Server 8.0\\Uploads\\Cyclistic.XLS\\202102-divvy-tripdata.csv'
INTO TABLE tripdata_202102
FIELDS TERMINATED BY ','
ENCLOSED BY ""
LINES TERMINATED BY '\n'
IGNORE 1 ROW; 

---March---
CREATE TABLE tripdata_202103 (ride_id VARCHAR(225) ,rideable_type TEXT, started_at VARCHAR(225),ended_at VARCHAR(225),start_station_name VARCHAR(225),start_station_id VARCHAR(225),end_station_name VARCHAR(225),
end_station_id TEXT,start_lat VARCHAR(225),start_lng VARCHAR(225),end_lat VARCHAR(225), end_lng VARCHAR(225),member_casual TEXT ,ride_length VARCHAR(225),day_of_week INT);
LOAD DATA INFILE 'C:\\ProgramData\\MySQL\\MySQL Server 8.0\\Uploads\\Cyclistic.XLS\\202103-divvy-tripdata.csv'
INTO TABLE tripdata_202103
FIELDS TERMINATED BY ','
ENCLOSED BY ""
LINES TERMINATED BY '\n'
IGNORE 1 ROW; 

---April---
CREATE TABLE tripdata_202104 (ride_id VARCHAR(225) ,rideable_type TEXT, started_at VARCHAR(225),ended_at VARCHAR(225),start_station_name VARCHAR(225),start_station_id VARCHAR(225),end_station_name VARCHAR(225),
end_station_id TEXT,start_lat VARCHAR(225),start_lng VARCHAR(225),end_lat VARCHAR(225), end_lng VARCHAR(225),member_casual TEXT ,ride_length VARCHAR(225),day_of_week INT);
LOAD DATA INFILE 'C:\\ProgramData\\MySQL\\MySQL Server 8.0\\Uploads\\Cyclistic.XLS\\202104-divvy-tripdata.csv'
INTO TABLE tripdata_202104
FIELDS TERMINATED BY ','
ENCLOSED BY ""
LINES TERMINATED BY '\n'
IGNORE 1 ROW; 

---May---
CREATE TABLE tripdata_202105 (ride_id VARCHAR(225) ,rideable_type TEXT, started_at VARCHAR(225),ended_at VARCHAR(225),start_station_name VARCHAR(225),start_station_id VARCHAR(225),end_station_name VARCHAR(225),
end_station_id TEXT,start_lat VARCHAR(225),start_lng VARCHAR(225),end_lat VARCHAR(225), end_lng VARCHAR(225),member_casual TEXT ,ride_length VARCHAR(225),day_of_week INT);
LOAD DATA INFILE 'C:\\ProgramData\\MySQL\\MySQL Server 8.0\\Uploads\\Cyclistic.XLS\\202102-divvy-tripdata.csv'
INTO TABLE tripdata_202105
FIELDS TERMINATED BY ','
ENCLOSED BY ""
LINES TERMINATED BY '\n'
IGNORE 1 ROW; 

---June---
CREATE TABLE tripdata_202106 (ride_id VARCHAR(225) ,rideable_type TEXT, started_at VARCHAR(225),ended_at VARCHAR(225),start_station_name VARCHAR(225),start_station_id VARCHAR(225),end_station_name VARCHAR(225),
end_station_id TEXT,start_lat VARCHAR(225),start_lng VARCHAR(225),end_lat VARCHAR(225), end_lng VARCHAR(225),member_casual TEXT ,ride_length VARCHAR(225),day_of_week INT);
LOAD DATA INFILE 'C:\\ProgramData\\MySQL\\MySQL Server 8.0\\Uploads\\Cyclistic.XLS\\202102-divvy-tripdata.csv'
INTO TABLE tripdata_202106
FIELDS TERMINATED BY ','
ENCLOSED BY ""
LINES TERMINATED BY '\n'
IGNORE 1 ROW; 

---July---
CREATE TABLE tripdata_202107 (ride_id VARCHAR(225) ,rideable_type TEXT, started_at VARCHAR(225),ended_at VARCHAR(225),start_station_name VARCHAR(225),start_station_id VARCHAR(225),end_station_name VARCHAR(225),
end_station_id TEXT,start_lat VARCHAR(225),start_lng VARCHAR(225),end_lat VARCHAR(225), end_lng VARCHAR(225),member_casual TEXT ,ride_length VARCHAR(225),day_of_week INT);
LOAD DATA INFILE 'C:\\ProgramData\\MySQL\\MySQL Server 8.0\\Uploads\\Cyclistic.XLS\\202102-divvy-tripdata.csv'
INTO TABLE tripdata_202107
FIELDS TERMINATED BY ','
ENCLOSED BY ""
LINES TERMINATED BY '\n'
IGNORE 1 ROW; 

---August---
CREATE TABLE tripdata_202108 (ride_id VARCHAR(225) ,rideable_type TEXT, started_at VARCHAR(225),ended_at VARCHAR(225),start_station_name VARCHAR(225),start_station_id VARCHAR(225),end_station_name VARCHAR(225),
end_station_id TEXT,start_lat VARCHAR(225),start_lng VARCHAR(225),end_lat VARCHAR(225), end_lng VARCHAR(225),member_casual TEXT ,ride_length VARCHAR(225),day_of_week INT);

LOAD DATA INFILE 'C:\\ProgramData\\MySQL\\MySQL Server 8.0\\Uploads\\Cyclistic.XLS\\202102-divvy-tripdata.csv'
INTO TABLE tripdata_202108
FIELDS TERMINATED BY ','
ENCLOSED BY ""
LINES TERMINATED BY '\n'
IGNORE 1 ROW; 

---September---
CREATE TABLE tripdata_202109 (ride_id VARCHAR(225) ,rideable_type TEXT, started_at VARCHAR(225),ended_at VARCHAR(225),start_station_name VARCHAR(225),start_station_id VARCHAR(225),end_station_name VARCHAR(225),
end_station_id TEXT,start_lat VARCHAR(225),start_lng VARCHAR(225),end_lat VARCHAR(225), end_lng VARCHAR(225),member_casual TEXT ,ride_length VARCHAR(225),day_of_week INT);
LOAD DATA INFILE 'C:\\ProgramData\\MySQL\\MySQL Server 8.0\\Uploads\\Cyclistic.XLS\\202102-divvy-tripdata.csv'
INTO TABLE tripdata_202109
FIELDS TERMINATED BY ','
ENCLOSED BY ""
LINES TERMINATED BY '\n'
IGNORE 1 ROW; 

---October---
CREATE TABLE tripdata_202110 (ride_id VARCHAR(225) ,rideable_type TEXT, started_at VARCHAR(225),ended_at VARCHAR(225),start_station_name VARCHAR(225),start_station_id VARCHAR(225),end_station_name VARCHAR(225),
end_station_id TEXT,start_lat VARCHAR(225),start_lng VARCHAR(225),end_lat VARCHAR(225), end_lng VARCHAR(225),member_casual TEXT ,ride_length VARCHAR(225),day_of_week INT);
LOAD DATA INFILE 'C:\\ProgramData\\MySQL\\MySQL Server 8.0\\Uploads\\Cyclistic.XLS\\202102-divvy-tripdata.csv'
INTO TABLE tripdata_202110
FIELDS TERMINATED BY ','
ENCLOSED BY ""
LINES TERMINATED BY '\n'
IGNORE 1 ROW; 

---November---
CREATE TABLE tripdata_202111 (ride_id VARCHAR(225) ,rideable_type TEXT, started_at VARCHAR(225),ended_at VARCHAR(225),start_station_name VARCHAR(225),start_station_id VARCHAR(225),end_station_name VARCHAR(225),
end_station_id TEXT,start_lat VARCHAR(225),start_lng VARCHAR(225),end_lat VARCHAR(225), end_lng VARCHAR(225),member_casual TEXT ,ride_length VARCHAR(225),day_of_week INT);
LOAD DATA INFILE 'C:\\ProgramData\\MySQL\\MySQL Server 8.0\\Uploads\\Cyclistic.XLS\\202102-divvy-tripdata.csv'
INTO TABLE tripdata_202111
FIELDS TERMINATED BY ','
ENCLOSED BY ""
LINES TERMINATED BY '\n'
IGNORE 1 ROW; 

---December---
CREATE TABLE tripdata_202112 (ride_id VARCHAR(225) ,rideable_type TEXT, started_at VARCHAR(225),ended_at VARCHAR(225),start_station_name VARCHAR(225),start_station_id VARCHAR(225),end_station_name VARCHAR(225),
end_station_id TEXT,start_lat VARCHAR(225),start_lng VARCHAR(225),end_lat VARCHAR(225), end_lng VARCHAR(225),member_casual TEXT ,ride_length VARCHAR(225),day_of_week INT);
LOAD DATA INFILE 'C:\\ProgramData\\MySQL\\MySQL Server 8.0\\Uploads\\Cyclistic.XLS\\202102-divvy-tripdata.csv'
INTO TABLE tripdata_202112
FIELDS TERMINATED BY ','
ENCLOSED BY ""
LINES TERMINATED BY '\n'
IGNORE 1 ROW; 
```

#### 3.2: Merging Datasets

Merging all tables into one table (cyclistic.tripdata_2021)

```SQL
CREATE TABLE tripdata_2021 AS(SELECT ride_id ,rideable_type ,started_at ,ended_at ,start_station_name ,start_station_id ,end_station_name ,end_station_id ,start_lat ,start_lng ,end_lat ,end_lng ,member_casual ,ride_length ,day_of_week 
FROM cyclistic.tripdata_202101
UNION ALL 
SELECT ride_id, rideable_type ,started_at ,ended_at ,start_station_name ,start_station_id ,end_station_name ,end_station_id ,start_lat ,start_lng ,end_lat ,end_lng ,member_casual ,ride_length ,day_of_week FROM cyclistic.tripdata_202102
UNION ALL 
SELECTride_id  ,rideable_type ,started_at ,ended_at ,start_station_name ,start_station_id ,end_station_name ,end_station_id ,start_lat ,start_lng ,end_lat ,end_lng ,member_casual ,ride_length ,day_of_week FROM cyclistic.tripdata_202103
UNION ALL 
SELECT ride_id  ,rideable_type ,started_at ,ended_at ,start_station_name ,start_station_id ,end_station_name ,end_station_id ,start_lat ,start_lng ,end_lat ,end_lng ,member_casual ,ride_length ,day_of_week FROM cyclistic.tripdata_202104
UNION ALL
SELECTride_id  ,rideable_type ,started_at ,ended_at ,start_station_name ,start_station_id ,end_station_name ,end_station_id ,start_lat ,start_lng ,end_lat ,end_lng ,member_casual ,ride_length ,day_of_week FROM cyclistic.tripdata_202105
UNION ALL
SELECT ride_id  ,rideable_type ,started_at ,ended_at ,start_station_name ,start_station_id ,end_station_name ,end_station_id ,start_lat ,start_lng ,end_lat ,end_lng ,member_casual ,ride_length ,day_of_week FROM cyclistic.tripdata_202106
UNION ALL
SELECT ride_id  ,rideable_type ,started_at ,ended_at ,start_station_name ,start_station_id ,end_station_name ,end_station_id ,start_lat ,start_lng ,end_lat ,end_lng ,member_casual ,ride_length ,day_of_week FROM cyclistic.tripdata_202107
UNION ALL
SELECTride_id  ,rideable_type ,started_at ,ended_at ,start_station_name ,start_station_id ,end_station_name ,end_station_id ,start_lat ,start_lng ,end_lat ,end_lng ,member_casual ,ride_length ,day_of_week FROM cyclistic.tripdata_202108
UNION ALL
SELECT ride_id  ,rideable_type ,started_at ,ended_at ,start_station_name ,start_station_id ,end_station_name ,end_station_id ,start_lat ,start_lng ,end_lat ,end_lng ,member_casual ,ride_length ,day_of_week FROM cyclistic.tripdata_202109
UNION ALL
SELECT ride_id  ,rideable_type ,started_at ,ended_at ,start_station_name ,start_station_id ,end_station_name ,end_station_id ,start_lat ,start_lng ,end_lat ,end_lng ,member_casual ,ride_length ,day_of_week FROM cyclistic.tripdata_202110
UNION ALL
SELECT ride_id  ,rideable_type ,started_at ,ended_at ,start_station_name ,start_station_id ,end_station_name ,end_station_id ,start_lat ,start_lng ,end_lat ,end_lng ,member_casual ,ride_length ,day_of_week FROM cyclistic.tripdata_202110
UNION ALL
SELECT ride_id  ,rideable_type ,started_at ,ended_at ,start_station_name ,start_station_id ,end_station_name ,end_station_id ,start_lat ,start_lng ,end_lat ,end_lng ,member_casual ,ride_length ,day_of_week 
FROM cyclistic.tripdata_202111
UNION ALL
SELECT ride_id  ,rideable_type ,started_at ,ended_at ,start_station_name ,start_station_id ,end_station_name ,end_station_id ,start_lat ,start_lng ,end_lat ,end_lng ,member_casual ,ride_length ,day_of_week FROM cyclistic.tripdata_202112);
```
#### 3.3 Cleaning Data (Filtering, Transforming)

In the previous section, the datatype of started_at and ended_at columns are supposed to be datetime. However, I input it as a string datatype. 
Hence, both columns are needed to be cast as datetime. Following are the actions taken for data cleaning. 

- ```cast``` the field to datetime type while retrieving other columns
* ```distinct``` remove the duplicate value 
+ use ```WEEKDAY``` function to sort out the day of week for each record

Also, use the ```create view `` command to create a temporary table that will not affect other tables. 

 ```SQL
-- retrieving filtered and cleaned data --- 

CREATE VIEW cyclistic.TRIPDATA AS SELECT
distinct(ride_id), ---------------------------------------------------------- remove the duplicate value 
rideable_type,
cast(str_to_date(started_at,'%d/%m/%y %H:%i') as datetime) as started_at, --- cast the field to datetime type while retrieving other columns 
cast(str_to_date(ended_at,'%d/%m/%y %H:%i') as datetime) as ended_at,     --- cast the field to datetime type while retrieving other columns 
start_station_name, 
start_station_id ,
end_station_name ,
end_station_id ,
start_lat ,
start_lng ,
end_lat,
end_lng,
member_casual ,
WEEKDAY(started_at) AS day_of_week, ------------------------------------------ use WEEKDAY function to sort out the day of week for each record 
 (CASE 
when day_of_Week = 6 then 'Sunday' 
when day_of_Week = 0 then 'Monday' 
when day_of_Week = 1 then 'Tuesday'
when day_of_Week = 2 then 'Wednesday'
when day_of_Week = 3 then 'Thursday'
when day_of_Week = 4 then 'Friday'
when day_of_Week = 5 then 'Saturday'
end ) AS weekday_weekend,
MINUTE(datediff(ended_at , started_at)) as ride_length ----------------------- using the DATEDIFF function to calculate the ride length of each users
FROM cyclistic.tripdata_2021
WHERE start_station_name !='' and  end_station_name != '' 
HAVING ride_length > MINUTE(0)
```

## Phase 4 Analyze (Tableau)   

Once turning datasets into a usable format, I export them into a ```csv.file``` and then import into Tableau software to visualise data. The ***following diagrams*** are the trends that I've identified during the data visualization process.

### 4.1 ```Average Ride Duration```    
<img src="https://i.imgur.com/JOUZW7q.png" height="450" width="600">

### 4.2 ``` Trip Count per rider``` 
<sub> Looking at the total count of trips for each day of the week, members take more trips during the weekdays than casual riders; except during weekends, the number of trips taken by casual riders exceeds members. We then can deduce that the majority of the member users use bikes for commuting to the workplace. This can be further supported by looking at the number of riders taken throughout the day.</sub> 

<img src="https://i.imgur.com/X8WaZkv.png" height="450" width="600">

###  4.3 ``` Hourly Traffic User Analysis```
<sub> Here, we can see that members take more bike rides overall than casual riders throughout the day. Ridership peaks around 8 am, 12 pm, and 6 pm, suggesting an increase in rides during the morning, lunch, and evening rush hours of the day. </sub>  

 <img src="https://i.imgur.com/ghp4lWs.png" height="450" width="600">

### 4.4 ```Monthly User Traffic```
<sub>Looking at the combined year, casual riders exceed members in number of bike rides between mid-May and mid-August, perhaps suggesting an increase in locals on vacation and tourists visiting Chicago during the summer months. </sub>    

<img src="https://i.imgur.com/rBuNeX0.png" height="450" width="600">

### 4.5 ```Most Popular Stations for Riders```   
<sub> Top 10 popular stations for casual and member users </sub>   

<img src="https://i.imgur.com/KibFps2.png" height="450" width="800">

## 5.Share  
### Findings   
```Members:```   
- Members are more likely ***daily travellers*** who take bikes consistently during weekdays than casual riders
+ Their ***average trip duration of 12.83 minutes*** is seven minutes less than the average trip length of casual users 
* Their ***ridership peaks around rush hour time during the day*** but declines during winter months    

```Casual Riders:```
- Casual Riders may be ***a mixture of locals and tourists*** who ride bikes for longer period and more often on the weekend. 
+ Their ***average trip duration is twice longer*** than average ride length of members riders 
* Their ***ridership peaks above members during the summer months***

## 6.Act  
### Recommendations 
I recommend a marketing campaign pinpointing the perks of subscribing to a membership pass such as lower cost per hour, access to booking system, and a loyalty program. 
- The place near the ***top 20 most popular stations should advertise heavily*** because it has the highest traffic across 200 stations which contributing to huge part of the profit. 
- During the cold season such as winters, ***promotion on membership*** could be considered to increase the ridership during the off season. 
- The ***social media marketing or advertisement*** should be more frequent during the peaks of days ( 8am, 12pm, 6pm) , months (summers). 
