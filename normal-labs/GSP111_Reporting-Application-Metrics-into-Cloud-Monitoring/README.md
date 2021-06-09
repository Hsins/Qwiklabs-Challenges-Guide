# GSP111 —— Reporting Application Metrics into Cloud Monitoring

<details>
  <summary>
    <strong>Table of Contents</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

- [GSP111 —— Reporting Application Metrics into Cloud Monitoring](#gsp111--reporting-application-metrics-into-cloud-monitoring)
  - [Overview](#overview)
  - [Install Go and OpenCensus](#install-go-and-opencensus)
  - [Viewing Cloud Function logs & metrics in Cloud monitoring](#viewing-cloud-function-logs--metrics-in-cloud-monitoring)
  - [Create Logs-based Metric](#create-logs-based-metric)
  - [Create Charts on The Monitoring Overview Window](#create-charts-on-the-monitoring-overview-window)
  - [References](#references)

</details>

## Overview

## Install Go and OpenCensus

[OpenCensus](https://opencensus.io/) is an open source framework for metrics collection and distributed tracing. It offers the following benefits to its users:

- Low overhead data collection.
- Standard wire protocols and consistent APIs for handling metrics and trace data.
- Vendor interoperability via the OpenMetrics standard. OpenCensus can ingest into multiple backends in parallel, enabling incremental transitions and side-by-side comparison of backends.
- Correlation with traces and, in the future, log entries.

While multiple methods exist for reporting application metrics to Cloud Monitoring (see Other Methods for Reporting Application Metrics to Cloud Monitoring later in this lab), Google and Cloud Monitoring have adopted OpenCensus officially as the default mechanism for ingestion.

```bash
$ go get go.opencensus.io
$ go get contrib.go.opencensus.io/exporter/stackdriver
$ go mod init test3
$ go mod tidy
```

## Viewing Cloud Function logs & metrics in Cloud monitoring

## Create Logs-based Metric

Logs-based metrics are Cloud Monitoring metrics that are based on the content of log entries.

## Create Charts on The Monitoring Overview Window

## References

