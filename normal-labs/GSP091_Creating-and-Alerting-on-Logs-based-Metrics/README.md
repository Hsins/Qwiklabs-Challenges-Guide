# GSP091 —— Creating and Alerting on Logs-based Metrics

<details>
  <summary>
    <strong>Table of Contents</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

- [Overview](#overview)
- [System Defined Logs-based Metrics](#system-defined-logs-based-metrics)
- [User Defined Logs-based Metrics](#user-defined-logs-based-metrics)
- [Labels](#labels)
- [References](#references)

</details>

## Overview

Logs-based metrics are [Cloud Monitoring](https://cloud.google.com/monitoring/docs/) metrics that are based on the content of log entries. It can help you identify trends, extract numeric values out of the logs, and set up an alert when a certain log entry occurs by creating a metric for that event. You can use both system and user-defined logs-based metrics in Cloud Monitoring to create charts and alerting policies. Logs-based metrics are time series that are generated from data in logs.

## System Defined Logs-based Metrics

System defined logs-based metrics are ready to use right out of the box. These system [logs-based metrics](https://cloud.google.com/monitoring/api/metrics_gcp#gcp-logging) include:

- **Metrics around logs ingested**
  - `Byte_count`: Number of bytes in all log entries ingested. This is broken down by monitored resource type, log stream name, and severity level.
- **Metrics around logs excluded**
  - `Excluded_byte_count`: Number of bytes in log entries that were excluded. This is broken down by the monitored resource type.
  - `Excluded_log_entry_count`: Number of log entries that were excluded. This is broken down by the monitored resource type.
- **Metrics around logs based metrics**
  - `Dropped_log_entry_count`: Despite the name, this does not show log entries dropped by Cloud logging but rather the number of log entries that did not contribute to logs based metrics because they arrived too late.
  - `Log_entry_count`: Number of log entries that contributed to logs based metrics so that dropped_log_entry_count + log_entry_count is the total number of log entries ingested by Cloud Logging.
  - `Metric_throttled`: Indicates if points are being dropped for logs-based metrics due to exceeding time series limits.
  - `Time_series_count`: Estimate of the active time series count for logs-based metrics.

Most system logs-based metrics are counter metrics. **Counter metrics** count the number of log entries that match an advanced logs filter.

## User Defined Logs-based Metrics

**User defined logs-based metrics** are our own logs-based metrics using data from existing logs we created. Follow the steps below to create user defined logs-based metrics:

1. In the Cloud Console, click **Navigation menu** > **Logging** > **Logs Explorer**.
2. Filter for activity logs from the resources.
3. Add criteria and then click **Run Query**.
4. On top right of the Query Results section, click **Actions** drop down and select **Create Metric**.

## Labels

We can also use user defined labels and add them to the user defined logs-based metrics we created.

The [labels](https://cloud.google.com/logging/docs/logs-based-metrics/labels#create-label) allow logs-based metrics to contain multiple time series — one for each label value. All logs-based metrics come with some default labels.

## References

- [Alert on Audit Logging Events | YouTube](https://www.youtube.com/watch?v=LdGqmnoowc8)