# GSP787 —— Insights from Data with BigQuery

<div align="center">
  <img src="https://i.imgur.com/0Oezy0M.png" alt="GSP787 —— Insights from Data with BigQuery">
</div>

<details>
  <summary>
    <strong>Table of Contents</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

- [GSP787 —— Insights from Data with BigQuery](#gsp787--insights-from-data-with-bigquery)
  - [Overview](#overview)
  - [Challenge Scenario](#challenge-scenario)
  - [Query 1: Total Confirmed Cases](#query-1-total-confirmed-cases)
    - [Description](#description)
    - [Solution (Google Cloud Console)](#solution-google-cloud-console)
    - [Solution (Command Line Interface)](#solution-command-line-interface)
    - [References](#references)
  - [Query 2: Worst Affected Areas](#query-2-worst-affected-areas)
    - [Description](#description-1)
    - [Solution (Google Cloud Console)](#solution-google-cloud-console-1)
    - [Solution (Command Line Interface)](#solution-command-line-interface-1)
    - [References](#references-1)
  - [Query 3: Identifying Hotspots](#query-3-identifying-hotspots)
    - [Description](#description-2)
    - [Solution (Google Cloud Console)](#solution-google-cloud-console-2)
    - [Solution (Command Line Interface)](#solution-command-line-interface-2)
    - [References](#references-2)
  - [Query 4: Fatality Ratio](#query-4-fatality-ratio)
    - [Description](#description-3)
    - [Solution (Google Cloud Console)](#solution-google-cloud-console-3)
    - [Solution (Command Line Interface)](#solution-command-line-interface-3)
    - [References](#references-3)
  - [Query 5: Identifying specific day](#query-5-identifying-specific-day)
    - [Description](#description-4)
    - [Solution (Google Cloud Console)](#solution-google-cloud-console-4)
    - [Solution (Command Line Interface)](#solution-command-line-interface-4)
    - [References](#references-4)
  - [Query 6: Finding days with zero net new cases](#query-6-finding-days-with-zero-net-new-cases)
    - [Description](#description-5)
    - [Solution (Google Cloud Console)](#solution-google-cloud-console-5)
    - [Solution (Command Line Interface)](#solution-command-line-interface-5)
    - [References](#references-5)
  - [Query 7: Doubling rate](#query-7-doubling-rate)
    - [Description](#description-6)
    - [Solution (Google Cloud Console)](#solution-google-cloud-console-6)
    - [Solution (Command Line Interface)](#solution-command-line-interface-6)
    - [References](#references-6)
  - [Query 8: Recovery rate](#query-8-recovery-rate)
    - [Description](#description-7)
    - [Solution (Google Cloud Console)](#solution-google-cloud-console-7)
    - [Solution (Command Line Interface)](#solution-command-line-interface-7)
    - [References](#references-7)
  - [Query 9: CDGR - Cumulative Daily Growth Rate](#query-9-cdgr---cumulative-daily-growth-rate)
    - [Description](#description-8)
    - [Solution (Google Cloud Console)](#solution-google-cloud-console-8)
    - [Solution (Command Line Interface)](#solution-command-line-interface-8)
    - [References](#references-8)
  - [Task: Create a Datastudio report](#task-create-a-datastudio-report)
    - [Description](#description-9)
    - [Solution (Google Cloud Console)](#solution-google-cloud-console-9)
    - [Solution (Command Line Interface)](#solution-command-line-interface-9)
    - [References](#references-9)

</details>

<details>
  <summary>
    <strong>Quest Outline</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

| Level | Code | Name | Note |
| :--: | :--: | :-- | :--: |
| Introductory | `GSP281` | [Introduction to SQL for BigQuery and Cloud SQL](https://google.qwiklabs.com/focuses/2802?parent=catalog) | [EN](../../normal-labs/GSP281_Introduction-to-SQL-for-BigQuery-and-Cloud-SQL/) |
| Introductory | `GSP072` | [BigQuery: Qwik Start - Console](https://google.qwiklabs.com/focuses/1145?parent=catalog) | [EN](../../normal-labs/GSP072_BigQuery-Qwik-Start-Console/) |
| Introductory | `GSP071` | [BigQuery: Qwik Start - Command Line](https://google.qwiklabs.com/focuses/577?parent=catalog) | [EN](../../normal-labs/GSP071_BigQuery-Qwik-Start-Command-Line/) |
| Fundamental | `GSP407` | [Exploring Your Ecommerce Dataset with SQL in Google BigQuery](https://google.qwiklabs.com/focuses/3618?parent=catalog) | [EN](../../normal-labs/GSP407_Exploring-Your-Ecommerce-Dataset-with-SQL-in-Google-BigQuery/) |
| Fundamental | `GSP408` | [Troubleshooting Common SQL Errors with BigQuery](https://google.qwiklabs.com/focuses/3642?parent=catalog) |  |
| Introductory | `GSP409` | [Explore and Create Reports with Data Studio](https://google.qwiklabs.com/focuses/3614?parent=catalog) |  |
| Expert | `GSP787` | [Insights from Data with BigQuery: Challenge Lab](https://google.qwiklabs.com/focuses/11988?parent=catalog) |  |

</details>

## Overview

This lab is recommended for students who have enrolled in the [Insights from Data with BigQuery](https://google.qwiklabs.com/quests/123) quest. Are you ready for the challenge?

## Challenge Scenario

You're part of a public health organization which is tasked with identifying answers to queries related to the Covid-19 pandemic. Obtaining the right answers will help the organization in planning and focusing healthcare efforts and awareness programs appropriately.

The dataset and table that will be used for this analysis will be: `bigquery-public-data`.`covid19_open_data.covid19_open_data`. This repository contains country-level datasets of daily time-series data related to COVID-19 globally. It includes data relating to demographics, economy, epidemiology, geography, health, hospitalizations, mobility, government response, and weather.

## Query 1: Total Confirmed Cases

### Description

Build a query that will answer "What was the total count of confirmed cases on Apr 15, 2020?" The query needs to return a single row containing the sum of confirmed cases across all countries. The name of the column should be `total_cases_worldwide`.

### Solution (Google Cloud Console)

```sql
SELECT
  SUM(cumulative_confirmed) AS total_cases_worldwide
FROM
  `bigquery-public-data.covid19_open_data.covid19_open_data`
WHERE
  date = "2020-04-15"
```

### Solution (Command Line Interface)

### References

## Query 2: Worst Affected Areas

### Description

Build a query for answering "How many states in the US had more than 100 deaths on Apr 10, 2020?" The query needs to list the output in the field `count_of_states`.

**Hint**: Don't include `NULL` values.

### Solution (Google Cloud Console)

```sql
WITH
  deaths_by_states AS (
  SELECT
    subregion1_name AS state,
    SUM(cumulative_deceased) AS death_count
  FROM
    `bigquery-public-data.covid19_open_data.covid19_open_data`
  WHERE
    country_name="United States of America"
    AND date='2020-04-10'
    AND subregion1_name IS NOT NULL
  GROUP BY
    subregion1_name )
SELECT
  COUNT(*) AS count_of_states
FROM
  deaths_by_states
WHERE
  death_count > 100
```

### Solution (Command Line Interface)

### References

## Query 3: Identifying Hotspots

### Description

Build a query that will answer "List all the states in the United States of America that had more than 1000 confirmed cases on Apr 10, 2020?" The query needs to return the State Name and the corresponding confirmed cases arranged in descending order. Name of the fields to return `state` and `total_confirmed_cases`.

### Solution (Google Cloud Console)

```sql
SELECT
  *
FROM (
  SELECT
    subregion1_name AS state,
    SUM(cumulative_confirmed) AS total_confirmed_cases
  FROM
    `bigquery-public-data.covid19_open_data.covid19_open_data`
  WHERE
    country_code="US"
    AND date='2020-04-10'
    AND subregion1_name IS NOT NULL
  GROUP BY
    subregion1_name
  ORDER BY
    total_confirmed_cases DESC )
WHERE
  total_confirmed_cases > 1000
```

### Solution (Command Line Interface)

### References

## Query 4: Fatality Ratio

### Description

Build a query that will answer "What was the case-fatality ratio in Italy for the month of April 2020?" Case-fatality ratio here is defined as (total deaths / total confirmed cases) * 100. Write a query to return the ratio for the month of April 2020 and containing the following fields in the output: `total_confirmed_cases`, `total_deaths`, `case_fatality_ratio`.

### Solution (Google Cloud Console)

```sql
SELECT
  SUM(cumulative_confirmed) AS total_confirmed_cases,
  SUM(cumulative_deceased) AS total_deaths,
  (SUM(cumulative_deceased)/SUM(cumulative_confirmed))*100 AS case_fatality_ratio
FROM
  `bigquery-public-data.covid19_open_data.covid19_open_data`
WHERE
  country_name="Italy"
  AND date BETWEEN "2020-04-01"
  AND "2020-04-30"
```

### Solution (Command Line Interface)

### References

## Query 5: Identifying specific day

### Description

Build a query that will answer: "On what day did the total number of deaths cross 10000 in Italy?" The query should return the date in the format `yyyy-mm-dd`.

### Solution (Google Cloud Console)

```sql
SELECT
  date
FROM
  `bigquery-public-data.covid19_open_data.covid19_open_data`
WHERE
  country_name = 'Italy'
  AND cumulative_deceased > 10000
ORDER BY
  date
LIMIT
  1
```

### Solution (Command Line Interface)

### References

## Query 6: Finding days with zero net new cases

### Description

The following query is written to identify the number of days in India between 21 Feb 2020 and 15 March 2020 when there were zero increases in the number of confirmed cases. However it is not executing properly. You need to update the query to complete it and obtain the result:

```sql
WITH india_cases_by_date AS (
  SELECT
    date,
    SUM(cumulative_confirmed) AS cases
  FROM
    `bigquery-public-data.covid19_open_data.covid19_open_data`
  WHERE
    country_name="India"
    AND date between '2020-02-21' and '2020-03-15'
  GROUP BY
    date
  ORDER BY
    date ASC
 )

, india_previous_day_comparison AS
(SELECT
  date,
  cases,
  LAG(cases) OVER(ORDER BY date) AS previous_day,
  cases - LAG(cases) OVER(ORDER BY date) AS net_new_cases
FROM india_cases_by_date
)
```

### Solution (Google Cloud Console)

### Solution (Command Line Interface)

### References

## Query 7: Doubling rate

### Description

Using the previous query as a template, write a query to find out the dates on which the confirmed cases increased by more than 10% compared to the previous day (indicating doubling rate of ~ 7 days) in the US between the dates March 22, 2020 and April 20, 2020. The query needs to return the list of dates, the confirmed cases on that day, the confirmed cases the previous day, and the percentage increase in cases between the days. Use the following names for the returned fields: `Date`, `Confirmed_Cases_On_Day`, `Confirmed_Cases_Previous_Day` and `Percentage_Increase_In_Cases`.

### Solution (Google Cloud Console)

```sql
WITH
  us_cases_by_date AS (
  SELECT
    date,
    SUM( cumulative_confirmed ) AS cases
  FROM
    `bigquery-public-data.covid19_open_data.covid19_open_data`
  WHERE
    country_name="United States of America"
    AND date BETWEEN '2020-03-22'
    AND '2020-04-20'
  GROUP BY
    date
  ORDER BY
    date ASC ),
  us_previous_day_comparison AS (
  SELECT
    date,
    cases,
    LAG(cases) OVER(ORDER BY date) AS previous_day,
    cases - LAG(cases) OVER(ORDER BY date) AS net_new_cases,
    (cases - LAG(cases) OVER(ORDER BY date))*100/LAG(cases) OVER(ORDER BY date) AS percentage_increase
  FROM
    us_cases_by_date )
SELECT
  Date,
  cases AS Confirmed_Cases_On_Day,
  previous_day AS Confirmed_Cases_Previous_Day,
  percentage_increase AS Percentage_Increase_In_Cases
FROM
  us_previous_day_comparison
WHERE
  percentage_increase > 10
```

### Solution (Command Line Interface)

### References

## Query 8: Recovery rate

### Description

Build a query to list the recovery rates of countries arranged in descending order (limit to 10) on the date May 10, 2020. Restrict the query to only those countries having more than 50K confirmed cases. The query needs to return the following fields: `country`, `recovered_cases`, `confirmed_cases`, `recovery_rate`.

### Solution (Google Cloud Console)

```sql
WITH
  cases_by_country AS (
  SELECT
    country_name AS country,
    SUM(cumulative_confirmed) AS cases,
    SUM(cumulative_recovered) AS recovered_cases
  FROM
    `bigquery-public-data.covid19_open_data.covid19_open_data`
  WHERE
    date="2020-05-10"
  GROUP BY
    country_name ),
  recovered_rate AS (
  SELECT
    country,
    cases,
    recovered_cases,
    (recovered_cases * 100)/cases AS recovery_rate
  FROM
    cases_by_country )
SELECT
  country,
  cases AS confirmed_cases,
  recovered_cases,
  recovery_rate
FROM
  recovered_rate
WHERE
  cases > 50000
ORDER BY
  recovery_rate DESC
LIMIT
  10
```

### Solution (Command Line Interface)

### References

## Query 9: CDGR - Cumulative Daily Growth Rate

### Description

The following query is trying to calculate the CDGR on May 10, 2020(Cumulative Daily Growth Rate) for France since the day the first case was reported. The first case was reported on Jan 24, 2020. The CDGR is calculated as:

```
((last_day_cases/first_day_cases)^1/days_diff)-1)
```

Where :

- `last_day_cases` is the number of confirmed cases on May 10, 2020
- `first_day_cases` is the number of confirmed cases on Feb 02, 2020
- `days_diff` is the number of days between Feb 02 - May 10, 2020

The query isn’t executing properly. Can you fix the error to make the query execute successfully?

```sql
WITH
  france_cases AS (
  SELECT
    date,
    SUM(cumulative_confirmed) AS total_cases
  FROM
    `bigquery-public-data.covid19_open_data.covid19_open_data`
  WHERE
    country_name="France"
    AND date IN ('2020-01-24',
      '2020-05-10')
  GROUP BY
    date
  ORDER BY
    date)
, summary as (
SELECT
  total_cases AS first_day_cases,
  LEAD(total_cases) AS last_day_cases,
  DATE_DIFF(LEAD(date) OVER(ORDER BY date),date, day) AS days_diff
FROM
  france_cases
LIMIT 1
)

select first_day_cases, last_day_cases, days_diff, SQRT((last_day_cases/first_day_cases),(1/days_diff))-1 as cdgr
from summary
```

**Note**: Refer to the following [page](https://cloud.google.com/bigquery/docs/reference/standard-sql/functions-and-operators) to learn more about the SQL function referenced `LEAD()`.

### Solution (Google Cloud Console)

```sql
WITH
  france_cases AS (
  SELECT
    date,
    SUM(cumulative_confirmed) AS total_cases
  FROM
    `bigquery-public-data.covid19_open_data.covid19_open_data`
  WHERE
    country_name="France"
    AND date IN ('2020-01-24',
      '2020-05-10')
  GROUP BY
    date
  ORDER BY
    date),
  summary AS (
  SELECT
    total_cases AS first_day_cases,
    LEAD(total_cases) OVER(ORDER BY date) AS last_day_cases,
    DATE_DIFF(LEAD(date) OVER(ORDER BY date),date, day) AS days_diff
  FROM
    france_cases
  LIMIT
    1 )
SELECT
  first_day_cases,
  last_day_cases,
  days_diff,
  POWER(last_day_cases/first_day_cases,1/days_diff)-1 AS cdgr
FROM
  summary
```

### Solution (Command Line Interface)

### References

## Task: Create a Datastudio report

### Description

Create a Datastudio report that plots the following for the United States:

- Number of Confirmed Cases
- Number of Deaths
- Date range : 2020-03-15 to 2020-04-30

### Solution (Google Cloud Console)

```sql
SELECT
  date,
  SUM(cumulative_confirmed) AS country_cases,
  SUM(cumulative_deceased) AS country_deaths
FROM
  `bigquery-public-data.covid19_open_data.covid19_open_data`
WHERE
  date BETWEEN '2020-03-15'
  AND '2020-04-30'
  AND country_name='United States of America'
GROUP BY
  date
```

1. Click **EXPLORE DATA** > **Explore with Data Studio**.
2. Click **AUTHORIZE** on the **Welcome to Google Data Studio** dialog.
3. In the Data Studio report, select **Add a chart** > **Time-series Chart**.
4. Add `country_cases` and `country_deaths` to the Metric field.
5. Click **Save**.

### Solution (Command Line Interface)

### References