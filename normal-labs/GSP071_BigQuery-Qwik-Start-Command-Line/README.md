# GSP071 —— BigQuery: Qwik Start - Command Line

<details>
  <summary>
    <strong>Table of Contents</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

- [Overview](#overview)
- [Examine Table](#examine-table)
- [Run Query](#run-query)
- [Create New Table](#create-new-table)
- [Clean Up](#clean-up)
- [References](#references)

</details>

## Overview

Storing and querying massive datasets can be time consuming and expensive without the right hardware and infrastructure. BigQuery is an [enterprise data warehouse](https://cloud.google.com/solutions/bigquery-data-warehouse) that solves this problem by enabling super-fast SQL queries using the processing power of Google's infrastructure. Simply move your data into BigQuery and let us handle the hard work. You can control access to both the project and your data based on your business needs, such as giving others the ability to view or query your data.

You can access BigQuery in the [Console](https://cloud.google.com/bigquery/docs/quickstarts/quickstart-web-ui), [Web UI](https://console.cloud.google.com/bigquery?utm_source=bqui&utm_medium=link&utm_campaign=classic&project=cloud-solutions-group) or a [command-line tool](https://cloud.google.com/bigquery/docs/bq-command-line-tool) using a variety of [client libraries](https://cloud.google.com/bigquery/docs/reference/libraries) such as Java, .NET, or Python. There are also a variety of [solution providers](https://cloud.google.com/bigquery) that you can use to interact with BigQuery.

## Examine Table

We can use `bq show` command for examing the schema of the given table.

```bash
$ bq show <PROJECT>:<DATASET.TABLE>
```

## Run Query

To run a query, run the command `bq query "[SQL_STATEMENT]"`.

```bash
$ bq query --use_legacy_sql=false \
'SELECT
   word,
   SUM(word_count) AS count
 FROM
   `bigquery-public-data`.samples.shakespeare
 WHERE
   word LIKE "%raisin%"
 GROUP BY
   word'
```

- Escape any quotation marks inside the `[SQL_STATEMENT]` with a `\` mark.
- Use a different quotation mark type than the surrounding marks `("versus")`.

## Create New Table

Every table is stored inside a dataset. A dataset is a group of resources, such as tables and views.

```bash
# list any existing datasets in our project
$ bq ls

# create a new dataset with given name
$ bq mk <DATASET_NAME>

# create or update a table and load data
$ bq load <DATASET:TABLE> <FILE> <SCHEMA>

# check the schema of given table
$ bq show <DATASET:TABLE>
```

## Clean Up

Run the `bq rm` command to remove the dataset with the `-r` flag to delete all tables in the dataset.

```bash
$ bq rm -r <DATASET>
```

## References

- [Get Meaningful Insights with Google BigQuery | Google Cloud Labs | YouTube](https://www.youtube.com/watch?v=rwZsPjCTkhw)
- [BigQuery: Qwik Start - Qwiklabs Preview | YouTube](https://www.youtube.com/watch?v=dOpNxH64JIU)
- [`bq` command-line tool reference | BigQuery Documentation](https://cloud.google.com/bigquery/docs/reference/bq-cli-reference)