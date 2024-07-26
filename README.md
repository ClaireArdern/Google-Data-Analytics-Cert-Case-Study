<h1> Google Data Analytics Certification Capstone: Case Study</h1>
<h6> The following includes documentation of all work done in the process of completing the capstone project for the Google Data Analytics Certification. This capstone project is a data analytics case study. </h6>

<h2>Scenario</h2>

Imagine you are a junior data analyst working on the marketing analyst team at Bellabeat, a high-tech manufacturer of health-focused products for women. Bellabeat is a successful small company, but they have the potential to become a larger player in the global smart device market. You have been asked to focus on one of Bellabeat’s products and analyze smart device data to gain insight into how consumers are using their smart devices. The insights you discover will then help guide marketing strategy for the company. You will present your analysis to the Bellabeat executive team along with your high-level recommendations for Bellabeat’s marketing strategy.

<h2>Business Task</h2>

Analyze smart device data to gain insight into how customers are using their smart devices.

**Problem Statement:** How can the trends found in the smart device usage data be utilized to improve the BellaBeat marketing strategy? 

<h2>Data Sources</h2>

The dataset used in this case study was provided by the Google Data Analytics Certificate course. This is a public dataset made available by Kaggle user [Mobius](https://www.kaggle.com/arashnic).

This Kaggle data set contains personal fitness tracker data from thirty fitbit users. It includes information about daily activity, steps, and heart rate that can be used to explore users’ habits.

[FitBit Fitness Tracker Data](https://www.kaggle.com/datasets/arashnic/fitbit)

<h3>Dataset Overview</h3>

This dataset is split into 2 time periods: 3/12/16 - 4/11/16 and 4/12/16 - 5/12/16. Initially, due to the mismatched number of files corresponding to each time period, it seems that the second time period includes more information than the first time period. However, this mismatched number of data files is mostly due to duplicate information represented in different formats (e.g. minute by minute rather than day by day). For this study, as we are simply observing usage trends, data that is summarized daily will be sufficient. 

There are 35 distinct IDs included in the first time period (March 2016 - April 2016) and 33 distinct IDs included in the second time period (April 2016 - May 2016). It seems that two of the users (IDs 2891001357 and 6391747486) are only included in the first time period, not the second. Although there is an inqual number of users between the two time periods, as we are simply observing behavior, this disparity should not affect our results.

It should also be noted that there is an overlap of one day (04-12-16) between the two time periods. As there are two users that are unaccounted for in the second period, it is better to use the records corresponding to this date from the first time period. Once we can confirm that the records for this day are the same across both of the time periods (excluding the 2 missing users in the second time period), we can remove this record from the second time period to ensure that the data corresponding to this day is not accounted for twice due to this overlap. 

In order to complete the analysis for each time period using data represented in the daily format rather than hourly or by minute, we will need the following files: 

- From the March 2016 - April 2016 time period:
    - dailyActivity_merged
    - heartrate_seconds_merged (to be converted to daily format)
    - minuteMETsNarrow_merged (to be converted to daily format)
    - minuteSleep_merged (to be converted to daily format)
    - weightLogInfo_merged

- From the April 2016 - May 2016 time period:
    - dailyActivity_merged
    - heartrate_seconds_merged (to be converted to daily format)
    - minuteMETsNarrow_merged (to be converted to daily format)
    - SleepDay_merged
    - weightLogInfo_merged

<h2>Data Cleaning and Manipulation</h2>

In order to simplify the titles of the data files and ensure proper organization, each of the files used were given new names when uploaded to BigQuery for cleaning. These changes are listed in the tables below.

For the first (March 2016 - April 2016) time period:

| Original Title  | Updated Title |
| ------------- | ------------- |
| dailyActivity_merged  | dailyActivity_P1 |
| heartrate_seconds_merged  | heartrate_seconds_P1  |
| minuteMETsNarrow_merged | minuteMETs_P1 |
| minuteSleep_merged | minuteSleep_P1 |
| weightLogInfo_merged | weightLogInfo_P1 |

For the second (April 2016 - May 2016) time period:


| Original Title  | Updated Title |
| ------------- | ------------- |
| dailyActivity_merged  | dailyActivity_P2 |
| heartrate_seconds_merged  | heartrate_seconds_P2  |
| minuteMETsNarrow_merged | minuteMETs_P2 |
| SleepDay_merged | SleepDay_P2 |
| weightLogInfo_merged | weightLogInfo_P2 |

As the included data files were often not logged in the desired daily format, the first task at hand was to correct this in order to ensure proper analysis. The tasks included in this process are as follows:

- Update heartrate_seconds_P1 and heartrate_seconds_P2 to be in the correct date/time format for future operations. Previously, the Time column in these tables was set as a String since the AM/PM format was not supported. After this change, the Time column in these tables is formatted in UTC. 
- Using a nested query, first split the date and time columns in heartrate_seconds_P1 and heartrate_seconds_P2 to be two separate columns: Date and Time. Next, average the daily heart rate for each individual user (Id). This is saved into a separate table for each time period, creating a new heartrate_daily_P1 and heartrate_daily_P2. These new tables each include columns Id, Date, Value. 
    - NOTE: For future queries using the Date column, we should first cast the Date column as Date. This is necessary because we cannot change the datatype of a column in BigQuery.
- Same process as above used for minuteMETs_P1 and minuteMETs_P2 to create METs_Daily_P1 and METs_Daily_P2.
- Update minuteSleep_P1 to match SleepDay_P2. The total number of minutes (records) that had a Value of 1 were counted as TotalMinutesAsleep. The total number of minutes per Id and logId were counted as TotalTimeInBed. The TotalMinutesAsleep and TotalTimeInBed were summed for each day for each Id.  The number of distinct logIds per SleepDay were stored as TotalSleepRecords. The result created a new table SleepDay_P2.

(cleaning still in progress)

<h2>Summary of Data Analysis</h2>

<h2>Key Visualizations and Findings</h2>

<h2>Insights and Recommendations</h2>
