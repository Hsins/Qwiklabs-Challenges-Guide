# GSP407 —— Exploring Your Ecommerce Dataset with SQL in Google BigQuery

<details>
  <summary>
    <strong>Table of Contents</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

- [Overview](#overview)
- [Identify duplicate rows](#identify-duplicate-rows)
- [Analyze The `all_sessions` Table](#analyze-the-all_sessions-table)
  - [Confirm No Duplicates Exist](#confirm-no-duplicates-exist)
  - [Shows Total Unique Visitors](#shows-total-unique-visitors)
- [References](#references)

</details>

## Overview

BigQuery is Google's fully managed, NoOps, low cost analytics database. With BigQuery you can query terabytes and terabytes of data without having any infrastructure to manage or needing a database administrator. BigQuery uses SQL and can take advantage of the pay-as-you-go model. BigQuery allows you to focus on analyzing data to find meaningful insights.

We have a newly available ecommerce dataset that has millions of Google Analytics records for the [Google Merchandise Store](https://shop.googlemerchandisestore.com/) loaded into a table in BigQuery. In this lab, you use a copy of that dataset. Sample scenarios are provided, from which you look at the data and ways to remove duplicate information. The lab then steps you through further analysis the data.

To follow and experiment with the BigQuery queries provided to analyze the data, see [Standard SQL Query Syntax](https://cloud.google.com/bigquery/docs/reference/standard-sql/query-syntax).

## Identify duplicate rows

We use the SQL `GROUP BY` function on every field and counts (`COUNT`) where there are rows that have the same values across every field.

- If every field is unique, the `COUNT` returns 1 as there are no other groupings of rows with the exact same value for all fields.
- If there are multiple rows with the same values for all fields, these rows are grouped together and the `COUNT` will be greater than 1.

```sql
#standardSQL
SELECT COUNT(*) as num_duplicate_rows, * FROM
`data-to-insights.ecommerce.all_sessions_raw`
GROUP BY
fullVisitorId, channelGrouping, time, country, city, totalTransactionRevenue, transactions, timeOnSite, pageviews, sessionQualityDim, date, visitId, type, productRefundAmount, productQuantity, productPrice, productRevenue, productSKU, v2ProductName, v2ProductCategory, productVariant, currencyCode, itemQuantity, itemRevenue, transactionRevenue, transactionId, pageTitle, searchKeyword, pagePathLevel1, eCommerceAction_type, eCommerceAction_step, eCommerceAction_option
HAVING num_duplicate_rows > 1;
```

The last part of the query is an aggregation filter using `HAVING` to only show the results that have a `COUNT` of duplicates greater than 1. Therefore, the number of records that have duplicates will be the same as the number of rows in the resulting table.

## Analyze The `all_sessions` Table

### Confirm No Duplicates Exist

```sql
#standardSQL
# schema: https://support.google.com/analytics/answer/3437719?hl=en
SELECT
fullVisitorId, # the unique visitor ID
visitId, # a visitor can have multiple visits
date, # session date stored as string YYYYMMDD
time, # time of the individual site hit  (can be 0 to many per visitor session)
v2ProductName, # not unique since a product can have variants like Color
productSKU, # unique for each product
type, # a visitor can visit Pages and/or can trigger Events (even at the same time)
eCommerceAction_type, # maps to ‘add to cart', ‘completed checkout'
eCommerceAction_step,
eCommerceAction_option,
  transactionRevenue, # revenue of the order
  transactionId, # unique identifier for revenue bearing transaction
COUNT(*) as row_count
FROM
`data-to-insights.ecommerce.all_sessions`
GROUP BY 1,2,3 ,4, 5, 6, 7, 8, 9, 10,11,12
HAVING row_count > 1 # find duplicates
```

### Shows Total Unique Visitors

```sql
#standardSQL
SELECT
  COUNT(*) AS product_views,
  COUNT(DISTINCT fullVisitorId) AS unique_visitors
FROM `data-to-insights.ecommerce.all_sessions`;
```

## References

- [Query syntax in Standard SQL | BigQuery Documentation](https://cloud.google.com/bigquery/docs/reference/standard-sql/query-syntax)